---
layout: post
title: Laravel Design Patterns
date: 2020-02-24 21:55 +0000
---


## Design patterns in Laravel [^ppt]

[^ppt]: [Laravel Design Patterns](https://www.slideshare.net/BobbyBouwmann/laravel-design-patterns-86729254)

- Factory Pattern
- Builder (Manager) Pattern
- Strategy Pattern
- Provider Pattern
- Repository Pattern
- Iterator Pattern
- Singleton Pattern
- Presenter Pattern
- Factory Pattern
- Builder (Manager) Pattern
- Strategy Pattern
- Provider Pattern


## Difference between Builder Design pattern and Factory Design pattern?

> Dependency Injection Container -> Service Locator -> Builder -> Factory [^ans]

[^ans]: [Creational Patterns](https://stackoverflow.com/a/47122130)

Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.
Builder often builds a Composite. [^ans2]

[^ans2]: [What's difference](https://stackoverflow.com/questions/757743/what-is-the-difference-between-builder-design-pattern-and-factory-design-pattern/47122130#47122130)

Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.

Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components get built. Abstract Factory, Builder, and Prototype can use Singleton in their implementations.
