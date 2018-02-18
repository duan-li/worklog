---
layout: post
title: apriori example
date: 2018-02-18 12:06:03 +1000
---
# Initial

```
$associator = new Phpml\Association\Apriori(0.5, 0.5);
```

# Training
```
$list ['apple', 'water', 'chips', 'beef'];

$purchaseList = [
	['apple', 'water', 'chips'], 
	['apple', 'water', 'beef'], 
	['apple', 'water', 'chips'], 
	['apple', 'water', 'beef']];

$labels  = [];

$associator->train($purchaseList, $labels);
```

# Prediction
```
$associator->predict(['apple','beef']); // water
$associator->predict(['apple','water']); // [chips, beef]]

$associator->predict([['apple','chips'],['water','beef']]);
```


# Associating
```
$associator->getRules();
```

# Frequent item sets
```
$associator->apriori();
```