# Epics and Stories (MVP + Post-MVP)

## MVP

- Epic: Task Data Model Updates (Frontend)
  - Story: Add optional due date field to task model
  - Story: Add priority field to task model with default P3
  - Story: Handle invalid due date values as absent
  - Story: Default missing priority to P3 for existing tasks
  - Story: Treat missing due date as no due date
  - Story: Ensure priority values are limited to P1/P2/P3

- Epic: Task Create/Edit UX
  - Story: Add due date input to task form
  - Story: Add priority selector to task form
  - Story: Allow creating tasks without a due date
  - Story: Default priority to P3 when creating tasks
  - Story: Preserve existing task completion toggle behavior

- Epic: Task Views and Filters
  - Story: Add All/Today/Overdue view tabs
  - Story: Implement All view to show all tasks
  - Story: Show completed and incomplete tasks in All view
  - Story: Implement Today view to filter by due date equals today
  - Story: Implement Overdue view to filter by due date before today
  - Story: Show incomplete tasks only in Today view
  - Story: Show incomplete tasks only in Overdue view
  - Story: Exclude tasks without due dates from Today view
  - Story: Exclude tasks without due dates from Overdue view
  - Story: Preserve selected view when toggling task completion

- Epic: Local-Only Persistence
  - Story: Persist due date and priority in local storage
  - Story: Confirm no backend changes are required for MVP
  - Story: Load tasks from local storage with due date and priority fields
  - Story: Handle older stored tasks missing due date and priority fields

## Post-MVP

- Epic: Overdue Visual Treatment
  - Story: Visually highlight overdue tasks in task list
  - Story: Apply overdue highlight only in views that show overdue tasks

- Epic: Task Sorting
  - Story: Sort overdue tasks ahead of non-overdue tasks
  - Story: Sort tasks by priority (P1 then P2 then P3)
  - Story: Sort tasks by due date ascending within priority
  - Story: Place tasks without due dates at the end
  - Story: Apply sorting consistently across All/Today/Overdue views
