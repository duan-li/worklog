---
layout: post
title: Artisan commands
date: 2018-07-23 06:30 +0000
---


# input

```php
$this->argument('argumentName');

$this->option('optionName')
```



# output

```php
$this->info('Finished syncing data');
$this->error('Finished syncing data');
$this->comment('Finished syncing data');
$this->question('Finished syncing data');
$this->confirm('Do it?');
```

```php
$this->secret()
$name = $this->ask("What is your name?")
$this->anticipate();
$this->choice();
```


## table
```php

$headers = ['name', 'type'];

$data = [
	[
		'name' => 'name 1',
		'type' => 'staff'
	],
	[
		'name' => 'name 1',
		'type' => 'staff'
	]
];

$this->table($headers, $data);

```

## progress bar
```
public function handle()
{
    $this->output->progressStart(10);

    for ($i = 0; $i < 10; $i++) {
        sleep(1);

        $this->output->progressAdvance();
    }

    $this->output->progressFinish();
}
```





Ref:
* https://mattstauffer.com/blog/advanced-input-output-with-artisan-commands-tables-and-progress-bars-in-laravel-5.1/
