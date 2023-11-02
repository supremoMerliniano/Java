In the main file, where the `@SpringBootApplication` annotation is declared. Use the `@EnableJpaRepositories` to define that we are going to use the _JPA Repositories_.


## SELECT all

To select all elements from the database using _JPA Repositories_, use `findAll()` method

```java
public List<ClassEntity> getAll() {  
    return this.classRepository.findAll();  
}
```

## SELECT all WHERE id

To select all columns from a table and filtering by id, using _JPA Repositories_, use `findById()` method.

```java
public ClassEntity get(int id) {  
    return this.classRepository.findById(id).orElse(null);  
}
```
