Django is the most famous python web framework. Complicated but fun to hack.

# ROUTING
Commonly, django apps has a urls.py file, which contains the endpoints that can be accessed in the website.  
Django uses 3 functions to route endpoints, ```path()```, ```re_path()```, and ```urls()```. The syntax is ```path("/endpoint", FUNCTION_TO_CALL)```  
## Examples
![](Django_routing.PNG)

# Class Based Views
In the example, you can see multiple ```as_view()``` function, this is a class based view  
These Classes Inherits from the View Class  
When the ```as_view()``` function is called, it will call ```dispatch()```, dispatch function will dispatch the request. If the request is get, it will call the ```get()``` function, if the request is post, it will call the post function.  
The flow is ```as_view()``` -> ```dispatch()``` -> ```get()```/```post()``` . Next, i will be discussing some of the builtin views of django.

# Template View
```python
class TemplateView(TemplateResponseMixin, ContextMixin, View):
    """
    Render a template. Pass keyword arguments from the URLconf to the context.
    """
    def get(self, request, *args, **kwargs):
        context = self.get_context_data(**kwargs)
        return self.render_to_response(context)
```
TemplateView inherits the ```View``` class and ```TemplateResponseMixin```, and ```ContextMixin```. The two mixin provide additional functionalities for this view.  
It has a get function which is called by the dispatch function of the View Class.  
It calls the get_context_data function which is in the ContextMixin.
```python
class ContextMixin:
    """
    A default context mixin that passes the keyword arguments received by
    get_context_data() as the template context.
    """
    extra_context = None

    def get_context_data(self, **kwargs):
        kwargs.setdefault('view', self)
        if self.extra_context is not None:
            kwargs.update(self.extra_context)
        return kwargs
```
It gets the kwargs and return it. Which is then stored in the context variable in the TemplateView ```get()``` function.