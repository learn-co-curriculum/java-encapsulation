# Encapsulation

## Learning Goals

- Review the concept of encapsulation

## Introduction

Encapsulation is one of the four pillars
in object-oriented programming. We've discussed the
concept in previous lessons about classes and objects.  In this
lesson, we'll review encapsulation before moving
on to the other pillars of inheritance, polymorphism, and abstraction.

## Encapsulation

**Encapsulation** is a technique of wrapping the data (variables)
and the code to access and modify the data (methods) together as a single unit
defined in a Java class.

![dog uml](https://curriculum-content.s3.amazonaws.com/6676/pillars/dog_uml.png)

The `Dog` class encapsulates the data about each dog
in the instance variables, and provides methods that model
the behavior of a dog to access and modify the data.

```java
public class Dog {
    private String name;
    private int weight;
    private boolean likesBaths;
    private boolean waggingTail;
    
    public Dog(String name, int weight, boolean likesBaths, boolean waggingTail) {
        this.name = name;
        this.weight = weight;
        this.likesBaths = likesBaths;
        this.waggingTail = waggingTail;
    }

    public void giveTreat() {
        waggingTail = true;
        weight++;
    }

    public void giveBath() {
        waggingTail = likesBaths;
    }

    @Override
    public String toString() {
        return "name='" + name + '\'' +
                ", weight=" + weight +
                ", likesBaths=" + likesBaths +
                ", waggingTail=" + waggingTail;
    }
}
```

**Data hiding** is a concept that is often
associated with encapsulation. Data hiding is important
when we develop applications that involve multiple classes.
Recall that an **access modifier** in Java
controls the visibility of a class, field, constructor, or method.
When an access modifier is not specified, the visibility defaults
to the `package` level.

| Modifier        | Class | Package  | Subclass In<br>Another Package  | World |
|-----------------|-------|----------|---------------------------------|-------|
| public          | Y     | Y        | Y                               | Y     | 
| protected       | Y     | Y        | Y                               | N     | 
| default/package | Y     | Y        | N                               | N     | 
| private         | Y     | N        | N                               | N     | 


In the UML `Dog` class diagram shown above,  member access is denoted using a symbol:

- `-` private member
- `+` public member
- `#` protected member
- `~` package/default member 

To follow standard practices of data hiding, we will declare instance variables
as `private`, and provide `public` methods to access and modify the variables.

- Instance variables `name`, `weight`, `likesBaths` and `tailWagging`
  are hidden from other classes by declaring them `private`.
- We provide `public` methods  such as `giveTreat()`, `giveBath()` and `toString()`
  to access and modify the values stored in the variables.

## Why do we hide instance variables?

One reason to hide instance variables is to protect object state
from unexpected or invalid modification by other classes.  Consider what would happen if
we add a public instance variable named `bark` to our `Dog` class:

```java
public class Dog {
    private String name;
    private int weight;
    private boolean likesBaths;
    private boolean waggingTail;
    public String bark = "Woof!";
    
    public Dog(String name, int weight, boolean likesBaths, boolean waggingTail) {
        this.name = name;
        this.weight = weight;
        this.likesBaths = likesBaths;
        this.waggingTail = waggingTail;
    }

    public void giveTreat() {
        waggingTail = true;
        weight++;
    }

    public void giveBath() {
        waggingTail = likesBaths;
    }

    @Override
    public String toString() {
        return "name='" + name + '\'' +
                ", weight=" + weight +
                ", likesBaths=" + likesBaths +
                ", waggingTail=" + waggingTail;
    }
}
```

Since `bark` is public, any class can modify the value.  We can create another
class that forces the dog to say "Meow!" instead of "Woof!"
when it barks.  This violates the model of a  `Dog` that the
class is trying to encapsulate.

```java
public class Main {
    public static void main(String[] args) {
        Dog fido = new Dog("fido", 30, true, false);
        snoopy.bark = "Meow!";
    }
}
```


Another reason to encapsulate instance variables is to facilitate change.
Suppose we have a `Person` class as shown:

```java
public class Person {
  private String name;
  private String street;
  private String city;
  private String state;

  public Person(String name, String street, String city, String state) {
    this.name = name;
    this.street = street;
    this.city = city;
    this.state = state;
  }

  public String getName() { return name; }

  public String getAddress() { return String.format("%s, %s, %s", street, city, state); }
}
```

The `Main` class creates a `Person` instance and call the public methods to print
the object state:

```java
public class Main {
  public static void main(String[] args) {
    Person p1 = new Person("Fred", "123 Main St", "Boston", "MA");
    System.out.println(p1.getName() + " lives at " + p1.getAddress());
  }
}
```

The output is:

```text
Fred lives at 123 Main St, Boston, MA
```

Now suppose we decide to create a new class named `Address` to encapsulate the `street`, `city`, and
`state`.  

```java
public class Address {
    private String street;
    private String city;
    private String state;

    public Address(String street, String city, String state) {
        this.street = street;
        this.city = city;
        this.state = state;
    }

    public String getStreet() {return street;}
    public String getCity() {return city;}
    public String getState() {return state;}
}
```

We can evolve the `Person` class to replace the 3 instance variables `street`, `city`, and `state`
with a single variable `address` that stores a reference to an `Address` object.
The public `getAddress` method calls  accessor methods to get the individual address fields.

```java
public class Person {
    private String name;
    private Address address; 

    public Person(String name, String street, String city, String state) {
        this.name = name;
        this.address = new Address(street, city, state);
    }

    public String getName() { return name; }

    public String getAddress() {
        return String.format("%s, %s, %s", address.getStreet(), address.getCity(), address.getState());
    }
}
```

The `Main` class does not need to change at all, since data hiding prevented
it from directly accessed the instance variables of the `Person` class.
The public interface of the `Person` class (i.e. methods `getName()` and `getAddress()`) remains the same,
even though the one of the method implementations changed.

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Fred", "123 Main St", "Boston", "MA");
        System.out.println(p1.getName() + " lives at " + p1.getAddress());
    }
}
```

The output is still:

```text
Fred lives at 123 Main St, Boston, MA
```

## Conclusion

Encapsulation bundles data and methods together into a single class.
Data hiding restricts access to the object state and class implementation details.
Encapsulation and data hiding are techniques that make a Java class reusable and adaptive to change.


