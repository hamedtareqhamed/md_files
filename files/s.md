# UniTask (Flutter/Dart) — Sample Application: System Features

**Repository:** https://github.com/hamedtareqhamed/UniTask  
**Language / Framework:** Dart + Flutter  
**Storage:** Local storage (offline persistence)

> **Rubric focus (excerpt):** “Find a sample application… Show the design of the system features with flowchart and description. Describe the output of each system feature…”  
> *(Screenshot for reference)*  
![Rubric excerpt](00_rubric_excerpt.png)

---

## System Feature 1 — App Startup & Data Initialization

![App startup & init](01_app_startup_init.png)

### Description (Flow)
1. App starts and shows a splash/loading screen.
2. App loads `savedData` from local storage.
3. If `savedData` exists: parse **Courses**, **Assessments**, **Deadlines**, and **DashboardStats**.
4. If `savedData` does not exist: initialize empty lists and default dashboard stats.
5. Build the Home UI with main tabs: **Courses**, **Calendar**, **Dashboard**.

### Output (What the user sees)
- Splash screen briefly appears.
- Then the Home screen loads.
- If there is saved data: the user sees their existing courses/assessments/deadlines and updated dashboard numbers.
- If no saved data: the user sees empty lists (no courses/tasks) and default dashboard widgets.

---

## System Feature 2 — Add Course (Courses Tab)

![Add course](02_add_course.png)

### Description (Flow)
1. User opens **Courses** tab and taps **Add Course**.
2. User enters:
   - `courseName`
   - `courseworkWeight`
   - `finalProjectWeight`
3. Validate:
   - `courseName` must not be empty.
   - `courseworkWeight + finalProjectWeight` must equal **100**.
4. If validation passes: save the course to local storage and refresh the Courses list.

### Output (What the user sees)
- If `courseName` is empty → error message “Course name required”.
- If weights don’t sum to 100 → error “Weights must sum to 100”.
- If valid → the new course appears in the Courses list (persisted after app restart).

---

## System Feature 3 — Add Assessment to a Course (Course Details)

![Add assessment](03_add_assessment.png)

### Description (Flow)
1. User opens a **Course Details** screen and taps **Add Assessment**.
2. User enters:
   - `assessmentTitle`
   - `maxScore`
   - `pointsWorth`
   - `scoreEarned`
   - `dueDate`
3. Validate:
   - `assessmentTitle` must not be empty.
   - `scoreEarned` must be ≤ `maxScore`.
4. If valid:
   - Save the assessment to the course.
   - Create & save a linked **deadline** to the calendar.
   - Update course stats:
     - `acquiredPoints += scoreEarned`
     - `lostPoints += (maxScore - scoreEarned)`
     - `remainingPoints = totalCoursePoints - acquiredPoints - lostPoints`
   - Update charts + save updated stats to local storage.

### Output (What the user sees)
- If title missing → error “Assessment title required”.
- If scoreEarned > maxScore → error “Score cannot exceed max score”.
- If valid → assessment shows in Course Details, calendar gets a due-date marker, and progress charts update immediately.

---

## System Feature 4 — Calendar Busy-Window Detection (Calendar Tab)

![Calendar busy window](04_calendar_busy_window.png)

### Description (Flow)
1. User opens **Calendar** tab.
2. App loads `deadlines` and the `semesterRange`.
3. For each day in semester range:
   - Define a 5-day window: `windowStart = day`, `windowEnd = day + 4`.
   - Count deadlines whose date is within the window.
   - If `count >= 5`, mark this window as a **Busy Window** (highlighted).
4. Render the calendar with urgency/busy-window highlights.

### Output (What the user sees)
- The calendar displays normal days plus highlighted “busy” periods where many deadlines are clustered (helps the user plan ahead).
- The highlight updates automatically based on the saved deadlines.

---

## System Feature 5 — Study Session Timer (Dashboard Tab)

![Study session](05_dashboard_study_session.png)

### Description (Flow)
1. User opens **Dashboard** and taps **Start Session**.
2. App sets `startTime = now`, `elapsed = 0`, `isRunning = true`.
3. While running:
   - Wait ~1 second (tick).
   - Update `elapsed = now - startTime`.
   - Display updated elapsed time.
