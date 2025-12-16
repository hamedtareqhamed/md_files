# Topic 2 (Part 1): Names and Bindings in Dart
*Based on Lecture 06: Names, Bindings, and Scopes*

## 1. Introduction to Names (Design Issues)
According to **Lecture 06**, the primary design issues for names are **Case Sensitivity** and **Special Words**.

### A. Case Sensitivity
* **Concept:** Does the language distinguish between uppercase and lowercase letters?
* **In Dart:** Dart is **case-sensitive** (similar to C, C++, and Java).
    * *Example:* `Result`, `result`, and `RESULT` are three different variables.
    * **Significance:** This increases the number of available names but requires readability discipline from the programmer.

### B. Special Words (Reserved Words)
* **Concept:** Words that are used to make programs readable and name actions.
* **In Dart:** Dart has **Keywords** (Reserved Words) that generally cannot be used as identifiers.
    * *Examples:* `class`, `if`, `while`, `import`, `super`.
    * *Context:* Unlike some languages mentioned in the lecture where keywords can be redefined, Dart treats them as reserved to prevent ambiguity.

---

## 2. Variables and Their Attributes
Lecture 06 states that a variable is an abstraction of a memory cell characterized by **6 attributes**. Here is how Dart implements them:

1.  **Name:** The identifier string (e.g., `studentName`).
2.  **Address (L-value):** The memory location. In Dart (being an object-oriented language), variables store *references* to objects in the Heap memory.
3.  **Value (R-value):** The actual data stored (e.g., "Ali").
4.  **Type:** Dart is a **Statically Typed** language.
    * This determines the range of values and operations (e.g., you cannot multiply a `String` by a `bool`).
5.  **Lifetime:**
    * Local variables live as long as the function executes (Stack-dynamic).
    * Objects live until the Garbage Collector removes them (Heap-dynamic).
6.  **Scope:** The range where the variable is visible (discussed below).

---

## 3. The Concept of Binding
[cite_start]**Binding** is the association between an entity and an attribute[cite: 726].

### A. Binding Time
* **Language Design Time:** Meaning of operators (e.g., `+` means addition).
* **Compile Time (Static):** Binding of types in Dart.
    * *Explicit Declaration:* `int count = 10;`
    * *Type Inference:* `var count = 10;` (Dart infers it is an `int` at compile time).
* **Run Time (Dynamic):** Binding of values and non-static local variables.

### B. Static vs. Dynamic Type Binding
* **Dart is Statically Typed:** Most variables are bound to a type before execution. [cite_start]This matches the **Static Binding** concept in the lecture[cite: 750].
* **Exception (Dynamic Keyword):** Dart offers a `dynamic` type which delays type binding until runtime.
    * *Example:* `dynamic x = 10; x = "Hello";` (This is allowed but risky, similar to dynamic languages mentioned in the lecture).

---

## 4. Scope (Static Scoping)
[cite_start]Lecture 06 defines **Scope** as the range of statements over which a variable is visible[cite: 877].

### Static (Lexical) Scoping
* **Concept:** Scope is determined by the text of the program (nested blocks).
* **In Dart:** Dart uses **Static Scoping**.
    * Variables defined in a block `{ ... }` are only visible within that block and its nested blocks.
    * **Shadowing:** A local variable can "hide" a global variable with the same name.

### Code Example for Presentation:
```dart
String language = "Dart"; // Global Scope

void main() {
  String framework = "Flutter"; // Local to main
  
  if (true) {
    String type = "Mobile App"; // Nested Scope
    
    print(language);  // Accessible (Global)
    print(framework); // Accessible (Parent Scope)
    print(type);      // Accessible (Current Scope)
  }
  
  // print(type); // Error: 'type' is not defined in this scope.
}
