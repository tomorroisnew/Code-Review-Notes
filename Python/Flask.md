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
Aside from route, we can also use `.endpoint()` which works like route, and `.before_request()`, this triggers on every requests, before the request is made, so worth checking out, and `.after_request()`, just like `before_request()`  but triggers after every requests.    
There is also a function called `add_url_rule()`. It is the same as `.route()`. `.route()` is just a decorator for `add_url_rule()`. The syntax for it is `add_url_rule("/endpoint", view_func=func_to_exec)`

# USER INPUTS
Like i said, flask is simple. To get form parameters, use `request.form`, it is a dictionary. To get get parmeters, use `request.args.get()`.  To get files parameters, use `request.files`, it is also a dictionary. 

# TEMPLATES
Django uses jinja2 for templating. The function for rendering templates is `render_template()`. The syntax is `render_template('template.html', argname=argvalue)`. Normally, variables in templates are automatically escaped that protects to xss. However, using the safe filter or autoescape off will disable the auto encoding. 

# SQLAlchemy
SQLAlchemy is like flask's implementation of models. It works like sql. In sqlalchemy, tables are classes. These classes have columns which corresponds to the Columns in the database. Example    
```python
class User(UserBase, Base):
    __tablename__ = 'user'
    __table_args__ = {'sqlite_autoincrement': True}

    id = Column(Integer, primary_key=True)
    name = Column(String(64), unique=True)
    email = Column(String(120), unique=True, default="")
    role = Column(SmallInteger, default=constants.ROLE_USER)
    password = Column(String)
```
Column is a class. The first argument of column is the datatype, and it has multiple optional arguemnts. This can then be queried using `.session.query(User)`. This will return a Query object which has alot of methods on its own like `.filter()`. Example. 
```py
user1 = db.session.query(User).filter(User.id == 1)
```    
`User.query.filter(User.id == 1)` can also work. It is the same as above.
