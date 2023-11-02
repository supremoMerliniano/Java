# Generics

Generics means parameterized types. The idea is to allow type (Integer, String, … etc., and user-defined types) to be a parameter to methods, classes, and interfaces. Using Generics, it is possible to create classes that work with different data types.

We have to use __Wrapper Classes__ of __primitive types__.

## Generic Class

Means that the items or functions in that class can be generalized with the parameter(example T) to specify that we can add any type as a parameter in place of T like Integer, Character, String, Double or any other user-defined type.

**Example:** Single type parameter

```java
public class GenericClass<T> {
	private T object;

	public GenericClass(T object) {
		this.object = object;
	}

	public void getType() {
		System.out.println(object.getClass().getSimpleName());
	}
}
```

**Implementation**

```java
public static void main(String[] args) {
GenericClass<Integer> intObject = new GenericClass(15);
GenericClass<String> stringObject = new GenericClass("Juan");

intObject.getType();
stringObject.getType();
}
```

## Generic Collections

We have to specify the _type_ inside the _diamond operator_ in the collection declaration.

```java
List listName<Type> = new ArrayList<>();
```

A `Map` is a particular case where we have to define th key and value types.

```java
Map mapName<Type, Type> = new HashMap<>();
```
