# Entity

It is a Java class that typically corresponds to a table in the relational database and is used to interact with the underlying database using JPA (Java Persistence API) annotations.

Entities in Spring JPA are POJOs (Plain Old Java Objects) that contain fields to represent the data columns in the database table. These fields are annotated with JPA annotations to define the mapping between the entity and the table.

## Creation

You have to define the entities inside the `entity` package.

After the class declaration you have to add the decorators:
- `@Entity`
- `@Table(name = "table_name")`

After the attribute declaration inside the class we use the `@Column(name = "colum_name")` decorator to link that attribute to the `column` of the database. If the attribute name doesn't change in the attribute class definition you don't have to use the `@Column` decorator.

To indicate that we are linking an attribute to the database's table primary key we use:

- `@Id`
- `@GeneratedValue(strategy = GenerationType.IDENTITY)`: this indicates that the database is responsible to auto generate the primary key
- `@Column(name = column_name)`


## Creation When Has More Than One Primary Key

Create a class which contains the primary keys as normal attributes.

```java
@Getter  
@Setter  
@NoArgsConstructor  
@AllArgsConstructor  
public class OrderItemId implements Serializable {  
	private Integer idOrder;  
	private Integer idItem;  
	  
	@Override  
	public boolean equals(Object o) {  
		if (this == o) return true;  
		if (!(o instanceof OrderItemId that)) return false;  
		return Objects.equals(idOrder, that.idOrder) && Objects.equals(idItem, that.idItem);  
	}  
	  
	@Override  
	public int hashCode() {  
		return Objects.hash(idOrder, idItem);  
	}  
}
```

Then to reference the primary keys we have to use the annotation `@IdClass(ClassName.class)`. Declare and annotate the attributes with the `@Id` annotation.

```java
@Entity  
@Table(name = "order_item")  
@IdClass(OrderItemId.class)  
@Getter  
@Setter  
@NoArgsConstructor  
public class OrderItemEntity {  
	@Id  
	@Column(name = "id_order", nullable = false)  
	private Integer idOrder;  
	  
	@Id  
	@Column(name = "id_item", nullable = false)  
	private Integer idItem;  
	  
	@Column(name = "id_pizza", nullable = false)  
	private Integer idPizza;  
	  
	@Column(nullable = false, columnDefinition = "Decimal(2,1)")  
	private Double quantity;  
	  
	@Column(nullable = false, columnDefinition = "Decimal(5,2)")  
	private Double price;  
	  
	@ManyToOne  
	@JoinColumn(name = "id_order", referencedColumnName = "id_order", insertable = false, updatable = false)  
	private OrderEntity order;  
	  
	@OneToOne  
	@JoinColumn(name = "id_pizza", referencedColumnName = "id_pizza", insertable = false, updatable = false)  
	private PizzaEntity pizza;  
}
```


## Join Column

Is used in combination with `@OneToOne` or `@ManyToOne` to create _entities_ associations, can be with foreign keys.

In the _Entity_ that has the _Foreign key_ from the database's table establish the relation with the annotations last exposed and use the `@JoinColumn(name = "primary_key")` annotation passing as parameter the column name that contains the _Primary key_, last define a method to store this relation. In the reference _Entity_ use the inverse annotation and pass as parameter of the `mappedBy` attribute the attribute that stores the _Foreign key_ (JoinColumn).


## Useful Parameters of the `@Column` Annotation

1. If our table's column has an specific length (`VARCHAR(50)`) we can pass the length by using `length` as parameter
2. When declaring `NOT NULL` columns in our table we can specify this in our entity by using `nullable = false`.
3. To declare in an _Entity_ that the value of an specific column cannot repeat we can use the `unique = true` parameter.
4. To declare Boolean, Float or Date columns in the entity we have to use the `columnDefnition` parameter. For Boolean values is: `columnDefnition = TINYINT`, for Float values is `columnDefinition = DECIMAL(5, 2)` and for Date values is `columnDefnition = DATETIME`.
5. To avoid a column to be updated and inserted we use use the attributes: `insertable = false` or `updatable = false`.
