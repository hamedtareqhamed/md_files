### Subprograms in Dart (Lecture 9)

#### Function Definition
A Dart function consists of a header (return type, name, formal parameters) and a body (executable code).
Example from the project:
```dart
void addTask(String title) {
  setState(() {
    tasks.add(Task(title: title));
  });
}
```
- `void`: return type (Procedure – no value returned)
- `addTask`: function name
- `(String title)`: formal parameter list

#### Procedures vs. Functions
- **Procedures** do not return a value (`void`). Example: `addTask`.
- **Functions** return a value. Example:
  ```dart
  Widget build(BuildContext context) {
    return Scaffold(...);
  }
  ```
  Returns a `Widget`, so it is a Function.

#### Parameter Types
**1. Positional Parameters**
Bound by position. Order must match the definition.
```dart
String createMessage(String name, int age) {
  return "Hello $name, you are $age years old.";
}
// Call:
print(createMessage("Ali", 22)); // Position matters
```

**2. Named Parameters**
Enclosed in `{}`; order does not matter. A key feature of Dart.
```dart
void showSnackbar({
  required BuildContext context,
  required String message,
  Color? backgroundColor = Colors.blue,
}) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text(message), backgroundColor: backgroundColor),
  );
}
```
Call examples:
```dart
showSnackbar(context: context, message: "Task added!", backgroundColor: Colors.green);
// or
showSnackbar(message: "Done!", context: context);
```
This matches the **keyword parameters** concept in Lecture 9 (Slide 1-6).

#### Function Signature
Defined by:
- Number and types of parameters
- Parameter names (for named parameters)
- Return type

Example signature:
```dart
void deleteTask({required BuildContext context, required int index})
```

#### Parameter-Passing Methods
- **Primitive types** (`int`, `String`, etc.) are passed **by value**: changes inside the function do not affect the original.
  ```dart
  void changeValue(int x) { x = 100; }
  int a = 5;
  changeValue(a);
  print(a); // prints 5
  ```
- **Objects** are passed **by object reference**: internal state can be modified.
  ```dart
  void updateTask(Task task) { task.title = "Updated"; }
  Task t = Task(title: "Old");
  updateTask(t);
  print(t.title); // prints "Updated"
  ```
This aligns with Lecture 9’s explanation for Java/Python (Slide 1-26): “Object parameters are passed by reference.”

#### Project Examples (from GitHub: UniTask)
**`main()` – Entry Point**
```dart
void main() {
  runApp(const MyApp());
}
```
- Procedure (`void`)
- Automatically called at startup

**Custom Function with Callback**
```dart
void deleteTask({
  required BuildContext context,
  required int index,
  required VoidCallback onConfirm,
}) {
  showDialog(
    context: context,
    builder: (ctx) => AlertDialog(
      actions: [
        TextButton(onPressed: () { onConfirm(); Navigator.pop(ctx); }, child: Text("Delete")),
      ],
    ),
  );
}
```
- Uses named parameters
- Accepts a function (`onConfirm`) as a parameter → demonstrates
