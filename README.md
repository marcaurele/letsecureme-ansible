# Ansible playbook to setup a secured Nginx web server

This is an Ansible playbook to configure a server following the recommendations
from https://letsecure.me.

## Inventory file

Create your inventory file with those 2 variables:
 - `domains`: a list of domain addresses which your webserver should server
 - `email`: the email address used to generate the let's encrypt certificate
 - `test`: create a test certificate if defined

```
[letsecureme]
198.51.100.1 domains="['yourdomain.here', 'www.yourdomain.here']" email=your-email
```

*The domains must already be defined on a DNS server so that let's encrypt can
make a HTTP call.*

## Execute the playbook

```
# To generate a test certificate
ansible-playbook -i hosts letsecureme.yml --extra-vars "test=true"

# To generate a true let's encrypt certificate
ansible-playbook -i hosts letsecureme.yml
```

Now your domain should server the demo page on the addresses you have defined
with a state of the art secured web configuration for nginx. Of course the
playbook is idempotent so you can run it as many time as you want.