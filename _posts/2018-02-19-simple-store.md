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
Square Rect[Product] --> E[Tag]
Square Rect[Product] --> F[Category]

```