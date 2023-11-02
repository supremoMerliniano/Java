_Spring RestController_ annotation is used to create RESTful web services using _Spring_ MVC.
To indicate that we are using a _RestController_ in the header we use the `@RestController` annotation


## Response Entity

In Spring Framework, a `ResponseEntity` represents the entire HTTP response, including the status code, headers, and body.

Here's a breakdown of what `ResponseEntity` encompasses:

1. **Status Code**: It includes the HTTP status code, like 200 for success, 404 for not found, 500 for internal server error, etc.
2. **Headers**: You can add custom headers to the response. This is useful for setting content type, caching directives, or any other custom headers required.
3. **Body**: This is the actual content of the response. It could be a JSON object, HTML content, an image, or any other type of data.

**Example:**

```java
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/user/{id}")
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        // Assume userService.getUserById(id) returns a User object
        User user = userService.getUserById(id);

        if (user != null) {
            return ResponseEntity.ok(user); // Returns a 200 OK status with the user object
        } else {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body(null); // Returns a 404 Not Found status
        }
    }
}

```


## Request Mapping

Is used to map HTTP requests to methods in your controller classes. It is one of the fundamental annotations for creating RESTful web services and handling incoming HTTP requests. The annotation is used to define which HTTP methods (GET, POST, PUT, DELETE, etc.) should be handled by specific methods in your Spring controller.

```java
@RestController @RequestMapping("/api")
public class MyController { 
	@RequestMapping(value = "/hello", method = RequestMethod.GET) 
	public String helloWorld() { 
		return "Hello, World!"; 
	}
}
```

1. The `@RestController` annotation indicates that this class will be a controller that handles incoming HTTP requests and produces responses.
2. The `@RequestMapping` annotation at the class level ("/api") establishes a base URL for all methods within the controller.
3. The `@RequestMapping` annotation at the method level ("/hello") maps the method to the specified URL.
4. The `method` attribute of the `@RequestMapping` annotation specifies that this method should handle only HTTP GET requests.

So, when a client sends an HTTP GET request to the URL `"/api/hello"`, the `helloWorld` method will be invoked, and the returned string "Hello, World!" will be sent back as the response.
It's worth noting that starting from Spring 4.3, you can use more specific annotations like `@GetMapping`, `@PostMapping`, `@PutMapping`, and `@DeleteMapping` to make your code more readable and concise.


## Get Mapping

Is an annotation designed for handling HTTP GET requests.

```java
@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/hello")
    public String helloWorld() {
        return "Hello, World!";
    }
}

```

In this example:

1. The `@RestController` annotation marks the class as a controller that handles incoming HTTP requests and generates responses.
2. The `@RequestMapping` annotation at the class level ("/api") establishes a base URL for all methods within the controller.
3. The `@GetMapping("/hello")` annotation is applied to the `helloWorld` method. This annotation indicates that the method should be triggered when an HTTP GET request is made to the "/api/hello" URL.
4. The method `helloWorld()` returns the string "Hello, World!" which will be sent back as the response when the corresponding URL is accessed with a GET request.


## Post Mapping

Is an annotation designed for handling HTTP POST requests.

```java
@PostMapping  
public ResponseEntity<PizzaEntity> add(@RequestBody PizzaEntity pizza) {  
    if (pizza.getIdPizza() == null || !this.pizzaService.exists(pizza.getIdPizza())) {  
        return ResponseEntity.ok(this.pizzaService.save(pizza));  
    }  
  
    return ResponseEntity.badRequest().build();  
}
```

1. `@PostMapping`: This annotation indicates that this method will handle HTTP POST requests. In this case, the method will be triggered when a POST request is made to the URL associated with this controller.
2. `ResponseEntity<PizzaEntity>`: This specifies that the method will return a `ResponseEntity` containing a `PizzaEntity`. `ResponseEntity` allows you to control the HTTP response, including status codes and headers.
3. `@RequestBody PizzaEntity pizza`: This annotation tells Spring to bind the request body to the `pizza` parameter. It's expecting the request body to be in JSON format that can be mapped to a `PizzaEntity` object.
4. This is an `if` statement that checks two conditions:
	- `pizza.getIdPizza() == null`: Checks if the `idPizza` of the `PizzaEntity` is `null`. This would mean that the pizza doesn't have an ID yet, which implies it's a new pizza.
	- `!this.pizzaService.exists(pizza.getIdPizza())`: Calls a method `exists()` on a `pizzaService` object. This method likely checks if a pizza with the given ID already exists in the database.
	If either of these conditions is true, it means that the pizza is new or doesn't already exist in the database. And that would return a `ResponseEntity` with a 200 OK status code and a body containing the saved `PizzaEntity`. `this.pizzaService.save(pizza)` likely saves the `PizzaEntity` to a database and returns the saved instance. If none of the conditions in the `if` statement were met, this line is executed. It returns a `ResponseEntity` with a 400 Bad Request status code. `.build()` creates a `ResponseEntity` with no body.

## Put Mapping

