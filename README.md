[![Ansible Galaxy](https://raw.githubusercontent.com/roles-ansible/ansible_role_sshd/main/.github/galaxy.svg?sanitize=true)](https://galaxy.ansible.com/do1jlr/sshd) [![MIT License](https://raw.githubusercontent.com/roles-ansible/ansible_role_sshd/main/.github/license.svg?sanitize=true)](https://github.com/roles-ansible/ansible_role_sshd/blob/main/LICENSE)

OpenSSH Server
==============

Ansible role to configure the OpenSSH Server ``SSHD``.
The main goal of this role is to manage the sshd.conf file. And some additional parts like deploying the defined ssh host keys at the configured path.

 Pro Tipp
----------------
Use Eliptic cureve cryptografie for your ssh keys:
```bash
ssh-keygen -t ed25519
```
*The default values of this role will only allow ed25519 keys. But you can change that obviously if you like.*

 intended use
---------------
This role is designed to manage linux hosts with the following roles. This role here basically only focuses on a good configuration of sshd and can define which users are allowd to use connect via ssh and which ssh key types are allowd.
Other roles distribute ssh public keys, creating users and configure sudo permission, roll out dotfiles or install a number of useful packages.

A list of suggested roles to manage your linux host:
 - [do1jlr.base](https://github.com/roles-ansible/ansible_role_base.git) *install some useful packages*
 - [do1jlr.users](https://github.com/roles-ansible/ansible_role_users.git) *create user and manage sudoers*
 - [do1jlr.auth](https://github.com/chaos-bodensee/role-ssh_authorized_keys.git) *deploy ssh pubkeys*
 - [do1jlr.sshd](https://github.com/roles-ansible/ansible_role_sshd.git) *(this one)*
 - [do1jlr.dotfiles](https://github.com/roles-ansible/ansible_role_dotfiles) *deploy some fancy dotfiles*

 Good to know:
---------------
The listed roles use the same variables to create accounts, admins and so on. But the roles have to run in the correct order to work properly.
For example you can't deploy a ssh public key for a user that is not created.

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
  You can define the used Key and Kex Algorithm here to. For the default values and some examples for the variables ``sshd__key_algorithmus`` and ``sshd__kex_algorithmus`` have a look into ``defaults/main.yml``.
  You can disable it by setting ``sshd__manage_key_algorithmus`` and ``sshd__manage_kex_algorithmus`` to ``false``.


+ **force new SSH Features**<br/>
  If you know that you use a ssh version ``>8`` you can optionally define it with ``true/false`` with the ``sshd__version_is_above_eight`` variable.

 Files
-----

The main task of this role is to configure the ``sshd.conf`` file.


 References
----------

* [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)

 Testing
--------
This role is tested with some linting tests. Sadly I don't know how to run this role in a docker container because systemd is involved... If you have ideas how to improve testing please dend me a message, open a issue or Pull Request.
If you want to find out more about our tests, please have a look at the github marketplace.

| test status | Github Marketplace |
| :---------  | :----------------  |
| [![Galaxy release](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/galaxy.yml/badge.svg)](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/galaxy.yml) | [publish-ansible-role-to-galaxy](https://github.com/marketplace/actions/publish-ansible-role-to-galaxy) |
| [![Yamllint GitHub Actions](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/yamllint.yaml/badge.svg)](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/yamllint.yaml) | [yamllint-github-action](https://github.com/marketplace/actions/yamllint-github-action) |
| [![Ansible Lint check](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/ansible-linting-check.yml/badge.svg)](https://github.com/roles-ansible/ansible_role_sshd/actions/workflows/ansible-linting-check.yml) | [ansible-lint action](https://github.com/marketplace/actions/ansible-lint)
