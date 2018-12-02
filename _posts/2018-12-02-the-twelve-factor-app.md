---
layout: post
title: The Twelve-Factor App
date: 2018-12-02 23:30 +0000
---

> In the modern era, software is commonly delivered as a service: called _web apps_, or _software-as-a-service_.

The twelve-factor app is a methodology for building software-as-a-service apps that: [^1]
1. **Codebase**: One codebase tracked in revision control, many deploys
2. **Dependencies**: Explicitly declare and isolate dependencies
3. **Config**: Store config in the environment
4. **Backing services**: Treat backing services as attached resources
5. **Build, release, run**: Strictly separate build and run stages
6. **Processes**: Execute the app as one or more stateless processes
7. **Port binding**: Export services via port binding
8. **Concurrency**: Scale out via the process model
9. **Disposability**: Maximize robustness with fast startup and graceful shutdown
10. **Dev/prod parity**: Keep development, staging, and production as similar as possible
11. **Logs**: Treat logs as event streams
12. **Admin processes**: Run admin/management tasks as one-off processes
13.

[^1]: [The Twelve-Factor App](https://www.12factor.net/)

--- 