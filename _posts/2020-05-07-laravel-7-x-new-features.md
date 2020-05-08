---
layout: post
title: Laravel 7.x new features
date: 2020-05-07 23:58 +0000
---

Laravel 7 released on March 3rd 2020, bug fixes until September 3rd 2020, and security fixes until March 3rd 2021 [^life]

1. Laravel Sanctum
1. Custom Eloquent Casts
1. 3. Blade Component Tags & Improvements
1. HTTP Client
1. Fluent String Operations
1. Route Model Binding Improvements
1. Multiple Mail Drivers
1. Route Caching Speed Improvements
1. CORS Support
1. Query Time Casts
1. MySQL 8+ Database Queue Improvements
1. Artisan test Command
1. Stub Customization
1. Queue maxExceptions Configuration
1. Markdown Mail Template Improvements




[^life]: [Laravel 7 Release Notes](https://laravel.com/docs/7.x/releases)


## Laravel Sanctum

Laravel Sanctum is a featherweight authentication system for SPAs[^SPAs]. Tt supports mobile application and simple, token based API. Each user of application will be allowed to generate multiple API tokens for their account. 



[^SPAs]: Single page applications


## Custom Eloquent Casts

### Eloquent cast class will be like. 

```php


namespace App\Casts;

use Illuminate\Contracts\Database\Eloquent\CastsAttributes;

class Json implements CastsAttributes
{
    /**
     * Cast the given value.
     *
     * @param  \Illuminate\Database\Eloquent\Model  $model
     * @param  string  $key
     * @param  mixed  $value
     * @param  array  $attributes
     * @return array
     */
    public function get($model, $key, $value, $attributes)
    {
        return json_decode($value, true);
    }

    /**
     * Prepare the given value for storage.
     *
     * @param  \Illuminate\Database\Eloquent\Model  $model
     * @param  string  $key
     * @param  array  $value
     * @param  array  $attributes
     * @return string
     */
    public function set($model, $key, $value, $attributes)
    {
        return json_encode($value);
    }
}
```

### In model

```php

namespace App;

use App\Casts\Json;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    /**
     * The attributes that should be cast to native types.
     *
     * @var array
     */
    protected $casts = [
        'options' => Json::class,
    ];
}

```



## Blade Component Tags & Improvements

Remember `@if` and `@endif`? Now you can do this. 


### Component class

```php

namespace App\View\Components;

use Illuminate\View\Component;

class Alert extends Component
{
    /**
     * The alert type.
     *
     * @var string
     */
    public $type;

    /**
     * Create the component instance.
     *
     * @param  string  $type
     * @return void
     */
    public function __construct($type)
    {
        $this->type = $type;
    }

    /**
     * Get the class for the given alert type.
     *
     * @return string
     */
    public function classForType()
    {
        return $this->type == 'danger' ? 'alert-danger' : 'alert-warning';
    }

    /**
     * Get the view / contents that represent the component.
     *
     * @return \Illuminate\View\View|string
     */
    public function render()
    {
        return view('components.alert');
    }
}
```

### Blade view template

```xml

<div class="alert {{ $classForType }}" {{ $attributes }}>
    {{ $heading }}

    {{ $slot }}
</div>

```


## HTTP Client

Laravel 7 provides a wrapper of Guzzle as **HTTP client**. It allows developer to quickly make outgoing HTTP requests to communicate with other web applications. 

```php

use Illuminate\Support\Facades\Http;

$response = Http::withHeaders([
    'X-First' => 'foo',
    'X-Second' => 'bar'
])->post('http://test.com/users', [
    'name' => 'Taylor',
]);

return $response['id'];

```

And also, Unit test can mock fake client in order to test. 

```php

Http::fake([
    // Stub a JSON response for GitHub endpoints...
    'github.com/*' => Http::response(['foo' => 'bar'], 200, ['Headers']),

    // Stub a string response for Google endpoints...
    'google.com/*' => Http::response('Hello World', 200, ['Headers']),

    // Stub a series of responses for Facebook endpoints...
    'facebook.com/*' => Http::sequence()
                            ->push('Hello World', 200)
                            ->push(['foo' => 'bar'], 200)
                            ->pushStatus(404),
]);


```

## Fluent String Operations


Creating a fluent `Illuminate\Support\Stringable` object using the `Str::of` method.

```php 
return (string) Str::of('  Laravel Framework 6.x ')
                    ->trim()
                    ->replace('6.x', '7.x')
                    ->slug();

```


## Route Model Binding Improvements

Laravel 7 provides more binding possibility when identify route.

### Key Customization

```php

Route::get('api/posts/{post:slug}', function (App\Post $post) {
    return $post;
});

```


### Automatic Scoping

```php
use App\Post;
use App\User;

Route::get('api/users/{user}/posts/{post:slug}', function (User $user, Post $post) {
    return $post;
});
```



## Multiple Mail Drivers

Laravel 7 allows single application to own multiple configuration of **mailers**. 

```php
Mail::mailer('postmark')
        ->to($request->user())
        ->send(new OrderShipped($order));


```

## Route Caching Speed Improvements

There is a **2x speed improvement** in requests per second on a simple "Hello World" benchmark.


## CORS Support

Cross-Origin Resource Sharing support. [^cors]

[^cors]: [Cross-Origin Resource Sharing](https://laravel.com/docs/7.x/routing#cors)


## Query Time Casts


```php
use App\Post;
use App\User;

$users = User::select([
    'users.*',
    'last_posted_at' => Post::selectRaw('MAX(created_at)')
            ->whereColumn('user_id', 'users.id')
])->get();

```


## MySQL 8+ Database Queue Improvements

For those applications using MYSQL 8+ as db backed queue, Laravel 7 is using the `FOR UPDATE SKIP LOCKED` clause and other SQL enhancements. 

## Artisan test Command

`php artisan test`



## Stub Customization

`php artisan stub:publish`




## Queue maxExceptions Configuration

```php

namespace App\Jobs;

class ProcessPodcast implements ShouldQueue
{
    /**
     * The number of times the job may be attempted.
     *
     * @var int
     */
    public $tries = 25;

    /**
     * The maximum number of exceptions to allow before failing.
     *
     * @var int
     */
    public $maxExceptions = 3;

    /**
     * Execute the job.
     *
     * @return void
     */
    public function handle()
    {
        Redis::throttle('key')->allow(10)->every(60)->then(function () {
            // Lock obtained, process the podcast...
        }, function () {
            // Unable to obtain lock...
            return $this->release(10);
        });
    }
}

```


## Markdown Mail Template Improvements


