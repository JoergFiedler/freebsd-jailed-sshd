freebsd-jailed-sshd
=========

[![Build Status](https://travis-ci.org/JoergFiedler/freebsd-jailed-sshd.svg?branch=master)](https://travis-ci.org/JoergFiedler/freebsd-jailed-sshd)

This role provides a jailed sshd server. Nothing more.

All incoming ssh connection will be redirected to this jail and if the user is allowed to login again forwarded to the hosts internal ssh server (needs proxy command to be set up - see `Vagrantfile` within this project for example).  

Requirements
------------

This role is intent to be used with a fresh FreeBSD 11.2 installation. There is a Vagrant Box with providers for VirtualBox and EC2 you may use.

Role Variables
--------------

##### sshd_authorized_keys_file

The public key used for user authentication. Will be added to `authorized_key` file of the user (host/jail). Defaults to vagrants insecure public key.

##### sshd_jump_host

Set to `yes` if this jail is used as jump host for the host system. Default: `no`.
 
##### sshd_port

The port the sshd server should listen on. Default: `22`.

##### sshd_user

The user name used to connect via ssh. Default: `'vagrant'`.

##### sshd_gid

The group id the ssh user should belong to. Default: `1001`.

##### sshd_user_home

The ssh user's home directory. Default: `/home/{{ sshd_user }}`.

##### sshd_user_shell

The default shell for the ssh user. Default: `/bin/sh`.

##### sshd_user_uid

The id for the ssh user. Default: `1001`.

Dependencies
------------

- [JoergFiedler.freebsd-jailed](https://galaxy.ansible.com/joergfiedler/freebsd-jailed)

Example Playbook
----------------

    - hosts: all
      become: true
    
      vars:
        ansible_python_interpreter: '/usr/local/bin/python2.7'
    
      tasks:
        - import_role:
            name: 'JoergFiedler.freebsd-jail-host'
        - include_role:
            name: 'JoergFiedler.freebsd-jailed-sshd'
          vars:
            jail_net_ip: '10.1.0.10'
            jail_name: 'sshd'
            jail_freebsd_release: '11.2-RELEASE'
            sshd_jump_host: true

License
-------

BSD

Author Information
------------------

Any ideas to improve this project, please open an issue on Github. Thanks.
