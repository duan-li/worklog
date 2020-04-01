---
layout: post
title: Jupyter docker stacks
date: 2020-04-01 22:35 +0000
---

Repo: https://github.com/jupyter/docker-stacks


## Relationship

```mermaid
graph TB

R[R] -- from --> M[minimal]
T[tensorflow] -- from --> SC[Scipy]
A[all-spark]  -- from --> PY[Pysspark]
D[datascience] -- from --> SC[Scipy]
PY[Pysspark] -- from --> SC[Scipy]
M[minimal] -- from --> B[Base]
SC[Scipy] -- from --> M[minimal]

```

