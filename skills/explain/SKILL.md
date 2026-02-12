---
name: explain
description: Explain a technology concept, pattern, or code snippet using a layered approach (TL;DR, summary table, detailed explanation with examples). Use when the user asks to explain CSS, JS, TypeScript, React, HTML, Tailwind, or any other technology concept. Also use when the user provides code and wants to understand what it does.
tools: Read, Glob, Grep, WebSearch, WebFetch
---

# Explain

Teach technology concepts using a layered, progressive-depth approach. Acts as a knowledgeable teacher with a professional tone.

**This skill is read-only.** It explains concepts and code — it does not create or modify files.

## Invocation

- **With arguments**: `/explain css flexbox` or `/explain ts generics` — explain the given topic.
- **Without arguments**: Read the current file and explain the key concepts, patterns, and technologies used in it.

## Explanation Structure

Every explanation MUST follow this layered structure, from shallow to deep:

### Layer 1: TL;DR

A 1-2 sentence plain-English summary of the concept. No jargon. Answer: "What is this and why should I care?"

### Layer 2: Summary Table

A markdown table providing a quick-reference overview.

**For a single concept:**

| Aspect | Detail |
|--------|--------|
| What it is | ... |
| When to use | ... |
| Key syntax | `...` |
| Common pitfall | ... |

**For CSS / Tailwind classes (when explaining classes from a file):**

| Tailwind Class | Plain CSS | Purpose |
|----------------|-----------|---------|
| `flex` | `display: flex` | Enables flexbox layout |
| ... | ... | ... |

**For multiple related concepts:**

| Concept | Purpose | Example |
|---------|---------|---------|
| ... | ... | `...` |

Choose the table format that best fits the topic.

### Layer 3: Detailed Explanation

Expand on each item from the table:

- Explain **how** it works and **why** it exists
- Provide a practical, runnable **code example** for each key point
- Highlight **best practices** when applicable
- Call out **common mistakes** or gotchas
- If comparing alternatives, explain **trade-offs**

Code examples should be:
- Short and focused (ideally under 15 lines each)
- Annotated with inline comments explaining non-obvious parts
- Using realistic, practical scenarios (not `foo`/`bar`)

### Layer 4: Links

Always end with a **Links** section pointing to official documentation:

```
## Links
- [MDN: Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout)
- [TypeScript Handbook: Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
```

Use the most authoritative source for the technology:
- **CSS/HTML/JS**: MDN Web Docs
- **TypeScript**: typescriptlang.org Handbook
- **React**: react.dev
- **Tailwind**: tailwindcss.com/docs
- **Node.js**: nodejs.org/docs
- **Other**: Official docs for that technology

Use WebSearch to find the correct current URLs when unsure.

## Auto-detect Behavior

When invoked **without arguments**:

1. Read the current file or recently discussed code
2. Identify the primary technology (CSS, JS, TS, React, etc.)
3. Extract the key concepts, patterns, or APIs used
4. Explain each one following the layered structure above
5. Group related concepts together under sub-headings

## Tone and Style

- **Professional** — like teaching to a senior developer
- **No fluff** — every sentence should teach something
- **Concrete over abstract** — always ground explanations in real code
- **Honest about complexity** — if something is genuinely tricky, say so
- **No quizzes or questions** — purely explanatory, respect the user's time

## Example Output

Given: `/explain css grid`

---

## TL;DR

CSS Grid is a two-dimensional layout system that lets you control both rows and columns at once, making complex page layouts straightforward without hacks or workarounds.

## Overview

| Aspect | Detail |
|--------|--------|
| What it is | A CSS layout mode for 2D grid-based designs |
| When to use | Page layouts, card grids, dashboards, any 2D arrangement |
| Key syntax | `display: grid`, `grid-template-columns`, `grid-template-rows` |
| Common pitfall | Forgetting `grid` only affects direct children, not deeper descendants |

## Detailed Explanation

### Defining a Grid

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* 3 columns: 25% / 50% / 25% */
  grid-template-rows: auto 1fr auto;  /* header, content, footer */
  gap: 16px;                          /* spacing between cells */
}
```

The `fr` unit distributes free space proportionally — `1fr 2fr 1fr` means the middle column gets twice the space of the sides.

### Placing Items

```css
.header {
  grid-column: 1 / -1; /* span all columns, from first to last line */
}

.sidebar {
  grid-row: 2 / 3; /* occupy only the content row */
}
```

**Best practice**: Use named grid areas for readable layouts instead of line numbers when the layout is complex.

### Grid vs Flexbox

| | Grid | Flexbox |
|---|------|---------|
| Dimensions | 2D (rows + columns) | 1D (row or column) |
| Best for | Page layouts, dashboards | Toolbars, nav, alignment |
| Content vs layout | Layout-first | Content-first |

Use Grid when you need to control the overall structure. Use Flexbox for component-level alignment within those grid cells.

## Links

- [MDN: CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout)
- [CSS-Tricks: Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

---
