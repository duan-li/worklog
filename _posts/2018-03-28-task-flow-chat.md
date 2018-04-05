---
layout: post
title: Task flow chat
date: 2018-03-28 12:07 +1100
---

```mermaid
graph TB

A[Relate code/Base code] --> B((How it work))
A[Relate code/Base code] --> D[Task aim]
A[Relate code/Base code] --> C((What result))
D[Task aim] --> E((Waht result need))
D[Task aim] --> F[Tool/Function]
D[Task aim] --> L((Waht result before))
F[Tool/Function] --> G((How to use it))
F[Tool/Function] --> J[Test it]
F[Tool/Function] --> H((How it work/any other example))
J[Test it] --> K((Test case))
J[Test it] --> N[Decition Made]
J[Test it] --> M((See real result))
N[Decition Made] --> O((Document Why))
N[Decition Made] --> P((Document what))
```