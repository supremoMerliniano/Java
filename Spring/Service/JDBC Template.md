Let us execute SQL raw queries.


## Creating an SQL Query

Inside our [Service](./Service) class we declare an `JdbcTemplate` variable. Later we define a method that it's return type is an _Entity_. To execute the _SQL query_ we have to use the `query` method and pass it the _SQL query_ and a `BeanPropertyRowMapper<>`.

```java
@Service  
public class PizzaService {  
    private final JdbcTemplate jdbcTemplate;  
  
    @Autowired  
    public PizzaService(JdbcTemplate jdbcTemplate) {  
        this.jdbcTemplate = jdbcTemplate;  
    }  
  
    public List<PizzaEntity > getAll() {  
        return this.jdbcTemplate.query("SELECT * FROM pizza;", new BeanPropertyRowMapper<>(PizzaEntity.class));  
    }  
}
```