---
layout: post
title: PHP self vs static
date: 2018-09-10 19:53 +0000
---

## `self`

```php
class Animal
{
  public static function model(){
    self::getModel();
  }

  protected static function getModel(){
    echo "This is a animal model";
  }
}

Animal::model();

Class Dog extends Animal
{
  protected static function getModel(){
    echo "This is a Dog model";
  }
}

Dog::model();
```

### Output
```
This is a animal model
This is a animal model
```

## `static`

```php
class Animal
{
  public static function model(){
    static::getModel();
  }

  protected static function getModel(){
    echo "This is a animal model";
  }
}

Animal::model();

Class Dog extends Animal
{
  protected static function getModel(){
    echo "This is a Dog model";
  }
}

Dog::model();
```

### Output
```
This is a animal model
This is a Dog model
```

https://segmentfault.com/a/1190000005060322


---
