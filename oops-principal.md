# C# Object-Oriented Programming (OOP) Principles

Object-Oriented Programming (OOP) is a programming paradigm centered around the concept of objects and classes. In C#, OOP principles help in organizing code and creating modular and reusable applications. The four main OOP principles are **Encapsulation**, **Inheritance**, **Polymorphism**, and **Abstraction**.

---

## 1. Encapsulation

Encapsulation is the principle of bundling data (properties) and methods that operate on that data within a single unit or class. It also involves restricting direct access to some components to maintain control over the data.

### Example

```csharp
public class BankAccount
{
    // Private field
    private decimal _balance;

    // Public property to access balance safely
    public decimal Balance
    {
        get { return _balance; }
    }

    // Public method to deposit money
    public void Deposit(decimal amount)
    {
        if (amount > 0)
            _balance += amount;
    }

    // Public method to withdraw money with validation
    public void Withdraw(decimal amount)
    {
        if (amount > 0 && amount <= _balance)
            _balance -= amount;
    }
}
```
In this example, _balance is private and only accessible through the Deposit and Withdraw methods, providing a controlled interface to manage the account's balance.

## 2. Inheritance

Inheritance allows a class to inherit the properties and methods of another class, promoting code reusability. In C#, a class can inherit from another class using a colon (:) followed by the base class name.

### Example

```csharp
// Base class
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Animal is eating");
    }
}

// Derived class
public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Dog is barking");
    }
}

// Usage
Dog dog = new Dog();
dog.Eat();  // Inherited method
dog.Bark(); // Method of Dog class

```
Here, the Dog class inherits from the Animal class, reusing the Eat method without duplicating code.

## 3. Polymorphism

Polymorphism allows methods to do different things based on the object they are acting on. In C#, polymorphism is typically achieved through method overriding or method overloading.

### Example: Method Overriding

```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("Animal sound");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Woof");
    }
}

public class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Meow");
    }
}

// Usage
Animal myDog = new Dog();
Animal myCat = new Cat();

myDog.Speak(); // Output: Woof
myCat.Speak(); // Output: Meow


```
In this example, Speak is overridden in the Dog and Cat classes, allowing the same method name to produce different outputs depending on the object.

## 4. Abstraction

Abstraction involves creating a simplified representation of complex systems by exposing only essential details and hiding implementation. Abstract classes and interfaces in C# are used to implement abstraction.

### Example: Method Overriding

```csharp
public abstract class Shape
{
    // Abstract method (no implementation here)
    public abstract double GetArea();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public Circle(double radius)
    {
        Radius = radius;
    }

    // Implementing the abstract method
    public override double GetArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public Rectangle(double width, double height)
    {
        Width = width;
        Height = height;
    }

    // Implementing the abstract method
    public override double GetArea()
    {
        return Width * Height;
    }
}

// Usage
Shape circle = new Circle(5);
Shape rectangle = new Rectangle(4, 6);

Console.WriteLine(circle.GetArea());    // Output: Area of the circle
Console.WriteLine(rectangle.GetArea()); // Output: Area of the rectangle


```
Here, the abstract Shape class defines a blueprint for other shapes. Circle and Rectangle classes inherit from Shape and provide specific implementations for the GetArea method.


## Summary

The four principles of OOP in C# are:

 1. **Encapsulation**: Protects data by exposing only necessary parts through a public interface.
 2. **Inheritance**: Allows reusability of code by inheriting properties and methods from a base class.
 3. **Polymorphism**: Allows methods to perform different functions based on the object that calls them.
 4. **Abstraction**: Simplifies complex systems by defining essential properties and hiding details.

These principles help create structured, efficient, and modular code in C#.