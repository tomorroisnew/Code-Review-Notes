LARAVEL IS COOL

# ROUTING
Routing in laravel is done using the `Route` class. The Route class has multiple functions for routing, there are
```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
Route::match(['get', 'post'], '/', function () {
    //
});
 
Route::any('/', function () {
    //
});
```
If a route returns a view, (views are like templates in laravel), you can use the `Route::view()` function
```php
Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```
We can add variables to the url to make it dynamic, for example
```php
Route::get("/user/{name}", function (Request $request, $name));
```
request is a parameter that is automatically added to callback functions. We can add names to routes. You can ignore it, these are only used for url generation, but the syntax for naming a route is 
```php
Route::get('/user/{id}/profile', function ($id) {
    //
})->name('profile');
```
There are more functions in the routing class, if you found a function that is not explained here, refer to the documentation, but these are what commonly are used. 

# CONTROLLERS
In php, you can make classes that extends the Controller class. These classes then can be used for routing, for example
```php
class UserController extends Controller
{
    public function show($id)
    {
        return view('user.profile', [
            'user' => User::findOrFail($id)
        ]);
    }
}
```
We then can call this show function through a route like
```php
Route::get('/user/{id}', [UserController::class, 'show']); or
Route::get('/user/{id}', "UserController@show")
```

# REQUESTS
Like i said earlier, on the callback functions, there is always a request argument. This holds all the informations about the requests. These are some of the interesting things in the Request class
```php
$request->header('X-Header-Name'); //GET HEADER VALUE
$name = $request->input('name'); // GET POST PARAMETERS
$name = $request->query('name'); // GET GET PARAMETERSS
$input = $request->only(['username', 'password']); // GET ONLY THE username and password parameter
$input = $request->except('credit_card'); //GET ALL INPUT EXCEPT FOR credit_card
$request->file('photo') // FILE PARAMETERS
```
There are other functions that allow us to get user inputs but these are the most common ones, if you found anything not in here, check out the docs.

# VIEWS
Views are like the template in laravel. Views are php files in `resources/views` that ends in `.blade.php`. Views uses the blade, templating engine. These views can be called using the function view() or the View class. Examples
```php
return view('greeting', ['name' => 'James']); //RENDER greeting.blade.php, with the variable name = James.
return View::make('greeting', ['name' => 'James']); //SAME AS ABOVE
return view('greeting')->with('name', 'James') //ANOTHER WAY TO PASS VARIABLES
```
There are other functions in View class, if you found one that is not listed here, check out the docs, but these are the most common ones.

