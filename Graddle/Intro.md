# Introduction

lel

## Install dependencies

To install dependencies is necessary that you add them to the `build.gradle` file in the `dependencies` section by using their respective keyword. You can search the string implementation in the **Maven Respository**.

**Meaning of the short graddle dependency declaration**

The parts of the dependency declaration are separated by the `:` character. They are _group_, _name_ and _version_.

```groovy
dependencies {
	implementation 'group:name:version'
}
```

## Implementation

The dependency is required for both compilation and runtime of your application. It indicates that the dependency is an integral part of your project's code and will be used during the development and execution phases.

```groovy
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa:3.1.1'
}
```

## RuntimeOnly

The dependency is required for the execution of your application but is not needed for compiling or building the project.

```groovy
dependencies {
	runtimeOnly 'org.postgresql:postgresql:42.6.0'
}
```
