
Building a RESTful Web Service with Spring
This guide walks you through the process of creating a “Hello, Name” RESTful web service with Spring.

What You Will Build
You will build a service that will accept HTTP GET requests at http://localhost:8080/greeting.

It will respond with a JSON representation of a greeting, as shown below:

```json
{"id":1,"content":"Hello, Name!"}
    

http://localhost:8080/greeting?name=User`

package com.spring.restfullService;

import java.util.concurrent.atomic.AtomicLong;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.spring.restfullService.Greeting;

@RestController
public class GreetingController {

	private static final String template = "Hello, %s!";
	private final AtomicLong counter = new AtomicLong();

	@GetMapping("/greeting")
	public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
		return new Greeting(counter.incrementAndGet(), String.format(template, name));
	}
}
```



-   
-   Java 17 or later
-   Gradle 7.5+ or Maven 3.5+
-   Spring Tool Suite (STS)
-   VSCode

### Build

`./gradlew build`
