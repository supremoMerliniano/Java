# Query Methods

Provide a way to define database queries by method naming conventions. These methods are automatically converted into SQL queries by the Spring framework, saving you from writing explicit SQL statements.

## Where to declare them

- **Repository Interfaces:** Query methods should be declared in interfaces that extend `JpaRepository` (or a similar repository interface provided by Spring Data JPA). These interfaces define the methods that can be used to interact with the database.
- **Custom Repository Interfaces:** You can create custom repository interfaces (e.g., CustomUserRepository) where you can declare additional query methods that  are specific to your application. These interfaces should also extend the base repository interface (JpaRepository).
- **Entity Classes:** You can also annotate your entity classes with `@Query` annotations to specify custom JPQL (Java Persistence Query Language) or native SQL queries.

## Simple Property Expressions

- **`findBy<Property>:`** Finds records where the specified property matches the given value.
- **`findBy<Property>And<Property>:`** Finds records where both properties match their respective values.
- **`findBy<Property>Or<Property>:`** Finds records where either of the properties match their respective values.

**Example:**

```java
List<User> findByLastName(String lastName);
List<User> findByFirstNameAndLastName(String firstName, String lastName);
List<User> findByAgeOrFirstName(int age, String firstName);
```

## Derived Query Methods with Sorting and Pagination

- **`findBy<Property>OrderBy<Property>:`** Finds records ordered by the specified property.
- **`findBy<Property>OrderBy<Property>Desc:`** Finds records ordered by the specified property in descending order.
- **`findBy<Property>OrderBy<Property>Desc(Pageable pageable):`** Paginates the result set.

**Example:**

```java
List<User> findByLastNameOrderByFirstNameAsc(String lastName);
Page<User> findByAge(int age, Pageable pageable);
```

## Counting Queries

- **`countBy<Property>:`** Counts the number of records with the specified property.

**Example:**

```java
long countByAge(int age);
```

## Exists Queries

- **`existsBy<Property>:`** Checks if a record with the specified property exists.

**Example:**

boolean existsByEmailAddress(String email);

## In Queries

- **`findBy<Property>In(List<Value>):`** Finds records where the property value is in the provided list.

**Example:**

```java
List<User> findByAgeIn(List<Integer> ages);
```

## IsNull and IsNotNull Queries

- **`findBy<Property>IsNull:`** Finds records where the property value is null.
- **`findBy<Property>IsNotNull:`** Finds records where the property value is not null.

**Example:**

```java
List<User> findByMiddleNameIsNull();
List<User> findByMiddleNameIsNotNull();
```

## Like Queries

- **`findBy<Property>Like(String pattern):`** Finds records where the property value matches a pattern.

**Example:**

```java
List<User> findByLastNameLike(String pattern);
```

## Starting With, Ending With

- **`findBy<Property>StartingWith(String prefix):`** Finds records where the property value starts with the given prefix.
- **`findBy<Property>EndingWith(String suffix):`** Finds records where the property value ends with the given suffix.

**Example:**

```java
List<User> findByFirstNameStartingWith(String prefix);
List<User> findByEmailAddressEndingWith(String suffix);
```
