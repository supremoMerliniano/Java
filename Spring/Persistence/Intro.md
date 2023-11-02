# Intro

This is the introduction for using Spring JPA

## Add dependency

First you need to add the `jpa` dependecy and the respective `jdbc` dependency to the `dependencies` section of the `build.gradle` file. The `jpa` dependency is an integral part so it needs to be added by using the `implementation` keyword. The `jdbc` dependecy only will be used when executing the application (runtime) so it has to be added by using the `runtimeOnly` keyword.

```groovy

dependencies {
	// https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-data-jpa
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa:3.1.1'

	// https://mvnrepository.com/artifact/org.postgresql/postgresql
	runtimeOnly 'org.postgresql:postgresql:42.6.0'
}
```

## Set the Datasource

In the application.properties, no matter if is the development or production profile, add the `driver-class-name`, `url`, `username` and `password`.

```bash
# Database
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/platzi-market
spring.datasource.username=postgres
spring.datasource.password=0202993180a+
```
