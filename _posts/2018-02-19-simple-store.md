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

A[User] -- one2many --> B[Order]
B[Order] -- one2many --> C[Order Item]
C[Order Item] -- one2one --> D[Product]
D[Product] -- many2many --> E[Tag]
D[Product] -- many2many --> F[Category]

```