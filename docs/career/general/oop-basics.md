---
date:
  created: 2023-11-14
  updated: 2023-11-28

description: >
  Introduction to the basic of object-orient programming characteristics.

tags:
    - OOP

comments: true
---
# Object-Oriented Programming Introduction

## What is OOP?

Object-oriented concept basically wants to make the programming easier by abstracting the *code* to material-world like. Therefore, the developer can easily build large functioning software with strong reference.

## Class and Object

**Class** is the fundation in OOP. It defines the boundaries for data and operations of an abstract concept. For example, a class named `Cat` should contain data of `color`, `genre`, `weight`, `age` and operations of `eat()`, `drink()`, `play()` and `poop()`.

**Object** is the instance of **Class**. One may create many objects of the same class. Just like you feed multiple *cats* in your home and those cats can live with different `color` and `age`. Those data and operations can be stored and opeared independently.

## Main Concepts

### Encapsulation

**Encapsulation** means the objects can hide its data and the detail of its opeartion implementation and only provide *interface* for others to access. This feature ensures the safety that no others can change the behavior of some object. Also, in my opinion, it makes the developer easier to use because you don't bother to understand *how* it works but only *what* it can do.

### Inheritance

**Inheritance** is to extends the original class to add or to adjust more features that previously defined. For example, `Cat` can be inherited from class `Animal` which has `numberOfLegs()` opeation. Also, `Cat` may add new `play()` for not every animals would play with humane. Overall, **inheritance** makes the relationship of classes clearer and let developer to mapping more complicated classes without duplicated code.

### Polymorphism

**Polymorphism** basically implies that the methods of same name provide by some class can have different behaviors. **Polymorphism** can be furthur divided into **Overloading** and **Overriding**.

**Overloading** means that the methods of same name can accepted different inputs whatever the number of the types. For example, you can let `Cat` `eat(DryFood)` or `eat(Can)` and the result might be sad and happy. 

**Overriding** means that the method inherited from its parent class can be changed. For example, `Animal` have `numberOfLegs()` return 2 by default, but `Cat` can redefined this method to return 4.

## Conclusion

OOP is an idea that every developer faces everyday, but few can explain to others intuitively. After writing this article, I feel like knowing this basic concept more. Hope this is also helpful for you. :)