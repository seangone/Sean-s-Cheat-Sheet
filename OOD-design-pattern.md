<extoc></extoc>

# Design Pattern

## Singleton

[Java Singleton Design Pattern Practices Examples](https://www.geeksforgeeks.org/java-singleton-design-pattern-practices-examples/)

**Motivation**

- Ensure a class has **only one instance** and **provide a global access point** to that instance.

**Eager initialization**

- simple to implement
- always create the instance whether it is required or not
- exception handling is not possible

```java
public class Singleton {
    private _static_ final Singleton INSTANCE = new Singleton();
    _private_ Singleton() {}
    
    _public static_ Singleton getInstance(){
        return INSTANCE;
    }
}
```

**Thread safe/lazy initialization Singleton**

- lazy initialization and thread safe
- getInstance() method is synchronized so it causes slow performance as multiple threads can’t access it simultaneously.
- improvement: change critcal section limited to create the instance.

```java
public class Singleton {
    private static final Singleton instance;
    private Singleton() {}
    synchronized public static Singleton getInstance() {
        if (instance == null) {
            instance == new Singleton();
        }
        return instance;
    }
}
```




## Builder Pattern

**Motivation**

- **reduce the number of constructors**
- **control the exposure of limited data while having multiple options to initialize an instance**
    - Data can be accessed when initializing but not after.
- ensure when an instance is completedly initialized semantically
- Use: ```User user = new User.UserBuilder("San", "Zhang")
.age(25)
.phone("1234567890")
.address("Fake Address")
.build()```

```java
public class User {
    private final String firstName; // required
    private final String lastName; // required
    private int age;
    private String phone;
    private String address;
}

private User(UserBuilder builder){
    this.firstName = builder.firstName;
    this.lastName = builder.lastName;
    this.age = builder.age;
    this.phone = builder.phone;
    this.address = builder.address;
}

public static class UserBuilder {
    private final String firstName; // required
    private final String lastName; // required
    private int age = 0;
    private String phone = "";
    private String address = null;
    public UserBuilder(String firstName, String lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    
    public UserBuilder age(int age){
        this.age = age;
        return this;
    }
    public UserBuilder phone(String phone){
        this.phone = phone;
        return this;
    }
    public UserBuilder address(String address){
        this.address = address;
        return this;
    }
    public User build(){
        return new User(this);
    }
}

public static void main(String[] args){
    User user = new User.UserBuilder("San", "Zhang")
    .age(25)
    .phone("1234567890")
    .address("Fake Address")
    .build()
}

```


## Factory Pattern

**Motivation**

- Create objects **without specifying the exact class** of object that will be created. Separate instance/object creation logic from its usage
    - eg. We want lots of `Shape`s. Some of them can be `Rectangle`s. Some of them can be `Circle`s. We want to create those from its `Name`s.

**Note**

- Create lots of Shapes, including `Rectangle`, `Triangle` and `Circle` using the names or other properties.
- Do not need to know about the constructor detail.

## Abstract Factory

**Motivation**

- Provides a way to encapsulate a group of individual factories that have a common theme without specifying the concrete classes.

**Note**

- abstract class `ControllerFactory` defines the way to create classes like `Button`, `InputBox` and other controllers.
- `IOSControllerFactory`, `AndroidControllerFactory` extends the abstract factory `ControllerFactory`.

