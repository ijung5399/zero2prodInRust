# Example
```
trait Speak {
    fn speak(&self) -> String;
}

struct Dog;
struct Cat;

impl Speak for Dog {
    fn speak(&self) -> String {
        "Woof!".to_string()
    }
}

impl Speak for Cat {
    fn speak(&self) -> String {
        "Meow!".to_string()
    }
}

fn make_it_speak<T: Speak>(animal: T) {
    println!("{}", animal.speak());
}
```

# `Trait` of Rust vs. `Interface` of C#
Let's compare **Rust's `trait`** and **C#'s `interface`** side by side to understand their similarities and differences.

---

## 🔶 Similarities

| Feature | Rust `trait` | C# `interface` |
|--------|---------------|----------------|
| **Purpose** | Defines shared behavior | Defines shared behavior |
| **Implementation** | Types must implement the trait | Classes/structs must implement the interface |
| **Polymorphism** | Enables static and dynamic dispatch | Enables polymorphism via inheritance |
| **No Fields** | Traits can't have fields | Interfaces can't have fields (until C# 8.0) |
| **Multiple Implementations** | A type can implement multiple traits | A class can implement multiple interfaces |

---

## 🔷 Key Differences

| Feature | Rust `trait` | C# `interface` |
|--------|---------------|----------------|
| **Default Methods** | ✅ Yes (since the beginning) | ✅ Yes (since C# 8.0) |
| **Associated Types** | ✅ Yes (via `type`) | ❌ No (use generics instead) |
| **Generics Integration** | Deeply integrated with generics and trait bounds | Uses generics, but less tightly coupled |
| **Dynamic Dispatch** | Via `dyn Trait` | Via interface references |
| **Static Dispatch** | ✅ Yes (monomorphization) | ❌ No (always dynamic) |
| **Orphan Rule** | ✅ Yes (you can’t implement external traits for external types) | ❌ No such restriction |
| **Trait Objects** | `Box<dyn Trait>` for dynamic dispatch | Interface references (`IFoo foo = new Bar();`) |
| **Implementation for Primitives** | ✅ Yes (e.g., implement trait for `i32`) | ❌ No (can't implement interfaces for built-in types) |

---

## 🧪 Example Comparison

### Rust

```rust
trait Drawable {
    fn draw(&self);
}

struct Circle;

impl Drawable for Circle {
    fn draw(&self) {
        println!("Drawing a circle");
    }
}
```

### C#

```csharp
interface IDrawable {
    void Draw();
}

class Circle : IDrawable {
    public void Draw() {
        Console.WriteLine("Drawing a circle");
    }
}
```

---

## 🧠 Summary

- **Rust traits** are more powerful and flexible, especially with **associated types**, **default methods**, and **static dispatch**.
- **C# interfaces** are simpler and more familiar to developers from OOP backgrounds, but have gained more power with recent versions (like default implementations in C# 8.0).

Would you like to see how **trait bounds** in Rust compare to **generic constraints** in C# next?

# About `Dynamic Dispatch`

**Dynamic dispatch** is a concept in programming where the method that gets called is **determined at runtime**, rather than at compile time. It's a key part of **polymorphism**, allowing different types to be treated uniformly through a common interface or trait.

---

## 🧠 In Simple Terms

Imagine you have a function that takes something that "can speak." You don’t care *what* it is — a dog, a cat, or a robot — as long as it knows how to speak. With **dynamic dispatch**, the program figures out *at runtime* which `speak()` method to call based on the actual type of the object.

---

## 🔧 In Rust

Rust uses **`dyn Trait`** to enable dynamic dispatch:

```rust
trait Speak {
    fn speak(&self);
}

struct Dog;
struct Cat;

impl Speak for Dog {
    fn speak(&self) {
        println!("Woof!");
    }
}

impl Speak for Cat {
    fn speak(&self) {
        println!("Meow!");
    }
}

fn make_it_speak(animal: &dyn Speak) {
    animal.speak(); // Dynamic dispatch happens here
}
```

Here, `&dyn Speak` is a **trait object**, and Rust uses a **vtable** (virtual method table) behind the scenes to call the correct method at runtime.

---

## 🔄 Dynamic vs Static Dispatch

| Feature | Dynamic Dispatch (`dyn Trait`) | Static Dispatch (`impl Trait` or generics) |
|--------|-------------------------------|-------------------------------------------|
| **When resolved** | Runtime | Compile time |
| **Performance** | Slightly slower (indirection) | Faster (inlined, monomorphized) |
| **Flexibility** | More flexible (heterogeneous types) | Less flexible (homogeneous types) |
| **Use case** | When type is unknown at compile time | When type is known and performance matters |

---

## 🧪 In C#

C# uses dynamic dispatch by default with interfaces:

```csharp
interface ISpeak {
    void Speak();
}

class Dog : ISpeak {
    public void Speak() => Console.WriteLine("Woof!");
}

void MakeItSpeak(ISpeak animal) {
    animal.Speak(); // Dynamic dispatch
}
```
