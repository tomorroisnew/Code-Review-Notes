Ye.

# ROUTING
In symfony, there are yaml files that stores the routes. To find it, search for the keyword `path: `, for example
```yaml
admin_import_data_configuration_index:
    path: /data
    methods: [POST]
    defaults:
        _controller: 'PrestaShopBundle:Admin\Configure\AdvancedParameters\ImportDataConfiguration:index'
        _legacy_controller: AdminImport
```
This will call the function `ImportDataConfiguration:index` when `/data` is accessed. Another way to route is through the use of `#[Route()]` or `@Route()` attributes. Example
```php
    #[Route('/api/posts/{id}', methods: ['GET', 'HEAD'])]
    public function show(int $id): Response
    {
        // ... return a JSON response with the post
    }
```
Another method is through the use of `$routes->add`. For example
```php
    $routes->add('blog_show', '/blog/{slug}')
        ->controller([BlogController::class, 'show'])
    ;
```
There is another method, called xml by the documentation, but i doubt anyone will use that. Like other frameworks, we can add path parameters in the routes, just like what we did with the last example, and it will be added as an argument to the function to be called. For example
```php
    #[Route('/blog/{slug}', name: 'blog_show')]
    public function show(string $slug)
    {
        // ...
    }
```

# TEMPLATES
Symfony uses twig for templates. We use the `render` function to render a template. We can also pass the variables in there. For example
```php
return $this->render('lucky/number.html.twig', ['number' => $number]);
```
twig automatically filters all parameters. This can be disabled by using the `raw` filter, so when looking for xss, search for `|raw`

# PARAMETERS
On a controller, a request parameter is always passed on to it. That is where we can access all the request data and get the user inputs.
```php
public function index(Request $request): Response
{
    $request->isXmlHttpRequest(); // is it an Ajax request?

    $request->getPreferredLanguage(['en', 'fr']);

    // retrieves GET and POST variables respectively
    $request->query->get('page');
    $request->request->get('page');

    // retrieves SERVER variables
    $request->server->get('HTTP_HOST');

    // retrieves an instance of UploadedFile identified by foo
    $request->files->get('foo');

    // retrieves a COOKIE value
    $request->cookies->get('PHPSESSID');

    // retrieves an HTTP request header, with normalized, lowercase keys
    $request->headers->get('host');
    $request->headers->get('content-type');
}
```