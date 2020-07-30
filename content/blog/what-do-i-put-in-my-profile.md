---
title: "What Do I Put in My Profile"
date: 2011-09-17T12:11:04+02:00
updated: 2020-04-24T07:43:04+02:00
draft: true
---

No, this is not about updating a Facebook or CV profile. This is about the `.profile` file and its friends like `.bashrc` on \*nix systems.

I admit that I still get confused about where to put my personal environment settings on a Linux machine. Nowadays I can always google for the answer, but I have now been overcome with a strong desire to try to sort it out and document it for my own sake once and for all. So here goes. Note that I am only talking about the Bash shell here!

First of all, Bash can be run as a login shell or as a normal shell. Bash can also be run in interactive mode, typically in a graphical terminal program, or as an interpreter of Bash scripts. Bash is started as a login shell by passing it the `-login` flag on invocation. This is done by the system when it listed as the login shell for a user in the `/etc/passwd` file.

# Bash as a login shell

The `/etc/profile` file is automatically read by all Bourne compatible shells, including the Bash shell, as the first thing after a successful login. The `/etc/profile` file will typically then call scripts in the directory `/etc/profile.d` and after that, execute the `/etc/bash.bashrc` file. The latter file contains Bash specific settings that are applied to all Bash login shells. All these files contain system wide settings applicable to all login sessions. You shouldn’t mess with these files unless you want to modify the behavior of all login Bash sessions.

After a Bash login shell has read the above mentioned files it will look for the files `~/.bash_profile`, `~/.bash_login`, and `~/.profile` in the current users home directory, and in that order, and it will read and execute the commands from the first file that exists and is readable. Note that these files are only read by Bash if it is invoked as an interactive login shell (or as a non-interactive shell with the `-login` option). Any settings in these files will affect all subsequent processes, including your desktop and other programs that rely on environment variables.

# Bash as a non-login shell

When Bash is invoked as a non-login shell (or without the `–login` option), for example as an interactive shell in a terminal program like xterm or konsole from within a graphical environment, only the users `~/.bashrc` file is executed.

Note that the `~/.bashrc` file is typically not read when Bash is invoked as a login shell!

# Terminating a login Bash shell

When a Bash login shell terminates it reads the `~/.bash_logout` file. So this file is not read on termination of non-login shells! I have never had the need to modify this file.

# Conclusions

Modify the `~/.profile` file for settings you want set upon login and which will affect all subsequent processes started from that login shell. For most situations, this is the file you will want to modify.

Modify the `~/.bashrc` file for settings you want set when starting interactive non-login Bash shells.
