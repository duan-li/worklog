---
layout: post
title: Laravel test eloquent observer
date:   2018-02-12 15:06:03 +1000
---
# Eloquent observer

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
