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

## Conclusion

Encapsulation bundles data and methods together into a single class.
Data hiding restricts access to the object state and class implementation details.
Encapsulation and data hiding are techniques that make a Java class reusable and adaptive to change.


