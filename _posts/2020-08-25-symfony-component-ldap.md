---
layout: post
title: Symfony component Ldap
date: 2020-08-25 05:37 +0000
---

* [The Ldap Component](https://symfony.com/doc/current/components/ldap)



```bash
use Symfony\Component\Ldap\Ldap;

$ldap = Ldap::create('ext_ldap', ['host' => '10.248.11.64', 'port' => '389']);

$ldap->bind('user@dn', 'password');

# fail
PHP Warning:  ldap_bind(): Unable to bind to server: Can't contact LDAP server in /var/www/vendor/symfony/ldap/Adapter/ExtLdap/Connection.php on line 60
Symfony/Component/Ldap/Exception/ConnectionException with message 'Can't contact LDAP server'

# success
null

```
