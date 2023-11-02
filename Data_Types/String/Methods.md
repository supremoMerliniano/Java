# Methods of String

The most useful String methods.

## ReplaceAll

Returns a string replacing all the sequence of characters matching regex and replacement string.

```java
String.replaceAll(String regex, String replacement)  
```

Example:

```java
public class ReplaceAllExample1{  
	public static void main(String args[]){  
		String s1="javatpoint is a very good website";  
		String replaceString=s1.replaceAll("a","e");//replaces all occurrences of "a" to "e"  
		System.out.println(replaceString);  
	}
}
```