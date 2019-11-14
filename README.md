 OpenSSH Server
==============

Ansible role to configure the OpenSSH `ssh` server.
Use Eliptic cureve cryptografie for your ssh keys e.g.:
```bash
ssh-keygen -t ed25519
```

 combinations
---------------
It is highly recomended to use this role together with a role to manage users and to manage the sshd configuration.<br/>
The following roles are tested in combination and work well - at least for the user [DO1JLR](https://github.com/do1jlr):
 - [github.com/chaos-bodensee/role-manage_users](https://github.com/chaos-bodensee/role-manage_users.git)
 - [github.com/chaos-bodensee/role-ssh_authorized_keys](https://github.com/chaos-bodensee/role-ssh_authorized_keys.git)
 - [github.com/chaos-bodensee/role_sshd](https://github.com/chaos-bodensee/role_sshd.git) *(this one)*


 Some Variables explained
------------------------------
**Remember:** Have a look into ``defaults/main.yml`` for all possible variables.

```bash
restrict_allow_users: True
```
With tis option you can enable or disable if a user needs to be in a special defined group. Like wheels, sudo or something else.
The default ddh groups are ``admins`` and ``root``

```bash
only_allow_ed25519: true 
```
Force ssh to deny all ssh keys except for eliptic curve ed25519 keys.

```bash
sshd_password_authentication: 'no' 
```
Change the string from 'no' to 'yes' if you want to log in with a password (not recomended).

There are some other cryptographic algorythmen you could enable...

### Important part:
Define the users (and optional their ssh keys) for the ssh config template:
```bash
users:
  l3d:
    - l3d
  ottojo:
   - ottojo@uni
   - ottojo@home
```
-> This means l3d and ottojo are able to login.


 Files
-----

* `sshd.conf`:


 References
----------

* [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

 Don't forget:
--------------
 + This role will not deploy or touch any ssh public keys. There are other roles to do that.
 + Be carefull if you don't have a eliptic curve ed25519 key. ``only_allow_ed25519: true`` is the default option.
   * If you really have to deal with RSA Keys or simmilar, you should think about a backup ed25519 ssh key. Better a backup than beeing locked out!
