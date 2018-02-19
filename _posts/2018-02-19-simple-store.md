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

User[Square Rect] --> Order[Square Rect]
Order[Square Rect] --> Order Item[Square Rect]
Order Item[Square Rect] --> Product[Square Rect]
Product[Square Rect] --> Tag[Square Rect]
Product[Square Rect] --> Category[Square Rect]

```