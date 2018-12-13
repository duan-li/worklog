---
layout: post
title: Use laravel view(blade) as a package
date: 2018-11-27 22:00 +0000
---


## Three blade packages
* Laravel-Blade [Source code](https://github.com/PhiloNL/Laravel-Blade/blob/master/src/Blade.php) [Documents](https://github.com/PhiloNL/Laravel-Blade) 
* laraport/blade [Source code](https://github.com/laraport/blade/blob/master/src/Blade.php) [Documents](https://github.com/laraport/blade) 
* jenssegers/blade [Source code](https://github.com/jenssegers/blade/blob/master/src/Blade.php) [Documents](https://github.com/jenssegers/blade) 


## `view()` helper

```php
return view('welcome');
```
In `helpers.php` of `illuminate/fundation`

```php
if (! function_exists('view')) {
    /**
     * Get the evaluated view contents for the given view.
     *
     * @param  string  $view
     * @param  array   $data
     * @param  array   $mergeData
     * @return \Illuminate\View\View|\Illuminate\Contracts\View\Factory
     */
    function view($view = null, $data = [], $mergeData = [])
    {
        $factory = app(ViewFactory::class);

        if (func_num_args() === 0) {
            return $factory;
        }

        return $factory->make($view, $data, $mergeData);
    }
}
```
`ViewFactory` is `Illuminate\Contracts\View\Factory`

## `Factory` as `ViewFactory`
In `ViewServiceProvider`, to make a `ViewFactory` need.
- Resolver
- Finder: filesystem 
- events: 


## Blade driver
```php
<?php
/**
 * Created by PhpStorm.
 * User: duan.li
 * Date: 13/12/18
 * Time: 12:50 PM
 */

namespace Library\ViewDriver;

use Illuminate\Container\Container;
use Illuminate\Contracts\Container\Container as ContainerInterface;
use Illuminate\Events\Dispatcher;
use Illuminate\Filesystem\Filesystem;
use Illuminate\View\Engines\EngineResolver;
use Illuminate\View\FileViewFinder;
use Illuminate\View\ViewServiceProvider;

class BladeDriver
{
    /**
     * Container instance.
     *
     * @var Container
     */
    protected $container;
    /**
     * Engine Resolver
     *
     * @var
     */
    protected $engineResolver;
    /**
     * Constructor.
     *
     * @param string|array       $viewPaths
     * @param string             $cachePath
     * @param ContainerInterface $container
     */
    public function __construct($viewPaths, $cachePath, ContainerInterface $container = null)
    {
        $this->viewPaths = $viewPaths;
        $this->cachePath = $cachePath;
        $this->container = $container ?: new Container;
        $this->setupContainer();
        $provider = new ViewServiceProvider($this->container);
        $provider->registerFactory();
        $this->registerViewFinder();
        $provider->registerEngineResolver();
        $this->engineResolver = $this->container->make('view.engine.resolver');
    }
    /**
     * Bind required instances for the service provider.
     */
    protected function setupContainer()
    {
        $this->container->bindIf('files', function () {
            return new Filesystem;
        }, true);
        $this->container->bindIf('events', function () {
            return new Dispatcher;
        }, true);
        $this->container->bindIf('config', function () {
            return [
                'view.paths' => (array) $this->viewPaths,
                'view.compiled' => $this->cachePath,
            ];
        }, true);
    }

    protected function registerViewFinder()
    {
        $this->container->bind('view.finder', function ($app) {
            return new FileViewFinder($this->container['files'], [$this->viewPaths], ['blade.php']);
        });
    }


    /**
     * Render shortcut.
     *
     * @param  string $view
     * @param  array  $data
     * @param  array  $mergeData
     *
     * @return string
     */
    public function render($view, $data = [], $mergeData = [])
    {
        return $this->container['view']->make($view, $data, $mergeData)->render();
    }
    /**
     * Get the compiler
     *
     * @return mixed
     */
    public function compiler()
    {
        $bladeEngine = $this->engineResolver->resolve('blade');
        return $bladeEngine->getCompiler();
    }
    /**
     * Pass any method to the view factory instance.
     *
     * @param  string $method
     * @param  array  $params
     * @return mixed
     */
    public function __call($method, $params)
    {
        return call_user_func_array([$this->container['view'], $method], $params);
    }
}
```

---