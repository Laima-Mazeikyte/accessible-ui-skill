# Color and Contrast Reference

## Table of Contents

- [WCAG 2.2 AA Requirements](#wcag-22-aa-requirements)
- [Safe Color Combinations](#safe-color-combinations)
- [Common Failures](#common-failures)
- [Color Independence](#color-independence)
- [Testing Tools](#testing-tools)
- [Dark Mode](#dark-mode)

## WCAG 2.2 AA Requirements

| Content Type | Minimum Ratio |
|--------------|---------------|
| Normal text (<18pt / <14pt bold) | 4.5:1 |
| Large text (≥18pt / ≥14pt bold) | 3:1 |
| UI components & graphics | 3:1 |

## Safe Color Combinations

**On white (#FFFFFF):**
- Black (#000000): 21:1 ✓
- Dark gray (#595959): 7:1 ✓
- Gray (#767676): 4.5:1 ✓ (AA minimum)
- Light gray (#949494): 3:1 ✓ (large text only)

**On black (#000000):**
- White (#FFFFFF): 21:1 ✓
- Light gray (#A6A6A6): 7:1 ✓
- Gray (#898989): 4.5:1 ✓ (AA minimum)

## Common Failures

### Placeholder Text

```css
/* Bad: 2.3:1 */
::placeholder { color: #c0c0c0; }

/* Good: 4.5:1 */
::placeholder { color: #767676; }
```

### Low Contrast Text

```css
/* Bad: fails contrast */
.muted {
  color: #aaaaaa;
  background: #ffffff;
}

/* Good: meets 4.5:1 */
.muted {
  color: #767676;
  background: #ffffff;
}
```

### Focus Indicators

Focus indicators need 3:1 contrast against adjacent colors:

```css
:focus-visible {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}
```

### Disabled States

Disabled elements are exempt from requirements, but should still be readable:

```css
button:disabled {
  color: #767676;
  background: #e0e0e0;
}
```

## Color Independence

**Never use color as the only way to convey information:**

```html
<!-- Bad: relies on color only -->
<span style="color: red;">Error</span>

<!-- Good: icon + text + color -->
<span class="error">
  <svg aria-hidden="true">⚠</svg>
  Error: Invalid email
</span>
```

### Form Validation

```html
<!-- Bad: only red border -->
<input style="border-color: red;">

<!-- Good: icon + text + border -->
<div class="field field--error">
  <label for="email">Email</label>
  <input type="email" id="email" aria-invalid="true" aria-describedby="email-error">
  <span id="email-error" class="error">
    <svg aria-hidden="true">⚠</svg>
    Please enter a valid email
  </span>
</div>
```

### Links in Text

Links must be distinguishable from surrounding text:

```css
/* Preferred: underline */
a {
  color: #005fcc;
  text-decoration: underline;
}

/* Alternative: 3:1 contrast vs surrounding text + indicator on hover/focus */
a {
  color: #005fcc;
  text-decoration: none;
}

a:hover,
a:focus {
  text-decoration: underline;
}
```

## Testing Tools

### Browser Extensions
- WAVE (WebAIM)
- axe DevTools (Deque)
- Accessibility Insights (Microsoft)

### DevTools
Chrome/Edge: Elements → Computed → Accessibility → Contrast ratio

### Online Tools
- WebAIM Contrast Checker: webaim.org/resources/contrastchecker
- Coolors Contrast Checker: coolors.co/contrast-checker

### Automated Testing
- axe-core (npm package)
- Pa11y (command line)
- Lighthouse (built into Chrome)

## Dark Mode

When supporting dark mode:

1. Test contrast in both modes
2. Don't just invert colors—verify ratios remain valid
3. Use `prefers-color-scheme` media query:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --text: #e0e0e0;
    --background: #1a1a1a;
  }
}
```

Verify contrast ratios remain valid in both themes.
