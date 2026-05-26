---
name: frontend-ui-engineering
description: Builds production-quality UIs in the GTDing project. Enforces robust React 19 patterns, Ant Design 6 tokens, and fights against cheap AI visual aesthetics.
version: 1.0.0
---

# Frontend UI Engineering

## Overview
This skill establishes high-fidelity standards for designing and implementing frontend components for the `gtding` project. It aims for a visually stunning, polished, and premium user experience that feels handcrafted by a professional engineer — avoiding all default "AI-generated" templates.

---

## When to Use
Apply this skill when:
- Creating new UI components, forms, layout grids, or pages in the project.
- Modifying existing React components or adjusting CSS styles.
- Integrating Ant Design 6 theme components or adjusting typography and spacing.
- Optimizing interface state management or adding smooth transitions/micro-animations.

**When NOT to Use:**
- Writing core backend integrations, database scripts, or pure dev tooling scripts.
- Refactoring unit test suites without touching UI files.

---

## Core Principles

### 1. The "No Modals" Absolute Guardrail
- **Rule**: Every screen, card editor, details pane, or configuration form MUST be implemented as a separate route using `React Router DOM 7`. 
- **Action**: Never write `<Modal>` popups. Instead, redirect to `/tasks/new`, `/tasks/:id/edit`, etc. Keep history navigable!

### 2. Fight the "AI Aesthetic"
AI-generated interfaces look identical and cheap. Follow these strict counters to maintain a premium feel:
- **Project Color Tokens**: Avoid heavy purple/indigo default templates. Use harmonized Ant Design 6 color palettes and neutral, high-end dark/light modes.
- **Subtle Gradients**: Use flat solids or very subtle, smooth HSL-tailored gradients instead of harsh, high-contrast visual noise.
- **Corner Radii Consistency**: Rely on the defined Ant Design 6 theme border-radii. Avoid rounding everything with extreme values (like generic `rounded-2xl`).
- **Realistic Placeholder Copy**: Never use `Lorem Ipsum` or generic "Task 1", "Task 2". Use realistic task descriptions matching a GTD app (e.g., *"Подготовить презентацию для Олега"*, *"Купить молоко"*, *"Написать тесты для TaskStore"*).

---

## Component Architecture Patterns

### 1. Prefer Composition over Configuration
Avoid massive components with dozens of layout configuration props. Use children composition:

```tsx
// Good: Composable, readable, and highly maintainable
<Card>
  <CardHeader>
    <CardTitle>Текущие задачи</CardTitle>
  </CardHeader>
  <CardBody>
    <TaskList tasks={tasks} />
  </CardBody>
</Card>

// Avoid: Over-configured, rigid component
<Card
  title="Текущие задачи"
  headerSize="large"
  bodyPadding="md"
  bodyContent={<TaskList tasks={tasks} />}
/>
```

### 2. Separate Data Fetching from Presentation
Isolate data fetching or global state hooks from the layout render components (Container vs. Presentation):

```tsx
// Container: handles Zustand state & hooks
export function TaskListContainer() {
  const { tasks, isLoading } = useTaskStore();

  if (isLoading) return <TaskListSkeleton />;
  if (tasks.length === 0) return <EmptyState message="Все задачи выполнены!" />;

  return <TaskList tasks={tasks} />;
}

// Presentation: handles rendering and styles
export function TaskList({ tasks }: { tasks: Task[] }) {
  return (
    <ul role="list" className="divide-y divide-gray-100">
      {tasks.map(task => <TaskItem key={task.id} task={task} />)}
    </ul>
  );
}
```

---

## State Management Decision Matrix
Always choose the simplest state container that fits:
1. **Local State (`useState`)**: For transient UI state (toggles, input focus, local button hover states).
2. **URL Search Parameters (`searchParams`)**: For filters, pagination, or query searches (keeps views easily shareable and bookmarkable).
3. **Global Store (`Zustand + Immer`)**: For app-wide entity state (tasks, active projects, user contexts). Keep state modifications immutable with Immer helper actions.
