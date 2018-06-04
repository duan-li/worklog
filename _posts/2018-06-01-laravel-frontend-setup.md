---
layout: post
title: Laravel frontend setup
date: 2018-06-01 16:30 +0000
---


Install laravel
`composer create-project --prefer-dist laravel/laravel project`


Host laravel
`php artisan serve`



Install npm components
```
npm install
```

add `/node_modules` to `.gitignore` file


Run npm
```
// Run all Mix tasks...
npm run dev

// Run all Mix tasks and minify output...
npm run production
```

or watch any file changed
```
npm run watch
```


Install bower
```
npm install -g bower
```

add .bowerrc file into project root
```
{
  "directory": "resources/bower-resources"
}
```



add file `bower.json`
```
{
  "name": "assert",
  "dependencies": {
    "jquery": "^2.2.0",
    "bootstrap": "~4.1.1",
    "gentelella": "~1.4.0"
  },
  "resolutions": {
    "jquery": "^2.2.0"
  },
  "private": true
}


```


Run
```
bower install
```

make sure .gitignore file contain
```
/node_modules
/public
resources/bower-resources/
```





Ref
 - [Laravel5-Bootstrap3-Starter-Site](https://github.com/Askedio/Laravel5-Bootstrap3-Starter-Site) 
 - [web pack example](https://github.com/ehsanhasani/laravel-5-angular-4/blob/master/webpack.mix.js)