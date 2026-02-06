# Epics and Stories (MVP + Post-MVP)

This document breaks down the PRD into epics and stories with acceptance criteria and technical requirements.

## MVP

### Epic: Task Data Model Updates (Frontend)

#### Story: Add optional due date field to task model

##### Acceptance Criteria

- Tasks can have an optional due date.
- Due dates are stored as an ISO date string in the format `YYYY-MM-DD`.
- Tasks without a due date continue to behave normally.

##### Technical Requirements

- Extend the in-memory task object shape to include `dueDate`.
- Represent the due date in local state and persistence as a `YYYY-MM-DD` string.

#### Story: Add priority field to task model with default P3

##### Acceptance Criteria

- Tasks include a `priority` field.
- Allowed values are `P1`, `P2`, and `P3`.
- New tasks created without an explicit priority default to `P3`.

##### Technical Requirements

- Extend the in-memory task object shape to include `priority`.
- Enforce the allowed priority values at the boundaries (UI input and/or state updates).

#### Story: Handle invalid due date values as absent

##### Acceptance Criteria

- If a due date value is invalid, the task is treated as having no due date.
- Invalid due dates do not break list rendering or filtering.

##### Technical Requirements

- Validate due date strings before using them in filters or comparisons.
- When loading persisted tasks, coerce invalid `dueDate` values to undefined/absent.

#### Story: Default missing priority to P3 for existing tasks

##### Acceptance Criteria

- Existing tasks missing a priority are treated as `P3`.
- Existing tasks continue to load without errors.

##### Technical Requirements

- When loading persisted tasks, set `priority: 'P3'` if missing.

#### Story: Ensure priority values are limited to P1/P2/P3

##### Acceptance Criteria

- Tasks cannot end up with a priority outside of `P1`, `P2`, `P3`.
- If an invalid priority is encountered, it is treated as `P3`.

##### Technical Requirements

- Add a small validation/coercion step where tasks are created/loaded/updated.

### Epic: Task Create/Edit UX

#### Story: Add due date input to task form

##### Acceptance Criteria

- The task form includes a due date input.
- The due date input allows leaving the value blank.
- Saving a task with a due date stores it as `YYYY-MM-DD`.

##### Technical Requirements

- Add a form control bound to the task's `dueDate` value.
- Ensure the stored value is normalized to `YYYY-MM-DD`.

#### Story: Add priority selector to task form

##### Acceptance Criteria

- The task form includes a priority control with options `P1`, `P2`, `P3`.
- Creating a task without choosing a priority results in `P3`.

##### Technical Requirements

- Add a form control constrained to `P1 | P2 | P3`.
- Ensure task creation sets `priority` (defaulting to `P3`).

#### Story: Allow creating tasks without a due date

##### Acceptance Criteria

- Users can create tasks without selecting a due date.
- Tasks without due dates appear in the All view.

##### Technical Requirements

- Ensure task creation allows `dueDate` to be absent/undefined.

#### Story: Preserve existing task completion toggle behavior

##### Acceptance Criteria

- Users can mark tasks completed and incomplete as before.
- Completion state is unaffected by the new due date and priority fields.

##### Technical Requirements

- Do not change the meaning or storage of the completion status field.

### Epic: Task Views and Filters

#### Story: Add All/Today/Overdue view tabs

##### Acceptance Criteria

- The UI provides three views: All, Today, and Overdue.
- The user can switch between these views.

##### Technical Requirements

- Add a simple view state (e.g., `all | today | overdue`).
- Render a tab or button group for switching the view.

#### Story: Show completed and incomplete tasks in All view

##### Acceptance Criteria

- All view shows both completed and incomplete tasks.

##### Technical Requirements

- Implement All view filtering as "no filter" on completion status.

#### Story: Implement Today view to filter by due date equals today

##### Acceptance Criteria

- Today view shows incomplete tasks with a due date equal to today.
- Tasks without a due date do not appear in Today view.

##### Technical Requirements

- Compute today's date in `YYYY-MM-DD` and compare against task `dueDate`.
- Apply the completion filter (incomplete only) in this view.

#### Story: Implement Overdue view to filter by due date before today

##### Acceptance Criteria

- Overdue view shows incomplete tasks with a due date before today.
- Tasks without a due date do not appear in Overdue view.

##### Technical Requirements

- Compare task `dueDate` values against today's date using `YYYY-MM-DD` semantics.
- Apply the completion filter (incomplete only) in this view.

### Epic: Local-Only Persistence

#### Story: Persist due date and priority in local storage

##### Acceptance Criteria

- Due date and priority are saved and restored locally.
- Refreshing the page retains due date and priority.

##### Technical Requirements

- Update local persistence serialization/deserialization to include `dueDate` and `priority`.

#### Story: Handle older stored tasks missing due date and priority fields

##### Acceptance Criteria

- Tasks stored prior to this change still load successfully.
- Missing `priority` behaves as `P3`.
- Missing `dueDate` behaves as no due date.

##### Technical Requirements

- Add a small migration/coercion step during task load from local storage.

#### Story: Confirm no backend changes are required for MVP

##### Acceptance Criteria

- The MVP can be completed without modifying backend behavior.

##### Technical Requirements

- Keep changes limited to the frontend and local persistence.

## Post-MVP

### Epic: Overdue Visual Treatment

#### Story: Visually highlight overdue tasks in task list

##### Acceptance Criteria

- Overdue tasks are visually distinguishable in the list.

##### Technical Requirements

- Add a conditional style for tasks that are overdue.
- Reuse existing design primitives/components (no new design system).

### Epic: Task Sorting

#### Story: Sort overdue tasks ahead of non-overdue tasks

##### Acceptance Criteria

- When sorting is enabled, overdue tasks appear before non-overdue tasks.

##### Technical Requirements

- Implement a sort comparator that groups overdue tasks first.

#### Story: Sort tasks by priority (P1 then P2 then P3)

##### Acceptance Criteria

- Within the same overdue/non-overdue group, tasks are ordered by priority: P1, then P2, then P3.

##### Technical Requirements

- Define a stable priority rank mapping: P1 < P2 < P3.

#### Story: Sort tasks by due date ascending within priority

##### Acceptance Criteria

- Within the same group and priority, tasks with due dates are ordered soonest-to-latest.

##### Technical Requirements

- Compare `YYYY-MM-DD` due dates to sort ascending.

#### Story: Place tasks without due dates at the end

##### Acceptance Criteria

- Tasks without a due date appear after tasks with due dates when sorting.

##### Technical Requirements

- Ensure the comparator consistently ranks missing due dates after present due dates.
