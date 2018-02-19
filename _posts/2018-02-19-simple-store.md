---
layout: post
title: Simple Store
date: 2018-02-19 16:38:03 +1000
---

# Element
 * User
 * Product
 * Order Item
 * Order
 * Category
 * Tag

```mermaid
graph LR

A[User] --> B[Order]
B[Order] --> C[Order Item]
C[Order Item] --> D[Product]
D[Product] --> E[Tag]
D[Product] --> F[Category]

```