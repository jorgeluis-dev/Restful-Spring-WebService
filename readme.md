Building a RESTful Web Service with Spring
This guide walks you through the process of creating a “Hello, Name” RESTful web service with Spring.

What You Will Build
You will build a service that will accept HTTP GET requests at http://localhost:8080/greeting.

It will respond with a JSON representation of a greeting, as shown below:

```
    {"id":1,"content":"Hello, Name!"}` `
    
    You can customize the greeting with an optional name parameter in the query string, as shown below:

http://localhost:8080/greeting?name=User` 

```