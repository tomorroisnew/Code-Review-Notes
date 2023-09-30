# ROUTING
Routes can be found in `app/Config/Routes.php`. There is a `RouteCollection` class object called `$routes`
Routes are routed this way
```php
<?php

$routes->get('/', 'Home::index'); #Home is the class, index is the function. If no function is given, the default function is the index function
$routes->get('product/(:num)', 'Catalog::productLookupByID/$1'); ## Routing with variable in url

## OTher methods
$routes->post('products', 'Product::feature');
$routes->put('products/1', 'Product::feature');
$routes->delete('products/1', 'Product::feature');

$routes->match(['get', 'put'], 'products', 'Product::feature'); ## Multiple methods

$routes->add('products', 'Product::feature'); ## Any method

$multipleRoutes = [
    'product/(:num)'      => 'Catalog::productLookupById',
    'product/(:alphanum)' => 'Catalog::productLookupByName',
];

$routes->map($multipleRoutes); ## Multiple add like

## Grouping routes
$routes->group('admin', static function ($routes) {
    $routes->get('users', 'Admin\Users::index');
    $routes->get('blog', 'Admin\Blog::index');
});
```

# Requests
The request object can be accessed through `$this->request`, response is `$this->response` 
