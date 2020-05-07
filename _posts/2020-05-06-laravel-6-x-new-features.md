---
layout: post
title: Laravel 6.x new features
date: 2020-05-06 23:50 +0000
---

1. Laravel 6 is LTS, release at September 3rd, 2019, Bug Fixes Unti September 3rd, 2021 and Security Fixes Until September 3rd, 2022.
1. Semantic Versioning
2. The extraction of frontend Laravel/UI
3. Improved authorization responses:
4. Lazy Collections
5. Job Middleware and Laravel Spark
5. Eloquent Subquery Enhancements
6. Improved Exceptions Via Ignition
7. Laravel Vapor Compatibility

##Semantic Versioning

Semantic versioning is just like a set of rules and instructions that elaborate on the typical changes that rises the number of versions or possible each of the three numbers representing the version. [^l]

[^l]: [Difference between Laravel 6.0 and It’s previous versions](https://medium.com/@samwatsonets/difference-between-laravel-6-0-and-its-previous-versions-efb2829d0f55)

##The extraction of frontend Laravel/UI

[Laravel UI](https://github.com/laravel/ui) is an authorized package of Laravel 6.0 that includes the extracted UI parts from a Laravel project.

```php

composer require laravel/ui "^1.0" --dev

php artisan ui vue --auth

```

##Improved authorization responses:

In Laravel 6, this is now much easier using authorization response messages and the new `Gate::inspect` method. [^official]

[^official]: [Laravel 6 Release Notes](https://laravel.com/docs/6.x/releases)

### Before

```php
/**
 * Determine if the user can view the given flight.
 *
 * @param  \App\User  $user
 * @param  \App\Flight  $flight
 * @return mixed
 */
public function view(User $user, Flight $flight)
{
    return $this->deny('Explanation of denial.');
}
```

### After

```php
$response = Gate::inspect('view', $flight);

if ($response->allowed()) {
    // User is authorized to view the flight...
}

if ($response->denied()) {
    echo $response->message();
}

```

##Lazy Collections

```php
use App\LogEntry;
use Illuminate\Support\LazyCollection;

LazyCollection::make(function () {
    $handle = fopen('log.txt', 'r');

    while (($line = fgets($handle)) !== false) {
        yield $line;
    }
})
->chunk(4)
->map(function ($lines) {
    return LogEntry::fromLines($lines);
})
->each(function (LogEntry $logEntry) {
    // Process the log entry...
});
```

##Job Middleware and Laravel Spark

```php

namespace App\Jobs\Middleware;

use Illuminate\Support\Facades\Redis;

class RateLimited
{
    /**
     * Process the queued job.
     *
     * @param  mixed  $job
     * @param  callable  $next
     * @return mixed
     */
    public function handle($job, $next)
    {
        Redis::throttle('key')
                ->block(0)->allow(1)->every(5)
                ->then(function () use ($job, $next) {
                    // Lock obtained...

                    $next($job);
                }, function () use ($job) {
                    // Could not obtain lock...

                    $job->release(5);
                });
    }
}

```

## Eloquent Subquery Enhancements

```php
return Destination::addSelect(['last_flight' => Flight::select('name')
    ->whereColumn('destination_id', 'destinations.id')
    ->orderBy('arrived_at', 'desc')
    ->limit(1)
])->get();
```


```php

return Destination::orderByDesc(
    Flight::select('arrived_at')
        ->whereColumn('destination_id', 'destinations.id')
        ->orderBy('arrived_at', 'desc')
        ->limit(1)
)->get();

```
