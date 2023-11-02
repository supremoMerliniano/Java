# JDBC

To install the use the `JDBC` is necessary that you install the dependecy for the _database_ that you are going to use. I'm focusing in the `mysql connector`.

## Connection

The first step is to create a `Conexion` class to connect us to the db. This class contains the `getConenction` method wich returns an `Connection` object. As well, we have to define the methods to _close_ the connections by using polimorphism. 

As a note: every method that we are using in this class throws an `SQLException`, so we can report it with the _clauss_ `throws` or wrap or code in a `try-catch` statement. As example we have the follow code:


```java
package datos;

import java.sql.*;

public class Conexion {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/test?useSSL=false&useTimezone=true&serverTimezone=UTC&allowPublicKeyRetrieval=true";
    private static final String JDBC_USR = "root";
    private static final String JDB_PASSWORD = "0202993180a+";
    
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(JDBC_URL, JDBC_USR, JDB_PASSWORD);
    }
    
    public static void close(ResultSet rs) throws SQLException {
        rs.close();
    }
    
    public static void close(Statement stmnt) throws SQLException {
        stmnt.close();
    }
    
    public static void close(PreparedStatement stmnt) throws SQLException {
        stmnt.close();
    }
    
    public static void close(Connection conn) throws SQLException {
        conn.close();
    }
}
```

## DTO

To transfer data between the DB and our application we are using the DTO (Data Transfer Object) design pattern. Which are objects that carry data between processes in order to reduce the number of methods calls.

In the following example I have definied an `PersonaDTO`  which is the one in charge to transfer the data between the `persona` _SQL_ table and our application:


```java
package domain;

public class Persona {
    private int idPersona;
    private String nombre;
    private String apellido;
    private String email;
    private String telefono;
    
    public Persona() { }

    public Persona(int idPersona) {
        this.idPersona = idPersona;
    }
    
    public Persona(String nombre, String apellido, String email,
                    String telefono) {
        this.nombre = nombre;
        this.apellido = apellido;
        this.email = email;
        this.telefono = telefono;
    }
    
    public Persona(int idPersona, String nombre, String apellido, String email,
                    String telefono) {
        this.idPersona = idPersona;
        this.nombre = nombre;
        this.apellido = apellido;
        this.email = email;
        this.telefono = telefono;
    }

    public int getIdPersona() {
        return idPersona;
    }

    public void setIdPersona(int idPersona) {
        this.idPersona = idPersona;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getApellido() {
        return apellido;
    }

    public void setApellido(String apellido) {
        this.apellido = apellido;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getTelefono() {
        return telefono;
    }

    public void setTelefono(String telefono) {
        this.telefono = telefono;
    }

    @Override
    public String toString() {
        return "Persona{" + "idPersona=" + idPersona + ", nombre=" + nombre + 
                ", apellido=" + apellido + ", email=" + email + ", telefono=" + 
                telefono + '}';
    }
}
```

## DAO

It's a design pattern where a class takes in charge of the data persistence operations on a table of a database.

For every method we have to define the variables of `connetion`, and `PreparedStatement`. In certain methods we have to define a `ResultSet` variable for store data recieved from the database.

The main steps are: 

1. Define `Connection` and  `PreparedStatement` variables and initializes them with null.
2. Use a `try-catch-finally` statement to report the SQLExeption that our methods could throw if we have a problem.
3. Inside the `try-catch-finally` statement initialize the `Conenction` variable using the `getConnection()` method from our `Conexion` class.
4. Next we have to use the pass the _SQL query string_  as a parameter to the method `prepareStatement()` from the `Connection` instance and store it on the `PreparedStatement` instance.
5. Close the `connections` inside the `finally` block.

### List

To list the data from a DB we can use a method which returns a `List<>` from the type of the DTO. We have to define a:
1. `ResultSet` instance to store the data recieved from the DB. 
2. An instance of the DTO class.
3. A `List<>` of DTO class type.

Once we have defined all of that. We can use `executeQuery()` method of `PreparedStatement` instance and store it in the `ResultSet` type variable. After that we can iterate usinf a `while` loop trough the `ResultSet` type variable by using the `next()` method which returns `false` when the cursor positionates before the last row. In the iteration we initalizes the `DTO` instance by calling it's coinstructor an passing as arguments the retrieved data, we pass as parmeter the column db nameto the `getString()` or `getInt()` method from `ResultSet` instance. And we use the `add()` method to append the `DTO` instance to our `List<>`.

In the `finally` block we have to close the `ResultSet`, `PreparedStatement` and `Connection` instances.

