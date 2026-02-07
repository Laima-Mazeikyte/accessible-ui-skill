---
name: accessible-ui
description: Accessibility guidelines and patterns for building WCAG 2.2 AA compliant HTML. Use when creating base page structures, building reusable UI components, or implementing forms. Provides guidance on semantic HTML, ARIA labels, alt text, keyboard navigation, and contrast ratios. Triggers on requests for accessible forms, page layouts, navigation, or any UI component that needs accessibility support.
---

# Accessible UI

Provide accessible, framework-agnostic HTML patterns that comply with WCAG 2.2 AA.

## Core Principles

1. **Semantic first** - Use correct HTML elements before adding ARIA
2. **Keyboard accessible** - All interactive elements reachable and operable via keyboard
3. **Visible focus** - Clear focus indicators on all interactive elements
4. **Labeled controls** - Every form control has an accessible name
5. **Sufficient contrast** - Text meets 4.5:1 ratio (3:1 for large text)

## Quick Reference

### Page Structure

```html
<body>
  <a href="#main" class="skip-link">Skip to main content</a>
  <header role="banner">
    <nav aria-label="Main">...</nav>
  </header>
  <main id="main">...</main>
  <footer role="contentinfo">...</footer>
</body>
```

### Form Pattern

```html
<form>
  <div>
    <label for="email">Email</label>
    <input type="email" id="email" name="email" required
           aria-describedby="email-hint">
    <span id="email-hint">We'll never share your email</span>
  </div>
  <button type="submit">Submit</button>
</form>
```

## Reference Files

Load these based on task requirements:

| File | When to load |
|------|--------------|
| [semantic-html.md](references/semantic-html.md) | Page structure, landmarks, headings |
| [forms.md](references/forms.md) | Inputs, textareas, radios, checkboxes, selects, buttons |
| [aria.md](references/aria.md) | Custom widgets, dynamic content, complex interactions |
| [keyboard.md](references/keyboard.md) | Focus management, tab order, keyboard handlers |
| [contrast.md](references/contrast.md) | Color selection, testing, visual design |

## Checklist Before Completion

- [ ] All form controls have associated labels
- [ ] Error messages linked via `aria-describedby`
- [ ] Required fields marked with `required` attribute and visual indicator
- [ ] Focus order matches visual order
- [ ] All images have appropriate alt text (or `alt=""` for decorative)
- [ ] Interactive elements have visible focus styles
- [ ] Color is not the only means of conveying information
