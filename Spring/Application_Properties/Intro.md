# Intro

The application.properties file is used to configure various properties and settings for your application. It is a key-value pairs file that allows you to customize the behavior of your Spring Boot application without modifying the source code.

## Use Cases

1. Application-level configuration: You can specify properties related to your application, such as the application name, server port, context path, logging settings, etc. For example:

```bash
spring.application.name=MyApp
server.port=8080
logging.level.org.springframework=INFO
```

2. Database configuration: You can configure the database connection properties, such as the database URL, username, and password. For example:

```bash
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
```

3. External service configuration: If your application interacts with external services like email servers, message queues, or APIs, you can configure the connection details and credentials in the application.properties file. For example:

```bash
mail.host=smtp.gmail.com
mail.port=587
mail.username=myemail@gmail.com
mail.password=mypassword
```

4. Profile-specific configuration: You can define different sets of properties for different environments or profiles, such as development, production, or testing. This allows you to customize settings based on the deployment environment. For example:

```bash
# Development profile
spring.profiles.active=dev
spring.datasource.url=jdbc:mysql://localhost:3306/devdb

# Production profile
# spring.profiles.active=prod
# spring.datasource.url=jdbc:mysql://localhost:3306/proddb
```

5. Custom application-specific properties: You can define custom properties specific to your application and access them in your code using the @Value annotation or Environment object. This provides a convenient way to externalize configurable values. For example:

```bash
myapp.feature.enabled=true
myapp.api.key=abc123
```

