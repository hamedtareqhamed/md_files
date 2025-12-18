
# Topic 2.1: Names and Bindings in Dart

### A.Names properties
#### Case Sensitivity
* In Dart: Dart is case-sensitive.
    * Example: `Result`, `result`, and `RESULT` are three different variables.
    * Significance: This increases the number of available names but requires readability discipline from the programmer.

#### Special Words (Reserved Words)
* In Dart: Dart has Keywords (Reserved Words) that cannot be used as identifiers.
    * Examples: `class`, `if`, `while`, `import`, `super`.

Unlike some languages where keywords can be redefined, Dart treats them as reserved to prevent ambiguity.

---

### B. Variables and Their Attributes
variable is an abstraction of a memory cell characterized by 6 attributes. Here is how Dart implements them:

1.  **Name:** The identifier string (e.g., `studentName`).
2.  **Address:** The memory location. In Dart (being an object-oriented language), variables store *references* to objects in the Heap memory.
3.  **Value:** The actual data stored (e.g., "Yousef").
4.  **Type:** Dart is a Statically Typed language.
    * This determines the range of values and operations (e.g., you cannot multiply a `String` by a `bool`).
5.  **Lifetime:**
    * Local variables live as long as the function executes (Stack-dynamic).
    * Objects live until the Garbage Collector removes them (Heap-dynamic).
6.  **Scope:** The range of statements where the variable is visible. Dart uses lexical (static) scoping, so visibility depends on where it’s declared (block, function, class, library).

---

### C. The Concept of Binding
**Binding** is the association between an entity and an attribute.

#### Binding Time
* **Language Design Time:** Meaning of operators (e.g., `+` means addition).
* **Compile Time (Static):** Binding of types in Dart.
    * *Explicit Declaration:* `int count = 10;`
    * *Type Inference:* `var count = 10;` (Dart infers it is an `int` at compile time).
* **Run Time (Dynamic):** Binding of values and non-static local variables.
 * *Example:* `dynamic x = 10; x = "Hello";` 



   

---

### D. Scope (Static Scoping)
**Scope** is the range of statements over which a variable is visible.

#### Static Scoping
* **In Dart:** Dart uses Static Scoping.
    * Variables defined in a block `{ ... }` are only visible within that block and its nested blocks.
    * **Shadowing:** A local variable can "hide" a global variable with the same name.

#### Code Example:
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
```
