No comment

# ROUTING
We can use the `Route()` decorator(i am not sure if it is called decorator in c#), to route a function. For example.
```C#
        [Route("Demo/Contact")]
        public IActionResult Contact()
        {
            return Content("Contact content");
        }
```
Alternatively, we can also use `HttpGet`, `HttpPost`, `HttpDelete`, `HttpPut` and `HttpPatch`. We can also add path parameter to the route and it will be added as a parameter in the function to be called.
```c#
    [HttpGet("/api/product/{productId}")]
    public async Task<ObjectResult> GetProductAsync(string productId)
    {
        //func
    }

    [HttpPost("/api/product/{productId}")]
    public async Task<ObjectResult> PostProductAsync(string productId)
    {
        //func
    }
    //You get the idea
```
We can also set the route in the class, and add the Http methods decorator in the functions. For example
```C#
    [Route("api/lucene")]
    public class ApiController : Controller
    {
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            //function
        }
        [HttpPost]
        public async Task<IActionResult> Post()
        {
            //function
        }
    }
```
## AREAS
Another way of routing is through the use of areas. Routing is done by the function `MapAreaControllerRoute`. It takes 4 parameter, name, areaName, pattern, and defaults. The only important thing is pattern and defaults. The route is defined in the pattern and the function to be called is in the defaults action parameter. Example
```C#
            routes.MapAreaControllerRoute(
               name: "DownloadDownload",
               areaName: "OrchardCore.Contents",
               pattern: _adminOptions.AdminUrlPrefix + "/Download/Download/{contentItemId}",
               defaults: new { controller = downloadControllerName, action = nameof(DownloadController.Download) }
           );
           //"/Download/Download/{contentItemId}" calls the function DownloadController.Download
```
MapControllerRoute also exist but its nearly similar with MapAreaControllerRoute