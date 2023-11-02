# Maven

lol

## Dependency Installation

To install dependencies you have to first open the _pom.xml_ file. In the _pom.xml_ you have to add the `<dependencies></dependencies>`, inside this tags you have to insert the `<dependency></dependency>` that you need. You can search it on the maven repository. Example:

```xml
 <dependencies>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.17</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.commons/commons-dbcp2 -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-dbcp2</artifactId>
            <version>2.9.0</version>
        </dependency>
    </dependencies
>```

In order to install all the _dependencies_ , you have to `Clean and build` the project again