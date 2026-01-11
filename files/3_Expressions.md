## Topic 2.2: Expressions and Assignment Statements

### A. Introduction

Expressions are the basic way to describe computations in a programming language. To understand expressions, we must know how operators and operands are evaluated and in what order. In imperative languages, assignment statements are very important because they change the program state.

### B. Arithmetic Expressions

Arithmetic expressions are made of operators, operands, parentheses, and function calls.

#### 1. Operator Classification

* **Unary operators**: Work on one operand, for example `-a`.
* **Binary operators**: Work on two operands, for example `a + b`.
* **Ternary operators**: Work on three operands, for example `a > b ? a : b`.

#### 2. Design Issues

* **Operator precedence**: Decides which operator is evaluated first. For example, multiplication is done before addition.
* **Operator associativity**: Decides the order when operators have the same precedence. Most operators are evaluated left to right, but exponentiation is often right to left.
* **Operand evaluation order**: Defines how variables, constants, and function calls are evaluated.

#### 3. Conditional Expressions (Ternary Operator)

In C-based languages, the ternary operator has this form:

`expression_1 ? expression_2 : expression_3`

If `expression_1` is true, the result is `expression_2`. Otherwise, the result is `expression_3`.

### C. Overloaded Operators

Overloaded operators are operators that have more than one meaning. For example, the `+` operator can add integers or floating-point numbers. In C++, the `&` operator can mean bitwise AND or address-of. Overloading can make code easier to read, but it can also cause confusion if used badly.

### D. Type Conversions

* **Narrowing conversion**: Converts a value to a smaller type that cannot hold all original values, such as converting `float` to `int`.
* **Widening conversion**: Converts a value to a larger type that can hold all original values, such as converting `int` to `float`.
* **Coercion**: An automatic type conversion done by the compiler. It can hide type errors.
* **Casting**: An explicit type conversion written by the programmer, for example `(int)angle` in C.

### E. Side Effects and Referential Transparency

A side effect happens when a function changes a variable outside its local scope, such as a parameter or a global variable. Referential transparency means that an expression can be replaced by its value without changing the program result. This makes programs easier to understand. Pure functional languages have this property because they do not use variables.

### F. Relational and Boolean Expressions

Relational operators compare values and return a Boolean result, such as `==`, `!=`, `>`, and `<`.

Short-circuit evaluation means that not all parts of a Boolean expression are evaluated. For example, in `(a > b) && (b++ / 3)`, if `(a > b)` is false, the second part is not evaluated.

### G. Assignment Statements

The general form of an assignment statement is:

`<target_var> <assign_operator> <expression>`

* **Compound assignment**: Short forms like `a += b`.
* **Unary assignment**: Increment and decrement operators (`++`, `--`).

  * `sum = ++count`: `count` is increased first, then assigned to `sum`.
  * `sum = count++`: `count` is assigned first, then increased.
* **Assignment as an expression**: In C-based languages, assignments return a value and can be used inside expressions, for example `while ((ch = getchar()) != EOF)`.
* **Multiple assignment**: Supported in languages like Perl and Ruby, for example `(first, second) = (20, 30)`.
* **Mixed-mode assignment**: Assigning values of different numeric types. Java and C# only allow widening conversions, such as `int` to `float`.
