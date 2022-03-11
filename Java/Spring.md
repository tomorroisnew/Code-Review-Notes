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