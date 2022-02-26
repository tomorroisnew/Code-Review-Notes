Express is a famous javascript library for backend development that can be used both on typescript and node. It is simple and you can see the api documentation here https://expressjs.com/en/api.html#res.location.

# ROUTING
Express has a class called Router which is responsible for routing endpoints. There are multiple functions for routing endpoints, most famous are get() post(), put(), delete(). The syntax is 
```js
router.get("/endpoint", function1, function2)
```
We can pass as many function as we want. There is also functions like all() and METHOD(). We can add variables to these endpoints like
```js
router.post('/survey/presession/:sessionId', async (req, res, next) => {
```

router.param() Adds callback triggers to route parameters . For example in the above route, we can make 
```js
router.param('sessionId', functocall)
```
every time the above endpoint or any endpoint that has sessionId, the function functocall will be called.
router.route() will return a route instace. For example
```js
router.route('/users/:user_id')
  .all(function (req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
    next()
  })
  .get(function (req, res, next) {
    res.json(req.user)
  })
  .put(function (req, res, next) {
    // just an example of maybe updating the user
    req.user.name = req.params.name
    // save user ... etc
    res.json(req.user)
  })
  .post(function (req, res, next) {
    next(new Error('not implemented'))
  })
  .delete(function (req, res, next) {
    next(new Error('not implemented'))
  })
```    
app.use(). Match and endpoint and execute the middlewares. Example    
```js
app.use('/abcd', function (req, res, next) {
  next()
})
```

# PARAMETERS
Like i said above, we can add variables to our endpoints, it can be obtained with req.params . req.params is dictionary. In our example, if i want to get sessionId, i will call ```req.params.sessionId``` or ```req.params[0]```  
For query parameters you can use `req.query` which is a dictionary of the query parameters. For post requests, you can use `req.body` which is also a dictionary of post parameters.  
There is also a function called `req.param()`. This is capable of getting the variable from post request, get request, and from the endpoint.