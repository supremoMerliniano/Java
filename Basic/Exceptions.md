# Exceptions

We can use the `try-catch` statement to manage exceptions. The `finally` block always execute. We can process many exception types, you have to add a `catch` block for every exception you want to process.

```java
try {

} catch (SQLException e) {
	e.prinStackTrace();
} catch(Exception e1) {

} finally {

}
```

The `throws` keyword in Java is used in the signature of a method to indicate that this method might throw one of the listed type exceptions.

```java
public static Connection getConexion() throws SQLException {
	
}
```


## Checked Exceptions

Are also known as compile-time exceptions as these exceptions are checked by the compiler during the compilation process to confirm whether the exception is handled by the programmer or not. If not, then the system displays a compilation error.

We have to process the using a try-catch statement or report it on the method signature by using `throws`.



## Unchecked Exceptions

Those exceptions that occur during the execution of the program. Hence they are also referred to as Runtime exceptions.