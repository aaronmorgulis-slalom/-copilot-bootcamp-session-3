# Product Requirements Document (PRD) - Todo App Upgrade (Due Dates, Priorities, Filters)

## 1. Overview

We are upgrading the basic Todo app (currently: task title + completed status) to support due dates, priority levels, and simple date-based filters. The goal is to keep the MVP simple/teachable and frontend-only (no backend changes).

Clarifications / TBD (explicitly not decided in the artifacts as MVP vs Post-MVP):
- Priority visual treatment: the meeting discussed color-coded priority badges (P1 red, P2 orange, P3 gray), but Slack only confirmed the `priority` field for MVP.
- Overdue highlight specifics: Slack confirmed overdue highlighting as Post-MVP, but did not specify the exact styling (the meeting suggested highlighting overdue tasks in red).

---

## 2. MVP Scope

- Data model updates (frontend/local only)
  - Add `dueDate` to tasks
    - Optional
    - Stored as ISO date string: `YYYY-MM-DD`
    - If invalid, treat as absent/undefined (ignore invalid values)
  - Add `priority` to tasks
    - Enum: `P1 | P2 | P3`
    - Default: `P3`
- UI/UX
  - Add filters/tabs for task views:
    - **All**
    - **Today**
    - **Overdue**
  - Filter behavior
    - **All**: shows both incomplete and completed tasks
    - **Today** and **Overdue**: show incomplete tasks only
- Persistence / architecture
  - Keep storage local only
  - No backend changes and no external storage

---

## 3. Post-MVP Scope

- Visual treatment
  - Visually highlight overdue tasks
- Sorting
  - Implement sort order:
    - Overdue tasks first
    - Then by priority (`P1` → `P2` → `P3`)
    - Then by due date ascending
    - Tasks without a due date appear last

---

## 4. Out of Scope

- Notifications
- Recurring tasks
- Multi-user / collaboration
- Keyboard navigation / special accessibility features beyond standard defaults
- Backend work or any external storage beyond local persistence