```java
private static final String SQL_SELECT = "SELECT id_persona, nombre, apellido, email, telefono FROM persona";

public List<PersonaDTO> select() {
        Connection conn = null;
        PreparedStatement stmt = null;
        ResultSet rs = null;
        PersonaDTO persona = null;
        List<PersonaDTO> personas = new ArrayList<PersonaDTO>();

        try {
            conn = Conexion.getConnection();
            stmt = conn.prepareStatement(SQL_SELECT);
            rs = stmt.executeQuery();
            while (rs.next()) {
                int id_persona = rs.getInt("id_persona");
                String nombre = rs.getString("nombre");
                String apellido = rs.getString("apellido");
                String email = rs.getString("email");
                String telefono = rs.getString("telefono");

                persona = new PersonaDTO();
                persona.setId_persona(id_persona);
                persona.setNombre(nombre);
                persona.setApellido(apellido);
                persona.setEmail(email);
                persona.setTelefono(telefono);

                personas.add(persona);
            }
        } catch(SQLException ex) {
            ex.printStackTrace(System.out);
        } finally {
            Conexion.close(rs);
            Conexion.close(stmt);
            Conexion.close(conn);
        }

        return personas;
    }
```


## UPDATE

In the _SQL query string_ we have to set the values as `?` in order to pass them as arguments.

Create a method that recieves as argument the `DTO` instance and returns an `int`. In the method use pass as argument the `get` methods from the `DTO` and the `column` table name to the `setString()` or `setInt()` methods from the `Statement` instance. Later use the `executeUpdate()` method from the `Statement` instance.

```java
private static final String SQL_UPDATE = "UPDATE persona SET nombre=?, apellido=?, email=?, telefono=? WHERE id_persona = ?";

public int update(PersonaDTO persona) {
        Connection conn = null;
        PreparedStatement stmt = null;
        int rows = 0;

        try {
            conn = Conexion.getConnection();

            System.out.println("ejecutando query: " + SQL_UPDATE);

            stmt = conn.prepareStatement(SQL_UPDATE);
            stmt.setString(1, persona.getNombre());
            stmt.setString(2, persona.getApellido());
            stmt.setString(3, persona.getEmail());
            stmt.setString(4, persona.getTelefono());
            stmt.setInt(5, persona.getId_persona());

            rows = stmt.executeUpdate();

            System.out.println("Registros actualizado:" + rows);

        } catch(SQLException ex) {
            ex.printStackTrace(System.out);
        } finally {
            Conexion.close(stmt);
            Conexion.close(conn);
        }

        return rows;
}
```

## Delete

In the _SQL query string_ we have to set the values as `?` in order to pass them as arguments.

Create a method that recieves as argument the `DTO` instance and returns an `int`. In the method use pass as argument the `getId()` method from the `DTO` instance and the `column` table name to the `setInt()` method from the `Statement` instance. Later use the `executeUpdate()` method from the `Statement` instance.

```java
public int delete(PersonaDTO persona) {
        Connection conn = null;
        PreparedStatement stmt = null;
        int rows = 0;

        try {
            conn = Conexion.getConnection();

            System.out.println("Ejecutando query:" + SQL_DELETE);

            stmt = conn.prepareStatement(SQL_DELETE);
            stmt.setInt(1, persona.getId_persona());

            rows = stmt.executeUpdate();

            System.out.println("Registros eliminados:" + rows);
        } catch(SQLException ex) {
            ex.printStackTrace(System.out);
        } finally {
            Conexion.close(stmt);
            Conexion.close(conn);
        }
}
```

## Insert

In the _SQL query string_ we have to set the values as `?` in order to pass them as arguments.

Create a method that recieves as argument the `DTO` instance and returns an `int`. In the method use pass as argument the `get` methods from the `DTO` and the `column` table name to the `setString()` or `setInt()` methods from the `Statement` instance. Later use the `executeUpdate()` method from the `Statement` instance.


```java
public int insert(PersonaDTO persona) throws SQLException {
        Connection conn = null;
        PreparedStatement stmt = null;
        int rows = 0;
        try {
            conn = Conexion.getConnection();
            stmt = conn.prepareStatement(SQL_INSERT);
            stmt.setString(1, persona.getNombre());
            stmt.setString(2, persona.getApellido());
            stmt.setString(3, persona.getEmail());
            stmt.setString(4, persona.getTelefono());

            System.out.println("ejecutando query:" + SQL_INSERT);
            rows = stmt.executeUpdate();
            System.out.println("Registros afectados:" + rows);
        } catch(SQLException ex) {
            ex.printStackTrace();
        } finally {
            Conexion.close(stmt);
            Conexion.close(conn);
        }

        return rows;
}

```