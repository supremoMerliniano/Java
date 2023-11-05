# Collections API

## Collection

Is a framework that provides an architecture to store and manipulate the group of objects.

### List

The elements inside a list are `Objects`. Can have duplicate values. The elements in a list follows the order of aggregation.

**Definition:**

```java
List listName = new ArrayList();
```

**Adding elements:**

```java
listName.add(element);
```

### Set

Doesn't follow the aggregation order. It's faster than a list. Doesn't allow us to store duplicate elements

**Definition:**

```java
Set setName = new HashSet();
```

**Adding elements:***

```java
setName.add(element);
```

### Linked Hash Set

Follows the aggregation order. Doesn't allow to store duplicate elements.

```java
LinkedHashSet<Generic> setName = new LinkedHashSet<Generics>();
```

**Adding elements:***

```java
setName.add(element);
```

## Map

**Definition:**

```java
Map mapName = new HashMap();
```

**Adding elements:**

```java
mapName.put(key, value)
```

**Get Elements:** Returns an object, so you must cast it to the type of the variable in which we will store it.

```java
(Type) mapName.get(key);
```

**Get all keys**: Is useful to iterate over the `Map`. Returns a `Set` (so it doesn't follow an specific order).

```java
mapName.keySet();
```

**Get all values:**

```java
mapName.values();
```
