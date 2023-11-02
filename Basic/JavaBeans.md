# JavaBeans

It has to have an empty constructor, each attribute has to be private and has to implement its respective getter and setter method, and implement an the Serializable interface. 

```java
public class Persona implements Serializable {
	private String nombre;
	private Strinf apellido;

	public Persona() { }

	public Persona(String nombre, String apellido) {
		this.nombre = nombre;
		this.apellido = apellido;
	}

	public String getNombre() {
		return this.nombre;
	}

	public String getApellido() {
		return this.apellido;
	}

	public void setNombre(String nombre) {
		this.nombre = nombre;
	}

	public void setApellido(String apellido) {
		this.apellido = apellido;
	}
}
```

We don't use the JavaBean constructor instead we use the `set` methods to initialize the class values and to retrieve the values we use the implemented `get` methods.