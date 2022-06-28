---
layout: post
title: PHP Iterator class example
date: 2022-06-28 02:06 +0000
---

## Iterator interface

```php
interface Iterator extends Traversable {
    /* Methods */
    public current(): mixed
    public key(): mixed
    public next(): void
    public rewind(): void
    public valid(): bool
}
```

## Implements example
```php
class Loop implements Iterator
{
    private $list = ['a', 'b', 'c'];

    private $index = 0;

    public function rewind()
    {
        $this->index = 0;
    }

    public function next()
    {
		$this->index++;
    }

	public function key()
	{
		return $this->index;
	}

    public function current()
    {
        return $this->list[$this->index];
    }
	
	public function valid()
	{
		return array_key_exists($this->index, $this->list);
	}		
}


$loop = new Loop();

while ($loop->valid()) {
	echo sprintf("%s<br /> \n", $loop->current());
	$loop->next();
}
	

echo "<br />\n";
	
foreach($loop as $key => $value) {
	echo sprintf("%d - %s<br /> \n", $key, $value);
}

```
