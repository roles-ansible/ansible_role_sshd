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
 - [github.com/roles-ansible/ansible_role_sshd](https://github.com/roles-ansible/ansible_role_sshd.git) *(this one)*


 Some Variables explained
------------------------------
**Remember:** Have a look into ``defaults/main.yml`` for all possible variables.

+ **SSH Port**<br/>
  The OpenSSH Port is defined with the variable ``sshd__port: 22``. Change it if you wish.

+ **Allowed Users and Groups**<br/>
  The default users that are allowd to login come from the ``users: {}`` list.<br/>
  The same ``users: {}`` variable is used in the other recomended ssh roles.<br/>
  A example to allow the login for the users and groups called ``l3d`` and ``ottojo`` are:
```
users:
  l3d:
    - l3d
  ottojo:
   - ottojo@uni
   - ottojo@home
```

+ **SSH Login via Passwort**<br/>
  The SSH Passwort auth is set to false via ``sshd__password_authentication: false``. This won't allow you to use your passwort to login via SSH.

+ **Manage SSH Key Types**<br/>
  By default this role configure which ssh key types are allowed to login. If you don't want to define that change the ``sshd__manage_key_types: true`` variable.

+ **Define allowed ssh key types**<br/>
  The allowed SSH Key Types are defined with this list. Some of them are commented out.<br/>
  Please not that by defualt only ``ed25519`` keys are allowed. Keep that in mind if you are using a rsa key.
```
  sshd__key_types:
  - 'ed25519'
  # - 'rsa'
  # - 'ecdsa'
  # - 'dsa' # (do not use!)
```

+ **Advanced SSH Algorithm Settings**<br/>
  You can define the used Key and Key Algorithm here to. For the default values and some examples for the variables ``sshd__key_algorithmus`` and ``sshd__kex_algorithmus`` have a look into ``defaults/main.yml``.


+ **force new SSH Features**<br/>
  If you know that you use a ssh version ``>8`` you can optionally define it with ``true/false`` with the ``sshd__version_is_above_eight`` variable.

 Files
-----

The main task of this role is to configure the ``sshd.conf`` file.


 References
----------

* [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)
