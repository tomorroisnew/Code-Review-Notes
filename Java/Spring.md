SPRING IS POORLY DOCUMENTED

# ROUTING
Spring allow routing through multiple decorators, namely
```java
@RequestMapping("/endpoint", method=POST)
@GetMapping("/endpoint")
@PostMapping("/endpoint")
@PutMapping("/endpoint")
@DeleteMapping("/endpoint")
@PatchMapping("/endpoint")
```
These endpoints can also contain variables, for example
```java
	@PatchMapping("/tags/{id}")
	public Tag updateTag(@PathVariable String id, HttpServletRequest req, HttpServletResponse res) {
		//Code
	}
```

# PARAMETERS
We use RequestParam for parameters, both for get and post parameters. Syntax:
```java
@GetMapping("/api/foos")
public String getFoos(@RequestParam String id) { //Get the id parameter
}

@PostMapping("/api/foos")
public String addFoo(@RequestParam(name = "id") String fooId, @RequestParam String name) { //Same as above.
}

@PostMapping("/api/foos")
public String addFoo(@RequestParam("id") String fooId, @RequestParam String name) { //Same as above.
}

@PostMapping("/import")
public String restore(@RequestParam("file") MultipartFile file){ //We can also set the variable type anything other than string
}

@PostMapping("/api/foos")
public String addFoo(@RequestHeader("header-parameter") int header-parameter) { //Same as above.
}
```

# MODELS 
models are like the templates in spring. They commonly end in .jsp extensions. To load a view, you use the class `ModelAndView`. To add variables to the view, you use the `addObject()` function in the `ModelAndView` object Example
```java
view = new ModelAndView("accounts/login");
view.addObject("isLogout", "Var1");
view.addObject("forwardUrl", "Var2");
```
In the Template, these variables can be accessed using `${var_name}`
```java
var forwardUrl = '${forwardUrl}' || '<c:url value="/" />';
window.location.href = forwardUrl;
```