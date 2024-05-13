---
title: Postfix and LDAP
layout: post
tags: [server]
---
## Getting Postfix to talk to your LDAP server.


POSTFIX was already installed in a simple fashion using real Unix accounts. We will continue to use these Unix accounts but pass authentication duties off to an LDAP server.


I used the Centos Directory Server and it was necessary to install the (75misc.ldif schema in the server to allow for mail aliases and mailing lists).


**NOTE:** the file /etc/postix/master.cf did not require changes for this set-up.


___
/etc/postfix/main.cf:

~~~bash

queue_directory = /var/spool/postfix
command_directory = /usr/sbin
daemon_directory = /usr/libexec/postfix
mail_owner = postfix
myhostname = vm239.example.com
mydomain = example.com
myorigin = $mydomain
inet_interfaces = all

mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

unknown_local_recipient_reject_code = 550
mynetworks_style = subnet

mynetworks = 10.200.3.0/24, 127.0.0.0/8

alias_maps = hash:/etc/aliases
alias_database = $alias_maps
local_recipient_maps = ldap:/etc/postfix/ldap-users.cf
home_mailbox = Maildir/
virtual_alias_maps = ldap:/etc/postfix/ldap-aliases.cf
newaliases_path = /usr/bin/newaliases.postfix

virtual_mailbox_domains = virtual.com
virtual_mailbox_base = /var/spool/virt_mailboxes/
virtual_mailbox_maps = hash:/etc/postfix/vmailboxvirtual_mailbox_base = /var/spool/virt_mailboxes/
virtual_mailbox_maps = ldap:/etc/postfix/ldap-users.cf
virtual_minimum_uid = 100
virtual_uid_maps = static:500
virtual_gid_maps = static:500
virtual_alias_domains = virtual.com
virtual_alias_maps = hash:/etc/postfix/valias

~~~

___
**Virtual Users**


This was added to the bottom of the /etc/aliases file but otherwise it was left as installed (note: run the newaliases command after any changes are made to the aliases file).


*root: tedc*


/etc/postfix/ldap-users.cf


~~~bash
bind = no
version = 3
timeout = 20
size_limit = 1
expansion_limit = 0
start_tls = no
tls_require_cert = no
server_host = ldap://vm241.example.com/
scope = sub
search_base = ou=people,dc=example,dc=com
query_filter = (mail=%s)
result_attribute = uid
~~~


___
/etc/ldap-aliases.cf


~~~bash
bind = no
timeout = 20
server_host = ldap://vm241.example.com
search_base = ou=aliases,dc=example,dc=com
scope = sub
version = 3
query_filter = (cn=%s)
result_attribute = rfc822MailMember
~~~

