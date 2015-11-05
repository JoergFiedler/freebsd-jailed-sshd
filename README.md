freebsd-jailed-sshd
=========

This role provides a jailed sshd server. Nothing more.

All incoming ssh connection will be redirected to this jail and if the user is allowed to login again forwarded to the hosts internal ssh server.

To see this role in action, have a look at [this project of mine](https://github.com/JoergFiedler/freebsd-ansible-demo).

Requirements
------------

This role is intent to be used with a fresh FreeBSD 10.2 installation. There is a Vagrant Box with providers for VirtualBox and EC2 you may use.

You will find a sample project which uses this role [here](https://github.com/JoergFiedler/freebsd-ansible-demo).

Role Variables
--------------

##### jail_name

The jail's name. Default: `'{{ jail_net_ip }}'`.

##### jail_domain

The domain the jail belongs to. Domain part of the hostname. Default: `'darkcity'`.

##### jail_net_ip

The jail's ip address. No default, a value must be set.

##### jail_net_if

The interface to which the jail's ip address is added. Default: `'lo0'`

##### host_ioc_jails_dir

The directory iocage creates jails in. Default: `'/iocage/jails'`.

##### host_sshd_user

The user name used to connect via ssh. Default: `'vagrant'`.

##### host_sshd_pubkey

The public key used for user authentication. Will be added to `authorized_key` file of the user (host/jail). Defaults to vagrants insecure public key.

##### host_sshd_port

The port the sshd server should listen on. Default: `22`.

##### host_net_int_ip

The jail's host internal ip address. Default: `'10.1.0.1'`.

##### host_net_ext_ip

The jail's host external ip address. Default: `'10.0.2.15'`.

##### host_net_ext_if

The jail's host external interface. Default: `'vtnet0'`.

##### syslogd_server

The syslogd server to which all syslog messages are going to be forwarded. No default value.

This feature is only active if the variable `use_syslogd_server` is set to any value.

##### ssmtp_forward_address

System mails are forwarded to this address. See [ssmtp man page](https://www.freebsd.org/cgi/man.cgi?query=ssmtp&apropos=0&sektion=0&manpath=FreeBSD+10.2-RELEASE+and+Ports&arch=default&format=html) for further information.

Default: 'freebsd-ansible-demo@maildrop.cc'.

This feature is only active, if the variable `use_ssmtp` is set to any value.

##### ssmtp_forward_mailhub

System mails are forwarded using this mail relay. See [ssmtp man page](https://www.freebsd.org/cgi/man.cgi?query=ssmtp&apropos=0&sektion=0&manpath=FreeBSD+10.2-RELEASE+and+Ports&arch=default&format=html) for further information.

Default: 'mail.maildrop.cc'.

This feature is only active, if the variable `use_ssmtp` is set to any value.

Dependencies
------------

- [JoergFiedler.freebsd-jail-host](https://galaxy.ansible.com/detail#/role/5827)

Example Playbook
----------------

    - { role: JoergFiedler.freebsd-jailed-sshd,
        tags: ['sshd'],
        jail_name: 'sshd',
        jail_net_ip: '10.1.0.2' }

License
-------

BSD

Author Information
------------------

Any ideas to improve this project, please open an issue on Github. Thanks.
