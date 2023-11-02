# Apuntes

lol

## Variables Paramaters

Syntax:

```java
public void functionName(tipo... variableName) { }
```

The variable arguments are converted to array type. The variables parameters must be the last in the parameters definition.

## Enums

Is a special "class" that represents a group of constants (`public`, `static` and `final`). An enum can, just like a class, have attributes, methods and a constructor. To call a method from the enum we have to do it as we where calling a method from an instance.

```java
public enum enumName {
	ENUM_ELEMENT1(1),
	ENUM_ELEMENT2(2);

	private int attributeName;

	enumName(int attributeName) {
		this.attributeName = attributeName;
	}

	public int getAttributeName() { return this.attributeName}
}
```

Printing the enum in console:

```java
public static void main(String[] args) {
	System.out.println("Element 1: " + enumName.ENUM_ELEMENT1);

	System.out.println("Attribute 1: " + enumName.ENUM_ELEMENT1.getAttributeName());
}
```

That would give us the follow out:

```sh
Element 1: ENUM_ELEMENT1
Attribute 1: 1
```

## ForEach

Syntax:

```java
for(dataType value: array) {
	System.out.println("Value: " + value);
}
```

## Overriding

To override a method from a parent class we have to use the `@Override` notation and same: access modifier, return type, name. To access the parent method we can use `super`.

```java
@Override
public String getDetails() {
	return super.getDetails() + ", departament: " + this.departament;
}
```

## Instanceof

The java `instanceof` operator is used to test whether the object is an instance of the specified type (class, subclass or interface).

```java
if(referenceParentClass instanceof ParentClass) {
	System.out.println("Is ParentClass type");
}
```

## Access to Child Methods using Object Conversion

If the we are using a parent class instance, we can access to child class methods by making a conversion from the parent class object to a child class object.

```java
((ChildClass) InstanceParentClass).childClassMethod();
```

## Abstract Classes

Are restricted classes that cannot be used to create objects (to access it, it must be inherited from another class). The methods can only be used in an abstract class, and it does not have a body (when are abstract definied). The body is provided by the subclass (inherited from).

```java
public abstract class AbstractClassName {
	protected String attributeName;

	protected ClassName(String attributeName) {
		this.attributeName = attributeName;
	}

	public abstrac void abstractMethodName();

	/* Getters, setters and toString*/
}
```

Once created the abstract class we need to implement it to create Objects.

```java
public class ClassName extends AbstractClassName {
	public ClassName(String attributeName) {
		super(attributeName);
	}

	@Override
	public void abstractMethodName() {
		System.out.println("Type: " + this.getClass.getSimpleName());
	}
}
```

## Interface

We used the interafaces when the relation between classes is given by its behaviour. The attributes are constants (`public`, `static` and `final`). 