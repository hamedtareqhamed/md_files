# Selection and Iteration Statements in UniTask

## 1. Selection Statements

In the **UniTask** application, selection statements are the main way to choose between two or more execution paths.

#### Two-Way Selectors

The application uses two-way selectors with the `if-else` general form.

* **Control Expression:**
  According to Dart static semantics, the control expression must be Boolean. It is written inside parentheses and decides whether the *then* clause or the *else* clause is executed.

* **Clause Form:**
  Compound statements enclosed in braces `{ }` are used. This allows more than one statement to be controlled by a single selector.

* **Design Issue (Nested Selectors):**
  For complex logic, UniTask follows the rule that an `else` matches the nearest previous `if`. Explicit braces are used to remove ambiguity and solve the *dangling else* problem.

#### UniTask Source Code Example (Input Validation)

```dart
// The boolean control expression checks if input is empty
if (taskController.text.isEmpty) {
  // Then clause: A compound statement to show an error
  showSnackBar("Error: Title is required");
} else {
  // Else clause: A compound statement to process the data
  saveTask(taskController.text);
}
```

---

## 2. Multiple-Way Selection

When UniTask must select one path from several possible options (such as task priority or category), it uses multiple-way selection statements.

* **Form and Type:**
  The `switch` statement is used, where the control expression decides which selectable segment will execute.

* **Execution Restriction:**
  Execution is limited to one selectable segment only.

* **Unconditional Branches:**
  The `break` statement is used to prevent *fall-through*. This ensures the program exits the `switch` statement immediately after the matching case. 

#### UniTask Source Code Example (Task Priority Color Handling)

```dart
// The control expression evaluates the task's priority string
switch (taskPriority) {
  case 'High':
    priorityColor = Colors.red; // Selectable segment
    break; // Unconditional branch to restrict execution
  case 'Medium':
    priorityColor = Colors.orange;
    break;
  default:
    priorityColor = Colors.grey; // Handles unrepresented expression values
}
```

---

## 3. Iterative Statements

Iteration in UniTask allows repeated execution of statements.

#### Iteration Based on Data Structures

Because UniTask manages collections of tasks, iteration is mainly based on data structures.

* **Control Mechanism:**
  The loop is controlled by the number of elements in the task list.

* **Iterator Function:**
  An iterator function such as `.map()` is used to process each element in the collection.

* **Design Issue (Counter-Controlled Loops):**
  When a standard `for` loop is used, the control expression is evaluated during each iteration. This ensures the loop reflects the current state of the data structure.

#### UniTask Source Code Example (Rendering Task List)

```dart
// Iteration controlled by the 'tasks' data structure
Column(
  children: tasks.map((task) {
    // The iterator function processes each element to return a widget
    return TaskItem(data: task);
  }).toList(), // Loop ends when no elements remain
)
```

---

## 4. User-Located Loop Control Mechanisms

UniTask uses loop control mechanisms that allow control from inside the loop body.

* **Unconditional Unlabeled Exits (`break`):**
  The `break` statement is used to exit a loop immediately.

* **Unlabeled Control Statements (`continue`):**
  The `continue` statement skips the rest of the current iteration and returns control to the loop condition.

#### UniTask Source Code Example (Task Search Logic)

```dart
// Searching for a specific Task ID in a list
for (var task in allTasks) {
  if (task.id == searchId) {
    foundTask = task;
    break; // Exit loop once the task is found
  }

  if (task.isArchived) {
    continue; // Skip archived tasks
  }

  // Logic for processing active tasks...
}
```
