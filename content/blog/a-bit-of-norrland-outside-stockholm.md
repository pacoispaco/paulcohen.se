---
title: "A Bit of Norrland Outside Stockholm"
date: 2020-07-29T21:57:58+02:00
updated: 2020-07-29T21:57:58+02:00
draft: true
---

This where I was today.

{{< instagram CDPDfLpA2k0 >}}

I found cloudberries and scared up a female black grouse!

And then when I got home, I wrote some Python!

{{< highlight python "linenos=true" >}}
    def authorized_by_roles(self, resource, context):
        assert resource is not None and type(resource) == str
        assert context is None or type(context) == dict
        assert self.ticket is not None, ("No user ticket has been set. Make sure to call "
                                         "'set_user_ticket' with a ticket before calling "
                                         "'is_authorized'.")
        granting_roles = []
        eval_msg = None
        evaluated_resources = self.resources(context=context)
        logger.debug(
            f"resource: {resource}, context: {context}, self.resources: {evaluated_resources}"
        )
        if resource in evaluated_resources:
            # Check which roles grants a privilege to the resource, and make sure to resolve all
            # context attributes in the privileged resources
            for role, rule in evaluated_resources[resource].items():
                logger.debug(f"role: {role}, rule: {rule}")
                parser = RARBACRuleParser()
                if parser.evaluated(rule):
                    granting_roles.append(role)
                    eval_msg = "Ok"
        log_data = {'feature': 'is_authorized',
                    'resource': resource,
                    'context': context,
                    'ticket': self.ticket,
                    'result': len(granting_roles) > 0,
                    'granting_roles': granting_roles,
                    'eval_msg': eval_msg}
        logger.debug(json.dumps(log_data))
        if len(granting_roles) > 0:
            result = 'GRANTED'
        else:
            result = 'DENIED'
        logger.critical(
            f"User '{self.ticket['uid']}' {result} access to resource '{resource} "
            f"by roles {granting_roles} in the context: {context}"
        )
        return granting_roles
{{< /highlight >}}

