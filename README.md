xmppdav
=======

An Ansible playbook to configure the Prosody XMPP and Radicale CardDAV/CalDAV servers to use a PostgreSQL authentication backend. This has only been tested against Debian 8.

Usage
=====

Install Ansible and configure an xmppdav group in /etc/ansible/hosts with one host. Configure an xmppdav:vars section for group variables. cert\_\* variables are only required if you don't specify an existing certificate. If there is no existing certificate a self-signed one will be generated. Your Ansible inventory file should look as follows:

```
[xmppdav]
myserver01 ansible_ssh_host=192.168.1.1

[xmppdav:vars]
db_password_prosody=password123
db_password_radicale=password456
xmpp_domain=example.com
xmpp_certificate=/etc/prosody/certs/example.com.crt
xmpp_key=/etc/prosody/certs/example.com.key
cert_country=US
cert_state=New York
cert_city=New York
cert_ou=IT
```

Run the playbook with `ansible-playbook xmppdav.yml -K` and enter your sudo password for the remote host.

usermgmt.sh
===========

This is a crude script to manage users in the PostgreSQL database. The playbook copies it to /root/usermgmt.sh on the remote host. Use it as follows:

```
usermgmt.sh list [USER]|add USER|delete USER|change USER
```
