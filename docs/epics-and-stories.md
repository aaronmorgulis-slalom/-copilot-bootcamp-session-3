# Epics and Stories (MVP + Post-MVP)

## MVP

- Epic: Task Data Model Updates (Frontend)
  - Story: Add optional due date field to task model
  - Story: Add priority field to task model with default P3
  - Story: Handle invalid due date values as absent

- Epic: Task Create/Edit UX
  - Story: Add due date input to task form
  - Story: Add priority selector to task form
  - Story: Preserve existing task completion toggle behavior

- Epic: Task Views and Filters
  - Story: Add All/Today/Overdue view tabs
  - Story: Show completed and incomplete tasks in All view
  - Story: Show incomplete tasks only in Today view
  - Story: Show incomplete tasks only in Overdue view

- Epic: Local-Only Persistence
  - Story: Persist due date and priority in local storage
  - Story: Confirm no backend changes are required for MVP

## Post-MVP

- Epic: Overdue Visual Treatment
  - Story: Visually highlight overdue tasks in task list

- Epic: Task Sorting
  - Story: Sort overdue tasks ahead of non-overdue tasks
  - Story: Sort tasks by priority (P1 then P2 then P3)
  - Story: Sort tasks by due date ascending within priority
  - Story: Place tasks without due dates at the end
