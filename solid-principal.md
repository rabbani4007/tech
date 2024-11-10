
# SOLID Principal 
The SOLID principles are a set of design guidelines that help developers create more maintainable and scalable software. Each letter in SOLID stands for a principle: **Single Responsibility**, **Open/Closed**, **Liskov Substitution**, **Interface Segregation**, and **Dependency Inversion**. Let’s look at each principle with a C# code example.



## 1. **Single Responsibility Principle (SRP)**
A class should have only one reason to change, meaning it should have only one job or responsibility.

```csharp
// Bad Example
public class InvoiceService
{
    public void GenerateInvoice() { /* Generates Invoice */ }
    public void PrintInvoice() { /* Prints Invoice */ }
    public void SendInvoiceEmail() { /* Sends Invoice via Email */ }
}

// Good Example
public class InvoiceGenerator
{
    public void GenerateInvoice() { /* Generates Invoice */ }
}

public class InvoicePrinter
{
    public void PrintInvoice() { /* Prints Invoice */ }
}

public class InvoiceEmailSender
{
    public void SendInvoiceEmail() { /* Sends Invoice via Email */ }
}

```
In the good example, each class has a single responsibility, making the code easier to maintain and modify.

## 2. **Open/Closed Principle (OCP)**
A class should be open for extension but closed for modification. This means you should be able to add new functionality to a class without modifying its existing code.

```csharp
// Bad Example
public class DiscountCalculator
{
    public double CalculateDiscount(string customerType, double amount)
    {
        if (customerType == "Regular")
            return amount * 0.1;
        else if (customerType == "VIP")
            return amount * 0.2;
        return 0;
    }
}

// Good Example (Using Inheritance)
public abstract class Discount
{
    public abstract double Calculate(double amount);
}

public class RegularCustomerDiscount : Discount
{
    public override double Calculate(double amount) => amount * 0.1;
}

public class VIPCustomerDiscount : Discount
{
    public override double Calculate(double amount) => amount * 0.2;
}

public class DiscountCalculator
{
    public double CalculateDiscount(Discount discount, double amount) => discount.Calculate(amount);
}

```
In the good example, adding a new discount type only requires creating a new subclass of `Discount` without modifying existing code.

## 3. **Liskov Substitution Principle (LSP)**
Derived classes should be substitutable for their base classes without affecting the correctness of the program. This means that subclasses should behave in a way consistent with the expectations set by their base classes.

```csharp
// Bad Example
public class Bird
{
    public virtual void Fly() { /* Birds can fly */ }
}

public class Ostrich : Bird
{
    public override void Fly()
    {
        throw new NotImplementedException("Ostriches can't fly!");
    }
}

// Good Example
public abstract class Bird
{
    // General properties and methods for birds
}

public class FlyingBird : Bird
{
    public void Fly() { /* Implementation for flying */ }
}

public class Ostrich : Bird
{
    // Ostrich-specific implementation, but no Fly method
}
```
In the good example, `Ostrich` does not inherit the `Fly` method, following LSP by not breaking expectations.

## 4. **Interface Segregation Principle (ISP)**
Clients should not be forced to implement interfaces they don’t use. Instead of one large interface, create smaller, more specific interfaces.

```csharp
// Bad Example
public interface IWorker
{
    void Work();
    void Eat();
}

public class Robot : IWorker
{
    public void Work() { /* Robot works */ }
    public void Eat() { throw new NotImplementedException(); } // Robots don't eat
}

// Good Example
public interface IWorker
{
    void Work();
}

public interface IEater
{
    void Eat();
}

public class HumanWorker : IWorker, IEater
{
    public void Work() { /* Human works */ }
    public void Eat() { /* Human eats */ }
}

public class Robot : IWorker
{
    public void Work() { /* Robot works */ }
}

```
In the good example, interfaces are split so that each implementing class only uses what it needs.

## 5. **Dependency Inversion Principle (DIP)**
High-level modules should not depend on low-level modules. Both should depend on abstractions, and abstractions should not depend on details.

```csharp
// Bad Example
public class EmailService
{
    public void SendEmail(string message) { /* Sends an email */ }
}

public class Notification
{
    private EmailService _emailService = new EmailService();
    
    public void Notify(string message)
    {
        _emailService.SendEmail(message);
    }
}

// Good Example
public interface IMessageService
{
    void SendMessage(string message);
}

public class EmailService : IMessageService
{
    public void SendMessage(string message) { /* Sends an email */ }
}

public class SMSService : IMessageService
{
    public void SendMessage(string message) { /* Sends an SMS */ }
}

public class Notification
{
    private readonly IMessageService _messageService;
    
    public Notification(IMessageService messageService)
    {
        _messageService = messageService;
    }
    
    public void Notify(string message)
    {
        _messageService.SendMessage(message);
    }
}

```
In the good example, `Notification` depends on the abstraction `IMessageService`, which allows for easy substitution of different message services without changing the `Notification` class itself.

These principles lead to more modular, flexible, and testable code. Following SOLID can help you avoid common pitfalls in object-oriented design.

