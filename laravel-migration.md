---
layout: page
title: Laravel Migration
---


# Database
## SQlite

### Create empty sqlite database [^sqlite_new]

[^sqlite_new]: [Create empty sqlite db from command line](https://stackoverflow.com/questions/20155693/create-empty-sqlite-db-from-command-line)

```bash
sqlite3 file.db "VACUUM;"
```

# Table

## Check table

```php
if (!Schema::hasTable('table_name')) {
	// Opt tables
}
```

## Check table column
```php
if (Schema::hasColumn('table_name', 'column_name')) {

}
```


## Create table
```php
Schema::create('table_name', function (Blueprint $table) {
    $table->increments('id');

    $table->integer('foreign_id')->unsigned();
    $table->foreign('foreign_id')->references('id')->on('foreign_table')->onDelete('cascade');

    $table->string('key');
    $table->text('value')->nullable(true);
    $table->timestamps();
});
```

### Create table with foreign key

```php
Schema::create('link_product_retailer', function (Blueprint $table) {
    $table->increments('id');
    $table->integer('product_id')->unsigned()->nullable();
    $table->integer('retailer_id')->unsigned()->nullable();
    $table->foreign('product_id')->references('id')->on('products');
    $table->foreign('retailer_id')->references('id')->on('retailers');
});
```

## Foreign Key

### Drop Foreign Key
```php
Schema::table('table', function(Blueprint $table){
    $table->dropForeign('foreign_name');
});
```

## Index
### Add index
```php
Schema::table('table', function(Blueprint $table) {
    $table->index(['col1', 'col2']);
});
```

### Remove index
```php
Schema::table('table', function(Blueprint $table) {
    $table->dropIndex('index_name');
});
```

## Rename table
```php
Schema::rename('table_name', 'new_table_name');
```

## Drop table
```php
Schema::dropIfExists('table_name');
 // DROP TABLE IF EXISTS `table_name`;
```

# View

## Create view
```php
DB::statement("
        CREATE 
            OR REPLACE 
            SQL SECURITY INVOKER
        VIEW `view_name` AS

        SELECT * 
        FROM `table`
        ")

```
## Drop view
```php
DB::statement('DROP VIEW IF EXISTS `view_name`;');
```

# Table row
```php
\App\Models\Model::where( [
    'key' => 'value'
])->first()->update([
    'key' => 'value'
    ],
]);
```


# Model

## Relationship


```mermaid
graph LR
A[Master] -- one to many --> B[Slave]
```

```php
$master->hasMany(Slave::class);
$slave->belongsTo(Master::class);
```

```mermaid
graph LR
E[Employer] --> L((employer_staff))
S[Staff] --> L((employer_staff))
```

```php
$employer->belongsToMany(Staff::class)
$staff->belongsToManu(Employer::class)
```

```mermaid
graph LR
U[User] -- one to one --> N[Name]
```

```php
$user->hasOne(Name::class)
$name->hasOne(User::class)
```
