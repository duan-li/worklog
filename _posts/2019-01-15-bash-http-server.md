---
layout: post
title: Bash HTTP server
date: 2019-01-15 00:56 +0000
---

5 lines code make a HTTP server [^1]

[^1]: [benrady/shinatra](https://github.com/benrady/shinatra/blob/master/shinatra.sh)

```bash
#!/usr/bin/env bash
RESPONSE="HTTP/1.1 200 OK\r\nConnection: keep-alive\r\n\r\n${2:-"OK"}\r\n"
while { echo -en "$RESPONSE"; } | nc -l "${1:-8080}"; do
  echo "================================================"
done
```

also like

```bash
RESPONSE="HTTP/1.1 200 OK\r\nConnection: keep-alive\r\n\r\n${2:-"conned"}\r\n"
while true ; do 
	echo -en "$RESPONSE" | nc -l "${1:-8111}";
done
```

Other one [avleen/bashttpd](https://github.com/avleen/bashttpd), it is using `netcat` [^2] .

[^2]: [minimal-web-server-using-netcat](https://stackoverflow.com/questions/16640054/minimal-web-server-using-netcat)

---