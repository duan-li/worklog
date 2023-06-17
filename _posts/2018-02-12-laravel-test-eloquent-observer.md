---
layout: post
title: Laravel test eloquent observer
date:   2018-02-12 15:06:03 +1000
categories: [Code]
tags: [design pattern, observer]
---

## Observer design pattern

The Observer design pattern is a behavioral design pattern that allows an object, called the subject, to notify other objects, known as observers, about changes in its state. This is particularly useful when there is a one-to-many dependency between objects, such as if one object should automatically notify others when it changes state.

The main idea behind this pattern is that the subject is the only one who knows about all its observers, while the observers only know about the subject, not about each other. This means the observers can keep their states in sync with the subject's state without needing to know about each other.

### Participants

1. *Subject*: The object being observed. It maintains a list of observers and provides methods to add, remove, and notify them.

2. *Observer*: The objects that are observing the Subject. They provide a method (usually called something like 'update') that gets called when the Subject's state changes.

3. *Concrete Subject*: A specific, concrete implementation of the Subject. It stores the state of interest to Concrete Observers and sends a notification to its Observers when its state changes.

4. *Concrete Observer*: A specific, concrete implementation of the Observer. It maintains a reference to a Concrete Subject object, stores state that should stay consistent with the Subject's, and implements the Observer updating interface to keep its state consistent with the Subject's.

### PHP Example

```php
interface Observer {
    public function update($subject);
}

interface Subject {
    public function attach($observer);
    public function detach($observer);
    public function notify();
}

class ConcreteSubject implements Subject {
    private $observers = array();
    private $state;

    public function getState() {
        return $this->state;
    }

    public function setState($state) {
        $this->state = $state;
        $this->notify();
    }

    public function attach($observer) {
        array_push($this->observers, $observer);
    }

    public function detach($observer) {
        $index = array_search($observer, $this->observers);
        if ($index !== FALSE) {
            unset($this->observers[$index]);
        }
    }

    public function notify() {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }
}

class ConcreteObserver1 implements Observer {
    public function update($subject) {
        if ($subject->getState() < 3) {
            echo "ConcreteObserver1: Reacted to the event.\n";
        }
    }
}

class ConcreteObserver2 implements Observer {
    public function update($subject) {
        if ($subject->getState() == 0 || $subject->getState() >= 2) {
            echo "ConcreteObserver2: Reacted to the event.\n";
        }
    }
}
```

```php
// The client code.
$subject = new ConcreteSubject;
$observer1 = new ConcreteObserver1;
$subject->attach($observer1);

$observer2 = new ConcreteObserver2;
$subject->attach($observer2);

$subject->setState(1);
$subject->setState(2);
$subject->setState(3);

$subject->detach($observer2);

$subject->setState(0);
```

This PHP example is a bit more complex than the Python one, but it illustrates the same principles. We have `Subject` and `Observer` interfaces, and `ConcreteSubject` and `ConcreteObserver` classes.

The `ConcreteSubject` class contains an array of observers and methods for adding, removing, and notifying observers. It also has a `state` property, with a `setState` method that changes the state and then notifies all observers of the change.

The `ConcreteObserver` classes implement the `update` method of the `Observer` interface, which is called when the `Subject`'s state changes.

The client code creates a `ConcreteSubject`, two `ConcreteObservers`, and attaches the observers to the subject. It then changes the state of the `subject` a few times to show the observers reacting to the changes.

## Laravel Eloquent observer

In Laravel, the Eloquent ORM (Object-Relational Mapping) provides an easy and convenient way to interact with your database using PHP objects. Eloquent also includes a feature called Observers, which can be seen as an implementation of the Observer pattern.

Eloquent Observers allow you to create methods that will be executed when certain events occur on an Eloquent model. These events include "retrieved", "creating", "created", "updating", "updated", "saving", "saved", "deleting", "deleted", "restoring", "restored", and "forceDeleted". By creating Observers, you can define actions that happen every time one of these events occur for a specific model.



```php
class UserObserver implements ShouldQueue
{
    public function updated(User $user)
    {
    	// logic
    }

    public function deleted(User $user)
    {
    	// logic
    }
}
```
# Test case

```php
public function test_observer_user_updated()
{
    $user = new User();
    $userObserver = \Mockery::mock(UserObserver::class);
    $userObserver->shouldReceive('updated')->once();
    \App::instance(UserObserver::class, $userObserver);

    $user->name = "new name";
    $user->save();
}

public function test_observer_user_deleted()
{
    $user = new User();
    $userObserver = \Mockery::mock(UserObserver::class);
    $userObserver->shouldReceive('deleted')->once();
    \App::instance(UserObserver::class, $userObserver);

    $user->delete();
}

```

## Summary 

Eloquent Observers are a powerful tool that allow you to keep your code clean and organized by separating concerns, and they provide a central place where you can handle model-related events.
