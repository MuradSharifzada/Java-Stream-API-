- [1. What is a Functional Interface?](#1-what-is-a-functional-interface)
- [2. You might be wondered...](#2-you-might-be-wondered)
- [3. Built-in Functional Interfaces](#3-built-in-functional-interfaces)
- [4. Custom Functional Interfaces](#4-custom-functional-interfaces)

## 1. What is a Functional Interface?

A **functional interface** is an interface with exactly one abstract method. This single abstract method defines the contract for the function, which can then be represented using a lambda expression or method reference.
Lambdas and method references in Java 8 are only possible because of functional interfaces. They act as the “target type” for these functional programming features.

---
## You might be wondered...

- **Why does Java need functional interfaces?**  
  They allow lambdas and method references to be used anywhere a single-method interface is expected. This brings functional programming to Java’s type system.
- **What happens if you add a second abstract method?**  
  The interface is no longer “functional” and cannot be used as a lambda target.
- **Can a functional interface have default/static methods?**  
  Yes! As long as there’s only one abstract method, default and static methods are allowed.
---

  **Example:**  
```java
@FunctionalInterface
public interface StringTransformer {
    String transform(String input);
}
```
The @FunctionalInterface annotation is optional but recommended. By placing this annotation on the class, you can avoid confusion and prevent yourself and others from accidentally adding a second abstract method.
## 3. Built-in Functional Interfaces
Java 8 provides many useful functional interfaces in the `java.util.function` package. Some of the most common:
| Interface      | Abstract Method         | Description                                     |
|----------------|------------------------|--------------------------------------------------|
| `Predicate<T>` | `boolean test(T t)`    | Tests a condition on an argument                 |
| `Function<T,R>`| `R apply(T t)`         | Transforms an argument into another value        |
| `Consumer<T>`  | `void accept(T t)`     | Performs an action on the argument               |
| `Supplier<T>`  | `T get()`              | Supplies a value, no input                       |
| `UnaryOperator<T>` | `T apply(T t)`     | Same input and output type, a specialization     |
| `BinaryOperator<T>`|`T apply(T,T)`      | Two inputs, one output, all same type            |

## 4. Custom Functional Interfaces
Processing a list of employees, each with a salary, and allowing customizable operations (like calculating bonuses, applying raises, or filtering).


**Example:**  
```java
@FunctionalInterface
public interface SalaryAdjuster {
    double adjust(double currentSalary);
}
```

**Usage with lambda and real data:**
```java
import java.util.*;

class Employee {
    String name;
    double salary;

    Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }
}

public class SalaryDemo {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Employee("Rufat", 50000),
            new Employee("Aqshin", 60000)
        );

        SalaryAdjuster raise = salary -> salary * 1.10;

        for (Employee e : employees) {
            double newSalary = raise.adjust(e.salary);
            System.out.println(e.name + "'s new salary: " + newSalary);
        }
    }
}
```
