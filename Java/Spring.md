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
```