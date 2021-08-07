---
title: "Setting Up a Website With Nginx and Let's Encrypt on Ubuntu 20.04"
date: 2020-08-25T22:15:13+02:00
updated: 2020-08-25T22:15:13+02:00
draft: false
tags:
 - linux
 - sysadmin
 - digital
 - web-dev
tsoc: true
---

# Introduction

This article describes how to set up a website www.example.org with [nginx](https://www.nginx.com/) and [Let's Encrypt](https://letsencrypt.org/) HTTPS certificates on [Ubuntu 20.04](https://releases.ubuntu.com/20.04/). I also describe how to make sure that the same website is served at [https://example.org](https://example.org) {{< sidenote-gvdb "1">}} The domain example.org is a reserved domain name for use in illustrative examples in documents. {{< /sidenote-gvdb >}} and https://www.example.org and that HTTP requests to the server's IP-adress are redirected to https://www.example.org.

The article is based on notes from when I set up this website on a [Digital Ocean droplet](https://www.digitalocean.com/products/droplets/). I mostly followed these articles:

* [How To Install Nginx on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)
* [How To Secure Nginx with Let's Encrypt on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04)

# Enable UFW firewall and enable the OpenSSH UFW profile

This is recommended by Digital Ocean on Ubuntu server 20.04. It will ensure that only connections to certain services on the server are allowed. UFW is disabled by default. Before you enable it make sure to allow OpenSSH!
```bash
$ sudo ufw allow OpenSSH
```

Enable UFW with:
```bash
$ sudo ufw enable
```

You can list the all the available UFW profiles and apps that can be allowed with:
```bash
$ sudo ufw app list
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

# Install nginx and enable its UFW profiles

Install with:
```bash
$ sudo apt install nginx
```

nginx will set up a default virtual server with the config file `/etc/nginx/sites-available/default` and a `/var/www/html/index.nginx-debian.html` file. nginx will also register a few UFW app profiles and you must allow them in order for nginx to serve HTTP and HTTPS. We will allow HTTP until we have set upp HTTPS with Let's encrypt in the end. We also want to allow the nginx Full profile (since that's what the Digital Ocean article above recommends).

To enable the nginx Full profile in UFW:
```bash
$ sudo ufw allow 'Nginx Full'
```

Listing the UFW profiles should produce this output:
```bash
$ sudo ufw app list
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```


Open a browser and enter the ip adress of the server and check that nginx is up and running. You should see the default website page served by nginx:

![welcome-to-nginx.png](/welcome-to-nginx.png)

# Create root directory and dummy index.html file for the website

Create the root directory for the website:
```bash
$ sudo mkdir /var/www/example.org
```

Then change the owner of that directory to yourself and give your self `rwx` rights, and the group owner of that directory to `www-data` and give that group `r-x` rights:
```bash
$ sudo chown username:www-data example.org/
$ chmod 750 example.org/
```

Add a simple `/var/www/example.org/index.html` with the following contents:
```html
<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Example site</title>
  <meta name="description" content="An example website">
  <meta name="author" content="Foo bar">

</head>

<body>
Coming soon!
</body>
</html>
```

Of course, if you already have the files for a working website, you can `scp` the directory structure and the files of that website to `/var/www.example.org/`, and have a working website pronto!

# Create nginx config file for the website

Create the file `/etc/nginx/sites-available/example.org` with the following contents:
```nginx
server {
  listen 80;
  listen [::]:80;

  root /var/www/example.org;

  index index.html;

  server_name example.org www.example.org;

  location / {
    try_files $uri $uri/ =404;
  }
}
```

Note that we make sure that this virtual server will serve requests to both [example.org](https://example.org) and www.example.org.

# Enable the new website

Create a link for the config file from sites-enabled to the config file in sites-available:
```bash
$ sudo ln -s /etc/nginx/sites-available/example.org /etc/nginx/sites-enabled/example.org
```

Restart nginx:
```bash
$ sudo systemctl restart nginx
```

nginx will complain if you've messed up the config file. Make sure it starts without complaining!

Reload the page in the browser and check that the default website page is still served by nginx.

# Set up the DNS-entry for your domain name

Go to your DNS service provider and set up an A entry that points to the ip adress of the Ubuntu server running in the Digiotal Ocean droplet. E.g:
```
example.org -> [A] -> 134.209.201.158
```

It will take some time, up to an hour or couiple of hours, before this DNS update has propagated to all DNS-servers. When that is done, check that the simple `/var/www/example.org/index.html` file is served at both:

 * http://example.org and
 * http://www.example.org

# Set up HTTPS with Let's encrypt

Install Certbot and its Nginx plugin:
```bash
$ sudo apt install certbot python3-certbot-nginx
```

Make sure that you have defined `server_name` for both the [example.org](https://example.org) domain and the www.example.org subdomain in the server block of the nginx config file for the website (which you should have, if you've follwed the steps above). Certbot will look in that config file for the domain names it will generate certificates for.

Certbot provides a variety of ways to obtain SSL certificates through plugins. The Nginx plugin will take care of reconfiguring Nginx and reloading the config whenever necessary. To use this plugin, type the following:
```bash
$ sudo certbot --nginx -d example.org -d www.example.org
```

This runs certbot with the `--nginx` plugin, using `-d` to specify the domain names we’d like the certificate to be valid for. The `/etc/nginx/sites-available/example.org` file should now look like this:
```nginx
server {

  root /var/www/example.org;

  index index.html;

  server_name example.org www.example.org;

  location / {
    try_files $uri $uri/ =404;
  }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/example.org/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/example.org/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}

server {
    if ($host = www.example.org) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    if ($host = example.org) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


  listen 80;
  listen [::]:80;

  server_name example.org www.example.org;
    return 404; # managed by Certbot

}
```

Reload the pages [example.org](https://example.org) and www.example.org in the browser and check that you are correctly redirected to the https://example.org and https://www.example.org

# Verifying Let's encrypt auto-renewal with Certbot

Let’s Encrypt’s certificates are only valid for ninety days. This is to encourage users to automate their certificate renewal process. The certbot package we installed takes care of this for us by adding a systemd timer that will run twice a day and automatically renew any certificate that’s within thirty days of expiration.

You can query the status of the timer with systemctl:
```
$ sudo systemctl status certbot.timer
```

# Ensure that HTTP requests to the server's IP adress are redirected to the website

Add a server block to the `/etc/nginx/sites-available/example.org` like this:
```nginx
# This server block is for redirecting HTTP requests to the servers IP adress to https://www.example.org
server {
  listen 80;
  listen [::]:80;
  server_name 134.209.201.158;

  add_header X-Frame-Options "SAMEORIGIN";

  return 301 https://www.example.org$request_uri;
}
```

# Set up a custom 404 page

Use the `error_page` directive so that when a 404 error occurs (when a requested file is not found), the custom page you created is served. Create a location block for the file, and ensure that the root matches our file system location and that the file is only accessible through internal Nginx redirects (and not requestable directly by clients):
```apache
server {

        root /var/www/example.org;

        . . .

        error_page 404 /404.html;
        location = /404.html {
                root /usr/share/nginx/html;
                internal;
        }
}
```

Of course we need to add our custom `404.html` page to the root directory of our website at `/var/www/example.org/404.html`.
