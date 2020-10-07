---
layout: post
title: Laravel 8.x new features
date: 2020-10-07 03:03 +0000
---


Laravel 8 released on September 8th, 2020, bug fixes until April 6th, 2021, and security fixes until September 8th, 2021. [^release]

[^release]: [8.x release note](https://laravel.com/docs/8.x/releases)


## Feature list

1. Laravel Jetstream
2. Models Directory
3. Model Factory Classes
4. Migration Squashing
5. Job Batching
6. Improved Rate Limiting
7. Improved Maintenance Mode
8. Closure Dispatch / Chain `catch`
9. Dynamic Blade Components
10. Event Listener Improvements
11. Time Testing Helpers
12. Artisan `serve` Improvements
13. Tailwind Pagination Views
14. Routing Namespace Updates


## Detail


### Laravel Jetstream

[Laravel Jetstream](https://jetstream.laravel.com/1.x/introduction.html) is a beautifully designed application scaffolding for Laravel. Jetstream provides the perfect starting point for your next project and includes login, registration, email verification, two-factor authentication, session management, API support via Laravel Sanctum, and optional team management. Laravel Jetstream replaces and improves upon the legacy authentication UI scaffolding available for previous versions of Laravel.

### Models Directory

By overwhelming community demand, the default Laravel application skeleton now contains an app/Models directory. We hope you enjoy this new home for your Eloquent models! All relevant generator commands have been updated to assume models exist within the `app/Models` directory if it exists. If the directory does not exist, the framework will assume your models should be placed within the app directory.

### Model Factory Classes

```php

<?php

namespace Database\Factories;

use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Str;

class UserFactory extends Factory
{
    /**
     * The name of the factory's corresponding model.
     *
     * @var string
     */
    protected $model = User::class;

    /**
     * Define the model's default state.
     *
     * @return array
     */
    public function definition()
    {
        return [
            'name' => $this->faker->name,
            'email' => $this->faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi', // password
            'remember_token' => Str::random(10),
        ];
    }
}

```

```php
use App\Models\User;

User::factory()->count(50)->create();
```



### Migration Squashing

```bash
php artisan schema:dump

// Dump the current database schema and prune all existing migrations...
php artisan schema:dump --prune

```

### Job Batching

```php
use App\Jobs\ProcessPodcast;
use App\Podcast;
use Illuminate\Bus\Batch;
use Illuminate\Support\Facades\Bus;
use Throwable;

$batch = Bus::batch([
    new ProcessPodcast(Podcast::find(1)),
    new ProcessPodcast(Podcast::find(2)),
    new ProcessPodcast(Podcast::find(3)),
    new ProcessPodcast(Podcast::find(4)),
    new ProcessPodcast(Podcast::find(5)),
])->then(function (Batch $batch) {
    // All jobs completed successfully...
})->catch(function (Batch $batch, Throwable $e) {
    // First batch job failure detected...
})->finally(function (Batch $batch) {
    // The batch has finished executing...
})->dispatch();

return $batch->id;
```


### Improved Rate Limiting

```php
use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Support\Facades\RateLimiter;

RateLimiter::for('global', function (Request $request) {
    return Limit::perMinute(1000);
});
```

```php
RateLimiter::for('uploads', function (Request $request) {
    return $request->user()->vipCustomer()
                ? Limit::none()
                : Limit::perMinute(100);
});
```


### Improved Maintenance Mode

```bash
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```

> https://example.com/1630542a-246b-4b66-afa1-dd72a4c43515

#### Pre-Rendering The Maintenance Mode View

```bash
php artisan down --render="errors::503"
```


### Closure Dispatch / Chain `catch`

```php
use Throwable;

dispatch(function () use ($podcast) {
    $podcast->publish();
})->catch(function (Throwable $e) {
    // This job has failed...
});
```


### Dynamic Blade Components

```html
<x-dynamic-component :component="$componentName" class="mt-4" />
```


### Event Listener Improvements

```php
use App\Events\PodcastProcessed;
use Illuminate\Support\Facades\Event;

Event::listen(function (PodcastProcessed $event) {
    //
});
```


```php

use App\Events\PodcastProcessed;
use function Illuminate\Events\queueable;
use Illuminate\Support\Facades\Event;

Event::listen(queueable(function (PodcastProcessed $event) {
    //
}));

```

```php
Event::listen(queueable(function (PodcastProcessed $event) {
    //
})->onConnection('redis')->onQueue('podcasts')->delay(now()->addSeconds(10)));
```

```php

use App\Events\PodcastProcessed;
use function Illuminate\Events\queueable;
use Illuminate\Support\Facades\Event;
use Throwable;

Event::listen(queueable(function (PodcastProcessed $event) {
    //
})->catch(function (PodcastProcessed $event, Throwable $e) {
    // The queued listener failed...
}));

```

### Time Testing Helpers

```php
public function testTimeCanBeManipulated()
{
    // Travel into the future...
    $this->travel(5)->milliseconds();
    $this->travel(5)->seconds();
    $this->travel(5)->minutes();
    $this->travel(5)->hours();
    $this->travel(5)->days();
    $this->travel(5)->weeks();
    $this->travel(5)->years();

    // Travel into the past...
    $this->travel(-5)->hours();

    // Travel to an explicit time...
    $this->travelTo(now()->subHours(6));

    // Return back to the present time...
    $this->travelBack();
}
```


### Artisan `serve` Improvements

The Artisan `serve` command has been improved with automatic reloading when environment variable changes are detected within your local `.env` file. Previously, the command had to be manually stopped and restarted.


### Tailwind Pagination Views

The Laravel paginator has been updated to use the Tailwind CSS framework by default. Tailwind CSS is a highly customizable, low-level CSS framework that gives you all of the building blocks you need to build bespoke designs without any annoying opinionated styles you have to fight to override. Of course, Bootstrap 3 and 4 views remain available as well.


### Routing Namespace Updates


```php
use App\Http\Controllers\UserController;

Route::get('/users', [UserController::class, 'index']);
```


```php
action([UserController::class, 'index']);

return Redirect::action([UserController::class, 'index']);
```