# Useful Terms

## Context Path

The **Context path** refers to the base URL path under which a web application is accessed. It helps identify and differentiate one web application from another when multiple applications are deployed on the same web server.

Think of the context path as the "folder" or "directory" in the URL hierarchy that represents a specific web application.

By default, in Spring Boot, the context path is set to `/`, meaning that the application is accessible at the root of the server URL. For example, if the server URL is `http://localhost:8080`, the application would be accessed directly at `http://localhost:8080`.

To set a custom context path in a Spring Boot application, you can define the server.servlet.context-path property in the application.properties file. For example:

```bash
server.servlet.context-path=/myapp
```

