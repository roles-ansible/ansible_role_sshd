OpenSSH Server
==============

Ansible role to configure the OpenSSH `ssh` server.
Use Eliptic cureve cryptografie for your ssh keys e.g.:
```bash
ssh-keygen -t ed25519
```


Variables
---------

* `restrict_allow_users`: enable the `AllowUsers` and `AllowGroups` options.

+ `users`: which user is allowed to login. 

Example config:
```bash
users:
  l3d:
    - l3d
  ottojo:
   - ottojo@uni
   - ottojo@home
```

Files
-----

* `sshd.conf`:


References
----------

* [Secure Secure Shell](https://stribika.github.io/2015/01/04/secure-secure-shell.html)
