# SUMMARY
net/http is the base http module for golang. It is simple

# ROUTING
Endpoints are routed using the `HandleFunc()` function. It takes two parameter, first is the route, and second is the function. The syntax is like this `http.HandleFunc("/route", functocall)`. When the function is called, two parmeters are automatically passed to it, the response and the request. Example
```go
http.HandleFunc("/api/admin/federation/send", admin.SendFederatedMessage)

func SendFederatedMessage(w http.ResponseWriter, r *http.Request) {
    //FUNCTION
}
```
When using mux, there is also another function called Handle for routing. Example
```go
api.BaseRoutes.Bot.Handle("/disable", disableFunc).Methods("POST")
```
Mux also has multiple functions that returns a router depending on what you need. Two of the most interesting functions are `PathPrefix()` and `Path()`. These will return a router object. We can then add handles to this router. 
Example
```go
Posts := api.BaseRoutes.APIRoot.PathPrefix("/posts")
Posts.Handle(handlefunc)
```

# REQUEST
Like i said, the second argument is the request, this contains all information about the request.    
To get the headers, you use `r.Header["HeaderToGet"]`. To get get parameters, you use `URL.Query()`. To get post parameters, you first need to parse the body using the `ParseForm()` then access the parameters with `r.Form["param"]` or `r.FormValue("param")` Examples
```go
func SendFederatedMessage(w http.ResponseWriter, r *http.Request) {
    user_agent := r.Header["User-Agent"]
    get_Param := r.URL.Query()["get_param"]
    r.ParseForm()
    post_param := r.Form["PostParam"]
    another_post_param := r.FormValue("PostParam") //Same As Above
}
```