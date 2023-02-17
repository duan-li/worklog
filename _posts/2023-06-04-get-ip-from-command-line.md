---
layout: post
title: Get IP from command line
date: 2023-06-04 11:27 +0000
categories: [System]
tags: [command line, ip, network]
---

To retrieve the IP address from the command line, you can use the following methods based on your operating system:

## `dig` command

The `dig` command is a powerful tool used for querying DNS (Domain Name System) information. It is commonly used to retrieve information such as IP addresses, domain names, MX records, and more. The dig command is typically available on Unix-like operating systems, including Linux and macOS.

Here's the basic syntax for using the `dig` command:

```bash
dig [options] [domain]
```

Here are a example of how you can use the `dig` command to retreive your IP address: 

```bash
dig -4 TXT +short o-o.myaddr.l.google.com @ns1.google.com
```

## `curl` command

The `curl` command is a powerful tool used for making requests to servers and retrieving data from URLs. It is commonly used in command-line interfaces and scripting.

Here's the basic syntax of the `curl` command:

```css

curl [options] [URL]
```

To use `curl`, you need to provide a URL to specify the server you want to interact with. Additionally, you can include various options to customize the request and handle the response in different ways.

Here are a example of how you can use the `curl` command to retreive your IP address:

```bash
curl -s http://checkip.dyndns.org/ | sed 's/[a-zA-Z<>/ :]//g'
```

