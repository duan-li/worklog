---
layout: page
title: PHPUNIT
---
# Basic Usage

## Static
`assertCount`, `assertEquals`, `assertContains`, `assertNotContains`, `assertTrue`, `assertFalse`, `assertSame`, `assertNotSame`, `assertNull`, `assertNotNull`, `assertGreaterThan`, `assertRegExp`, `assertArrayHasKey`

## Response
`assertStatus`, `assertSuccessful`, `assertJsonStructure`, `assertJson`, `assertRedirect`, `assertViewHas`, `assertSee`, `assertDontSee`, `assertJsonFragment`, `assertSessionHas`, `assertSessionHasErrors`

## Database
`assertDatabaseHas`, `assertDatabaseMissing`

## Exception
`expectException`

## Event
`expectsEvents`

## Object
`assertInstanceOf`



# Laravel

## Validation
```php
$data = [
    'name' => 'Daniel'
];

$rule = [
    'name'  => 'required'
];

$v = $this->app['validator']->make(
        $data,
        $rule
    );

static::assertTrue($v->passes());

```
## Console Command
```php
$this->artisan('command', [
            'param1' => 'value1',
            '--param2' => 'value2',
        ]);
$output = Artisan::output();

static::assertContains('output wording', $output);
```
## Controller
Two ways to test controller
```php
$response = $this->get(action('Controller@edit', [$retailer->id]))
            ->assertSuccessful();
```

```php
$this->get(route("route.name"))
            ->assertSuccessful();
```


## Middleware
**Middleware class**
```php
namespace App\Http\Middleware;

use Closure;

class Sample
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request $request
     * @param  \Closure $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        return $next($request);
    }
}
```

**Test case**
```php
use App\Http\Middleware\Sample;
use Mockery;

class SampleMiTest extends \TestCase
{
    public function test_sample_middleware()
    {
        $response = $this->faker->md5;

        $request = Mockery::mock(\App\Http\Requests\Request::class);

        $request->shouldReceive('test')
            ->once()
            ->andReturn($response);

        $middleware = new Sample();

        $result = $middleware->handle($request, function ($r) {
            return $r->test();
        });

        $this->assertSame($response, $result);
    }
}
```


