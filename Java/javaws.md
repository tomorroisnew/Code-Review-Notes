Also poorly documented

# ROUTING
Routing is done with the Path decorator. We also set the request method using decorators.
```java
@DELETE
@Path("/{id}/users/{userid}")
public ServiceResult removeUser(@PathParam("id") Long id ,@PathParam("userid") Long userid) throws ServiceException
{
}
```

# PARAMETERS
Parameters can be added as arguments to a function using the PathParam, WebParam, QueryParam, FormParam
```java
@DELETE
@Path("/{id}/users/{userid}")
public ServiceResult removeUser(@PathParam("id") Long id ,@PathParam("userid") Long userid, @QueryParam("queryparam") String query, @WebParam("WebParam") String Web) throws ServiceException
{
}
```