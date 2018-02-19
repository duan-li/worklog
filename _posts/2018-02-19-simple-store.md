---
layout: post
title: Simple Store
date: 2018-02-19 16:38:03 +1000
---

# Element
 * User
   * id
   * name
   * email
   * password
   * timestamp
 * Product
 	* id
 	* name
 	* price
 	* timestamp
 * Order
 	* id
 	* user_id
 	* amount
 	* timestamp
 * Order Item
 	* id
 	* order_id
 	* product_id
 	* name
 	* qty
 	* price
 	* subtotal
 	* timestamp
 * Category
 	* id
 	* name
 	* timestamp
 * Tag
 	* id
 	* name
 	* timestamp
 * Review
 	* id
 	* user_id
 	* type
 	* entity_id
 	* content


```mermaid
graph LR

A[User] -- one2many --> B[Order]
B[Order] -- one2many --> C[Order Item]
C[Order Item] -- one2one --> D[Product]
```


```mermaid
graph LR

D[Product] -- many2many --> E[Tag]
D[Product] -- many2many --> F[Category]
```

```mermaid
graph LR
R[Review] -- one2one --> P[Product]
R[Review] -- one2one --> O[Order]
R[Review] -- one2one --> I[Order Item]
```

