Wordpress is one of the most famous cms in the world. When hacking it, you will mostly be targetting the plugins. It is not hard and basic knowledge of php is required

# HOOKS and FILTERS
In wordpress, there are hooks and filters. They are nearly similar. There are alot of default hooks in wordpress. You can hook them using the function add_action. Example ```add_action("wp_ajax_nopriv_hook", "func_to_hook")```.   
When wp_ajax_nopriv_hook is triggered, the function func_to_hook will be executed. There are alot of hooks in wordpress and i recommend you checking them all. You can start up by grepping all add_action and all add_filter functions. The documentation is your friend when you dont know what a hook do.    
When looking for unauthenticated bugs, the most common hooks are wp_ajax_nopriv, admin_post_nopriv, admin_init, init, template_redirect,  plugins_loaded, wp_loaded, wp_head, wp_footer, and parse_request

# API
Wordpress has an api and you can add your api endpoints into it using the ```register_rest_route()``` function. Example   
The syntax is ```register_rest_route("v1/namespace", "endpoint/sample", [args])```. This api endpoint can then be access in `/wp-json/v1/namespace/endpoint/sample`   
The args is a dictionary of values
The three most famous arguments are methods, this is the http method - like GET or POST, callback - the function to be called when the endpoint is accessed, and permission_callback - it is liek the callback but is called before the callback, it is normally used for permission checks.

# COMMON BUGS
All php bugs can exist in wordpress. However, we have to note, in wordpress, there is a thing called magic quotes. All $_REQUEST, $_GET, $_POST, $_COOKIES values are autmatically encoded. It appends backslash on quotes meaning, sqli can be harder to achieve, but xss is still possible. Also, in api, the parameters are not affected by this so there is a higher chance of sqli in api.

# PRACTICE
<https://wordpress.org/plugins/>
<https://gist.github.com/joncave/5348689>