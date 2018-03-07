OpenSSH Server
==============

Ansible role to configure the OpenSSH `ssh` server.


Variables
---------

* `sshd_allow_users` (default `[root]`):
  List of users for the `AllowUsers` keyword

* `sshd_allow_groups` (default `[root]`):
  List of groups for the `AllowGroups` keyword


References
----------

* [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)
