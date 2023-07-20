
# Building a RESTful Web Service with Spring

This guide walks you through the process of creating a "Hello, Name" RESTful web service with Spring.

## What You Will Build

You will build a service that will accept HTTP GET requests at http://localhost:8080/greeting.

It will respond with a JSON representation of a greeting, as shown below:

```json
{"id":1,"content":"Hello, Name!"}` 

You can customize the greeting with an optional name parameter in the query string, as shown below:

bashCopy code

`http://localhost:8080/greeting?name=User` 

The name parameter value overrides the default value of "Name" and is reflected in the response, as shown below:

jsonCopy code

`{"id":1,"content":"Hello, User!"}` 

## What You Need

-   About 15 minutes
-   A favorite text editor or IDE
-   Java 17 or later
-   Gradle 7.5+ or Maven 3.5+

You can also import the code straight into your IDE:

-   Spring Tool Suite (STS)
-   IntelliJ IDEA
-   VSCode

## How to Complete This Guide

Like most Spring Getting Started guides, you can start from scratch and complete each step, or you can bypass basic setup steps that are already familiar to you. Either way, you'll end up with working code.

### Starting with Spring Initializr

1.  You can use the pre-initialized project [here](https://start.spring.io/) and click "Generate" to download a ZIP file. This project is configured to fit the examples in this tutorial.
    
2.  Alternatively, manually initialize the project by navigating to [https://start.spring.io](https://start.spring.io/). Choose either Gradle or Maven and the language you want to use (this guide assumes Java).
    
3.  Click "Dependencies" and select "Spring Web".
    
4.  Click "Generate" and download the resulting ZIP file.
    

### Create a Resource Representation Class

Now that you have set up the project and build system, you can create your web service.

To model the greeting representation, create a resource representation class. To do so, provide a Java record class for the id and content data, as shown below:


`package com.spring.restfullService;

public record Greeting(long id, String content) { }` 

This application uses the Jackson JSON library to automatically marshal instances of type Greeting into JSON.

### Create a Resource Controller

In Spring’s approach to building RESTful web services, HTTP requests are handled by a controller. These components are identified by the `@RestController` annotation, and the GreetingController handles GET requests for `/greeting` by returning a new instance of the Greeting class.

`package com.spring.restfullService;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @GetMapping("/greeting")
    public Greeting greeting(@RequestParam(value = "name", defaultValue = "Name") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
}` 

The `@GetMapping` annotation ensures that HTTP GET requests to `/greeting` are mapped to the `greeting()` method.

The `@RequestParam` binds the value of the query string parameter "name" into the `name` parameter of the `greeting()` method. If the "name" parameter is absent in the request, the defaultValue of "Name" is used.

This controller populates and returns a Greeting object. The object data will be written directly to the HTTP response as JSON, thanks to Spring's HTTP message converter support.

### Build 

You can run the application from the command line with Gradle or Maven. You can also build a single executable JAR file that contains all the necessary dependencies, classes, and resources and run that.

To build the JAR file using Gradle:

`./gradlew build`