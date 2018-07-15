---
layout: post
title: ML Similarity Measurement
date: 2018-07-12 17:07 +0000
---


# Distance

## Euclidean Distance
{% katex display %}
d_{12} = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2}
{% endkatex %}

{% katex display %}
d_{12} = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2 + (z_1-z_2)^2}
{% endkatex %}


{% katex display %}
d_{12} = \sqrt{\sum_{k=1}^n(x_{1k} - x_{2k})^2}
{% endkatex %}


### Standardized Euclidean distance
{% katex display %}
X^* = \frac{X - m}{s}
{% endkatex %}



also Weighted Euclidean distance

## Manhattan Distance 
also called City Block distance
{% katex display %}
d_{12} = |x_1 - x_2| + |y_1 - y_2|
{% endkatex %}

{% katex display %}
d_{12} = \sum_{k=1}^n|x_{1k}-x_{2k}|
{% endkatex %}

## Chebyshev Distance

{% katex display %}
d_{12} = \max(|x_1 - x_2| , |y_1 - y_2|)
{% endkatex %}

{% katex display %}
d_{12} = \max_i(|x_{1i} - x_{2i}|)
{% endkatex %}


{% katex display %}
d_{12} = \lim_{k \rightarrow \infty}\bigg( \sum_{i=1}^n|x_{1i} - x_{2i}|^k \bigg)^{\frac{1}{k}}
{% endkatex %}


## Minkowski Distance
Minkowski Distance is not a distance, but a set definition of distance.

{% katex display %}
d_{12} = \sqrt[p]{\sum_{k=1}^n{|x_{1k} - x_{2k}}|^p}
{% endkatex %}

let's say `p` is var
* `p=1` city block distance
* `p=2` Euclidean Distance
* {% katex %} k \rightarrow \infty {% endkatex %}  Chebyshev Distance

## Mahalanobis Distance

## Hamming distance

# Cosine

# Jaccard similarity coefficient

# Correlation coefficient and Correlation distance

# Information Entropy





Ref 
* https://www.cnblogs.com/xbinworld/archive/2012/09/24/2700572.html
