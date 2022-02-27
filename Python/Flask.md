Flask is another famous web framework for python. It is more simple than django.

# ROUTING
When routing in flask, we use the decorator function called route. They syntax of it is `.route("/endpoint", methods=['GET', 'POST'])`. Example   
```py
@app.route("/api/v1/users/", methods=['GET', 'POST', 'PUT'])
def users():
    #... Logic goes here
```    
We can also pass variables to the endpoints, and it will be an argument to the function. For example,    
```py
@app.route('/guest/<guest>')
def hello_guest(guest):
   return 'Hello %s as Guest' % guest
```
Aside from route, we can also use `.endpoint()` which works like route, and `.before_request()`, this triggers on every requests, before the request is made, so worth checking out.

# USER INPUTS
Like i said, flask is simple. To get form parameters, use `request.form`, it is a dictionary. To get get parmeters, use `request.args.get()`.  To get files parameters, use `request.files`, it is also a dictionary. 

# TEMPLATES
Django uses jinja2 for templating. The function for rendering templates is `render_template()`. The syntax is `render_template('template.html', argname=argvalue)`. Normally, variables in templates are automatically escaped that protects to xss. However, using the safe filter or autoescape off will disable the auto encoding. 