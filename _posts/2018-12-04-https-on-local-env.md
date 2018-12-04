---
layout: post
title: HTTPS on local env
date: 2018-12-04 04:09 +0000
---

Using OpenSSL to generate all of our certificates.[^1]
[^1]: [How to get HTTPS working on your local development environment in 5 minutes](https://medium.freecodecamp.org/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)

## Root SSL certificate
```bash
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
```

## Trust the root SSL certificate
Import root ssl into you system, include windows, Mac os and linux

## Domain SSL certificate

```bash
openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config <( cat server.csr.cnf )

openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile v3.ext

```
And put two file before run above commands [^2]

[^2]: [dakshshah96/local-cert-generator](https://github.com/dakshshah96/local-cert-generator/blob/master/server.csr.cnf)

### File `server.csr.cnf`
```bash
[req]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn

[dn]
C=US
ST=RandomState
L=RandomCity
O=RandomOrganization
OU=RandomOrganizationUnit
emailAddress=hello@example.com
CN = <domain name>
```

### File `v3.ext`

```bash
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
```




---