---
title: "Router in php"
description: "Simple router in php."
date: 2020-10-23
---
lets build our very own PHP’s router for managing our endpoints well for our next PHP project.
If you want to create simple web app like blog and the decision goes against large frameworks, the question of Pretty Url routing will eventually come up. How does one particular URL cause a certain content to be outputted? I want to describe a simple way of processing friendly URLs using RegExp and PHP's anonymous functions.
>###### 
>Note This article requires OOP and Regx knowledge
## A Very Simple PHP Router for Pretty URls

```PHP
class Router {
  public function route(String $url, Closure $callback) {
    $matches = array();
	  if (preg_match('~' . $url . '~', $_SERVER['REQUEST_URI'], $matches)) {
      array_shift($url);
		  return call_user_func_array($callback, $matches);
	  }
  }
}
```
Usage
```PHP
$url = new Router;
$url->route('/', function() {
  return 'Hello World';
});

$url->route('/blog/(\d+)', function($id) {
  return 'blogId => ' . $id;
});
```
