# Household Chore Management App — Functional Specification

## 1. Purpose

A simple tool for managing shared household chores between two adults, focused on:

1. Organization
2. Accountability
3. Motivation

## 2. Household

- Exactly one household per user.
- Household is a first-class entity.
- Exactly two adults.
- Adults use the fixed labels **Me** and **Partner**.
- Labels are fixed when the household is created.
- Both adults have identical permissions.
- Both adults can create, edit, and delete chores/tasks.
- Household name is simply **Household**.
- Household is created automatically on first launch.
- No onboarding flow.
- No authentication/account identity.
- Data restoration after reinstall/data loss is out of scope.

## 3. Persistence and Connectivity

- Persistent storage is required.
- Storage technology is intentionally unspecified.
- Internet connection is required.
- Offline operation and synchronization are out of scope.

## 4. Chores and Tasks

### 4.1 Recurring Chores

Recurring chores are the core feature.

- Each recurrence creates a concrete task instance for the current period.
- Frequency is weekly only.
- A recurring chore occurs on a specific weekday.
- Required fields:
  - Name
  - Frequency
  - Assignment/rotation
- Recurring chores can be fully edited, including frequency and assignment.
- Editing affects only future occurrences.
- A recurring chore can be reassigned for the current week's task only.
- Reassigning the current week's task does not affect future assignments.
- Changing the assignment resets the rotation from that point onward.
- Recurring chores can be archived.
- Archiving stops future occurrences.
- Archiving removes the current task from Today immediately.
- Archived chores are excluded from statistics.
- Historical task records remain immutable.
- Archiving requires confirmation.

### 4.2 One-Off Tasks

One-off tasks are supported.

Required fields:

- Name
- Specific date
- Assignee

Upcoming one-off tasks:

- Can be permanently deleted.
- Deletion requires confirmation.

## 5. Assignment and Rotation

Assignment uses a hybrid approach:

- Some chores are explicitly assigned.
- Others rotate automatically.

The rotation mechanism should remain deliberately simple for the homework project.

Only one rotation mechanism is required.

## 6. Task States

A task can have one of three states:

- `OPEN`
- `DONE`
- `SKIPPED`

### 6.1 Completion

- Either adult can complete any task.
- Completion records:
  - Who completed the task
  - When it was completed
- The original assignment remains unchanged.
- No confirmation is required.
- There is no undo.

### 6.2 Skipping

- Either adult can skip a task.
- A skip reason is optional.
- Skipped tasks disappear from Today immediately.
- Skipping is recorded.
- Skipping does not affect the next recurrence.
- No confirmation is required.
- There is no undo.

## 7. Today View

The main screen is **Today**.

It displays current tasks only.

### 7.1 Layout

Two sections:

- **Mine**
- **Partner's**

### 7.2 Task Visibility

- Open tasks are displayed.
- Completed tasks remain visible until tomorrow.
- Completed tasks appear in a separate **Done** section.
- The Done section is collapsed by default.
- Skipped tasks are not displayed.
- The assignee does not need to be displayed on individual tasks because of the Mine/Partner sections.

### 7.3 Ordering

- Tasks are ordered by due date.
- There is no defined secondary ordering for tasks with the same due date.
- Users cannot manually reorder tasks.

### 7.4 Available Actions

From Today, users can:

- Complete a task.
- Skip a task.
- Mark all of their own open tasks as done.

The bulk-completion action requires confirmation.

### 7.5 Search and Filtering

- No search.
- No filtering.

## 8. Reminders

- There is one daily reminder for unfinished tasks.
- Reminder text is generic:
  - "You have unfinished chores."
- The reminder time is fixed for the household.
- Either adult can change the reminder time.
- The reminder time can be changed directly from Today.
- A small settings button on Today provides access to the reminder-time setting.
- Reminders cannot be disabled.
- There are no task-specific due-time notifications.

## 9. Motivation

The application uses gentle nudges rather than gamification.

Requirements:

- Nudges should be encouraging.
- Each adult receives nudges only for their own unfinished tasks.
- Example:
  - "Almost there! 2 chores left today."
- No separate "helping partner" statistic is required.

## 10. Statistics

Statistics are accessible from Today.

### 10.1 Statistics Included

- Completion rate
- Individual workload share

### 10.2 Presentation

- Statistics include a simple summary and charts.
- Statistics cover the current week only.
- The week runs from Monday to Sunday.
- The current incomplete week is included.
- Current-week statistics are calculated up to today.
- Charts show weekly totals only.
- Day-by-day chart data is not required.
- Workload is based on raw task counts.
- No difficulty or weighting system is used.

### 10.3 Completion Rate

Completion rate is shown separately for each adult.

Rules:

- A task completed by its assignee counts as completed for that adult.
- A task completed by the other adult counts as **not completed** for the assignee.
- Skipped tasks count as not completed.
- Completion rate is therefore based on whether the assigned adult completed the task.

### 10.4 Workload

Two perspectives are shown separately:

1. Tasks assigned to each adult.
2. Tasks actually completed by each adult.

No separate "helping partner" statistic is required.

### 10.5 Historical Data

- There is no separate history view.
- Completed/skipped tasks are available only through statistics.
- Historical completed/skipped task records are immutable.

## 11. Settings

There is no separate settings screen.

A small settings control is available from Today.

It provides:

- Household reminder time

No other preferences are required.

## 12. Household Creation

On first launch:

1. The household is automatically created.
2. Both adults are created automatically.
3. No joining or invitation step is required.
4. The application starts directly on Today.

The household:

- Has the fixed name `Household`.
- Contains exactly two adults.
- Uses `Me` and `Partner` as fixed labels.

## 13. Errors

- Errors are presented using generic, user-friendly messages.
- Failed actions provide a **Retry** option.
- Automatic silent retry is not required.

## 14. Refresh Behavior

- Today automatically refreshes when the user enters or returns to the screen.
- There is no periodic refresh while Today remains open.

## 15. Historical Data Integrity

- Completed tasks cannot be modified.
- Skipped tasks cannot be modified.
- Historical task records are immutable.
- Editing a recurring chore never modifies past occurrences.
- Reassignment of a recurring chore for the current week does not modify historical assignments.

## 16. Explicitly Out of Scope

The following are explicitly out of scope:

- Authentication
- Account/login management
- Multiple households per user
- Offline operation
- Synchronization
- Data restoration after reinstall/data loss
- Data export
- Onboarding
- Custom household names
- Custom adult names
- Switching Me/Partner identities
- Children as participants
- Chore templates
- Search
- Filtering
- Manual task ordering
- Task-specific notifications
- Reminder disabling
- Notes/comments
- Separate history view
- Gamification
- Helping-partner statistic
- Difficulty/weighting for workload
- Detailed statistical periods
- Historical task editing
- Undoing completed tasks
- Undoing skipped tasks
