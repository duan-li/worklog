---
layout: post
title: Symfony DomCrawler example
date: 2021-01-21 22:50 +0000
---

[Compont 5.0 Document](https://symfony.com/doc/5.0/components/dom_crawler.html)

```php

	$html = <<<'HTML'
<!DOCTYPE html>
<html>
    <body>
    	<dl class='item'>
    		<dd>
    			<a href=1>a</a>
			</dd>
		</dl>
		<dl class='item'>
    		<dd>
    			<a href=2>b</a>
			</dd>
		</dl>
    </body>
</html>
HTML;
	// $html = file_get_contents('url');

    $crawler = new Crawler($html);

    $chs = $crawler->filter('dl.item > dd > a');

    $a = [];
    if ($chs->count() > 0) {
        foreach($chs as $ch) {
            /** @var \DOMElement $ch */
            $a[] = [
                'url' => $ch->getAttribute('href'),
                'name' => $ch->textContent
            ];
        }
    }


```