4. If user taps **Pause**:
   - set `isRunning = false`
   - save partial `elapsed` to local storage
   - show “Paused”
5. If user taps **Stop**:
   - set `isRunning = false`
   - save `sessionSummary(elapsed)` to local storage
   - update dashboard stats
   - show “Session saved”
   - return to dashboard

### Output (What the user sees)
- A live timer counting up every second.
- On Pause → timer stops and “Paused” appears (elapsed is preserved).
- On Stop → confirmation “Session saved” and dashboard totals/summary update.

---

## System Feature 6 — Add Task via “Quick Action” (Dashboard)

![Add task quick action](06_add_task_quick_action.png)

### Description (Flow)
1. User opens **Dashboard** and taps **Quick Action**.
2. Chooses **Add Task**.
3. Enters:
   - `taskTitle` (required)
   - optional `taskNotes`
   - optional `dueDate`
4. Validate `taskTitle` is not empty.
5. Create `newTask(..., status="Pending")` and save to local storage.
6. Refresh dashboard widgets and task list.

### Output (What the user sees)
- If title missing → error “Task title required”.
- If valid → “Task added” confirmation, and the task appears in Tasks/Dashboard (saved for next app open).

---

## System Feature 7 — Toggle Task Completion + Progress Widget Update

![Toggle task completion](07_toggle_task_complete_progress.png)

### Description (Flow)
1. User opens **Dashboard** or **Tasks** list and selects a task.
2. User taps **Complete** toggle.
3. If task is currently Completed → set to Pending; else set to Completed.
4. Save updated task list to local storage.
5. Recalculate progress:
   - `completedCount = count(tasks where status == "Completed")`
   - `totalCount = count(all tasks)`
   - if `totalCount == 0` → `progressPercent = 0`
   - else `progressPercent = (completedCount / totalCount) * 100`
6. Update progress widget and refresh UI.

### Output (What the user sees)
- Task visually changes between Completed/Pending.
- The progress widget percentage (or bar/ring) updates immediately.
- The change persists after restart.

---

## System Feature 8 — Deadline Urgency Coloring + “Upcoming Deadlines” List

![Deadline urgency](08_deadline_urgency_upcoming_list.png)

### Description (Flow)
1. User opens **Calendar** or **Dashboard**.
2. App loads all deadlines and sorts them by nearest date.
3. For each deadline:
   - compute `daysLeft = deadline.date - today`
   - assign urgency color:
     - `daysLeft < 0` → **Overdue (Red)**
     - `daysLeft <= 2` → **Urgent (Orange/Red)**
     - `daysLeft <= 7` → **Soon (Yellow)**
     - else → **Normal (Green/Blue)**
4. Render:
   - calendar markers colored by urgency
   - dashboard “Upcoming Deadlines” list sorted by soonest first

### Output (What the user sees)
- Deadlines appear in the calendar with color markers based on urgency.
- A sorted Upcoming Deadlines list shows what’s due soonest.
- Overdue items are visually emphasized.

---

## System Feature 9 — Edit / Delete an Item (Course / Assessment / Task)

![Edit delete item](09_edit_delete_item.png)

### Description (Flow)
1. User opens an item details screen (Course / Assessment / Task) and taps **Edit** or **Delete**.
2. **Edit path**
   - show edit form with existing values
   - user updates fields
   - validate inputs
   - if invalid → show error
   - else → save updated item to local storage, refresh related screens, show “Updated”
3. **Delete path**
   - show confirmation “Are you sure?”
   - if user cancels → return to details screen
   - else:
     - remove item from local storage
     - if item has `linkedDeadline` → remove that deadline from deadlines list too
     - refresh related screens and show “Deleted”
     - return to list screen

### Output (What the user sees)
- Edit: updated values appear immediately, with a confirmation message.
- Delete: item disappears from lists; any linked calendar deadline also disappears; user sees “Deleted”.

---

## Quick checklist (to maximize marks)

- ✅ **Flowchart** shown for each major system feature (9 total).  
- ✅ Each feature includes:
  - **Description (Flow)**: step-by-step design explanation
  - **Output**: what the user sees / what changes in the UI + storage  
- ✅ Offline persistence is clearly mentioned wherever “save to localStorage” occurs.

  
