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
`expectsEvents`, `expectsJobs`

## Object
`assertInstanceOf`

# Date time

```php
Carbon::setTestNow(Carbon::create(2018, 6, 21, 11, 39, 04));
```

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
This way can check output.
```php
$this->artisan('command', [
            'param1' => 'value1',
            '--param2' => 'value2',
        ]);
$output = Artisan::output();

static::assertContains('output wording', $output);
```

### Command tester
This way can use debug and output.
```php
$command = new \App\Console\Commands\CommandClass();
$command->setLaravel($this->app);

$tester = new \Symfony\Component\Console\Tester\CommandTester($command);
$tester->execute([
            'param1' => 'value1',
            '--param2' => 'value2',
        ]);
$output = $tester->getDisplay();
self::assertContains('Wording that expected.', $output);
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

## Model
**Code**
```php
$productProvider = new Product;

$product = $productProvider->where('id', 1)->first();
 
$product->name = 'name';

$productNumber = $product->number;

$product->save();

```
**Test**

```php

$model = \Mockery::mock(Product::class);

$model->shouldReceive('where')
    ->once()
    ->andReturnSelf();

$model->->shouldReceive('first')
    ->once()
    ->andReturnSelf();

$model->shouldReceive('setAttribute')
    ->once();

$model->shouldReceive('getAttribute')
    ->with('number')
    ->andReturn($this->faker->numberBetween(1,10));

$model->shouldReceive('save')
    ->once();    

```


## Abstract Class
**Abstract Class**
```php
abstract class AbstractClass
{
    public function method()
    {
        return $this->property;
    }
}
```

**Test case**
```php
class SampleMiTest extends \TestCase
{
    private function getSubclass($property)
    {
        $subclass = new class($property) extends AbstractClass
        {
            protected $property;

            public function __construct($property)
            {
                $this->property = $property;
            }
        };

        return $subclass;
    }

    public function testMethod()
    {
        $property = 'string';

        $sub = $this->getSubclass($property);

        static::assertSame($property, $sub->getMethod());
    }
}
```

## Request
**Test Code**
```php
// Create request and set attribute
use Illuminate\Http\Request;

$request = new Request;
$request->attribute = 'value';

// Mockery request
$request = Mockery::mock(\Illuminate\Http\Request::class);
$request->shouldReceive('hasSession')
    ->andReturn(true)
    ->shouldReceive('getSession')
    ->andReturn(md5(''))
    ->shouldReceive('get')
    ->andReturn('test')
    ->shouldReceive('has')
    ->andReturn(false)
    ;

// Mockery request with upload file

$expected = [
    'path' => sprintf('csv-storage://%s/%s', $this->getUploadPath(), __FILE__),
    'size' => 0,
    'mimeType' => $csv ? 'text/csv' : 'application/pdf'
]

$uploadedFile = Mockery::mock(\Illuminate\Http\UploadedFile::class);
$uploadedFile
    ->shouldReceive('hashName')
    ->andReturn(__FILE__)
    ->shouldReceive('getMimeType')
    ->andReturn($expected['mimeType'])
    ->shouldReceive('getSize')
    ->andReturn($expected['size']);

$request = Mockery::mock(\Illuminate\Http\Request::class);
$request->shouldReceive('hasFile')
->andReturn(true)
->shouldReceive('file')
->andReturn($inputFile);


// MOckery request with getting file
$file = new \stdClass();
$file->name = 'name';
$file->uuid = 'uuid';
$file->mimeType = 'mimeType';
$file->size = 100;
$file->isImage = $image;

if ($image) {
    $file->originalImageInfo = new \stdClass();
    $file->originalImageInfo->height = 100;
    $file->originalImageInfo->width = 100;
}

$requestFile = json_encode($file);
$request = Mockery::mock(Request::class);
$request->shouldReceive('get')->andReturn($requestFile);



```


## app() helper

**test code**
```php

$this->app->bind(ClassName::class, function () {
    return Mockery::mock()
            ->shouldReceive('setMethod')->with('x')->once()
            ->shouldReceive('getMethod')->once()->andReturn('y')
            ->getMock();
});

```