---
layout: post
title: Logging to syslog in Python
date: 2020-02-05 23:44 +0000
---


```python
import logging
import logging.handlers

my_logger = logging.getLogger('MyLogger')
my_logger.setLevel(logging.DEBUG)

handler = logging.handlers.SysLogHandler(address = '/dev/log')
# handler = logging.handlers.SysLogHandler(address = ('127.0.0.1',514))

my_logger.addHandler(handler)

my_logger.debug('this is debug')
my_logger.critical('this is critical')
my_logger.info('this is info')

```


* https://stackoverflow.com/questions/38907637/quick-remote-logging-system
* https://stackoverflow.com/questions/3968669/how-to-configure-logging-to-syslog-in-python

