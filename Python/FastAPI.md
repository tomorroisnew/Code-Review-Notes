I was forced to learn this because of microsoft

# PYDANTIC
FastAPI use Pydantic, as models. Pydantic allows us to make class models by interpreting through its BaseModel class. This will be important later. For example
```python
class Item(BaseModel):
    name: str
    description: Optional[str] = None
```

# ROUTING
In fastapi, like in flask, we use the decorator `.get`, `.post`, `.put`, `.delete` to define routes. For example, a simple route
```python
@app.get("/")
async def root():
    return {"message": "Hello World"}
```
This Whenever you access the `/` endpoint, the root function will be executed. We can also add path parameters on our endpoint. The parameter will be passed as an argument to the function. optionally, we can also define the type of the parameter with different data types like string, int, or a class. For example
```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

# USER INPUTS
When you add a parameter on a function, that is not a path parameter, it will be interpreted as query or a body parameter parameter. For example
```python
@app.get("/items")
async def read_item(item_id: int = 0):
    return {"item_id": item_id}
# This endpoint can be called with /items?item_id=12
```
For post parameters, we can use Pydantic to read the request body. You can then access the attributes of the class. For example
```python
class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: Optional[float] = None

@app.post("/items/")
async def create_item(item: Item):
    return item.name
```
Alternatively, if we are not using json and is using forms, we need to use the Form class to a parameter for it to be interpreted as a form value
```python
@app.post("/login/")
async def login(username: str = Form(...), password: str = Form(...)):
    return {"username": username}
```
For cookies, we need to add `Cookie(None)` to a parameter to be interpreted as a cookie value. We need to add `Header(None)` to a parameter to be interpreted as a header value
```python
@app.get("/items/")
async def read_items(ads_id = Cookie(None), header = Header(None)):
    return {"ads_id": ads_id, "header": header}
```

# TEMPLATES
Fastapi use Jinja for templating. To render a template, we use the `templates.TemplateResponse` function. The first argument is the template file, and the second argument is the contexts for the template. 
```python
@app.get("/items/{id}", response_class=HTMLResponse)
async def read_item(request: Request, id: str):
    return templates.TemplateResponse("item.html", {"request": request, "id": id})

"""item.html
<html>
<head>
    <title>Item Details</title>
    <link href="{{ url_for('static', path='/styles.css') }}" rel="stylesheet">
</head>
<body>
    <h1>Item ID: {{ id }}</h1>
</body>
</html>
"""
```

# WEBSOCKET
To define a route as a websocket function, we use the `.ws` decorator. To send and recive data from the websocket, we use the `receive_text`, and `send_text` function respectively. For example.
```python
@app.websocket("/ws")
async def websocket_endpoint(websocket: WebSocket):
    await websocket.accept()
    while True:
        data = await websocket.receive_text()
        await websocket.send_text(f"Message text was: {data}")
```