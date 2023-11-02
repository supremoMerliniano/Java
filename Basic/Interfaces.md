# Interfaces

They don't have a constructor. The methods are abstract (doesn't have an implementation). The attributes are constants (public, static and final) and the methods are public and abstract. By definition the first letter of the Interface name has to be an I.

We use them when the relation between classes is for behaviour.


```java
public interface IAccessoDatos {
	int MAX_REGISTROS = 10;

	void insertar();
	void listar();
	void actualizar();
	void eliminar();
}
```

We can't create objects. We call implementation to the classes that uses the `interface` and use the `implements` keyword to explicitly define the implementation. We have to implements all the method from the interface and use the `@Override` annotation.

```java
public class ImplementacionMySQL implements IAccessoDatos {
	@Override
	public void insertar() {
		System.out.println("Insertar desde MySQL");
	}

	@Override
	public void insertar() {
		System.out.println("Insertar desde MySQL");
	}

	@Override
	public void insertar() {
		System.out.println("Insertar desde MySQL");
	}

	@Override
	public void insertar() {
		System.out.println("Insertar desde MySQL");
	}
}
```

In a `main` method we call the class `interface` implementation.

```java
public class TestInterfaces {
	public static void Main(String[] args) {
		IAccessoDatos datos = new ImplementacionMySQL();

		imprimir(datos);

	}

	public static void imprimir(IAccessoDatos datos) {
		datos.listar();
	}
}
```
