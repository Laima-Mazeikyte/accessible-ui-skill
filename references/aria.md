# ARIA Reference

## Table of Contents

- [First Rule of ARIA](#first-rule-of-aria)
- [When ARIA Is Needed](#when-aria-is-needed)
- [Accessible Names](#accessible-names)
- [ARIA States](#aria-states)
- [ARIA Properties](#aria-properties)
- [Live Regions](#live-regions)
- [aria-hidden](#aria-hidden)
- [Visually Hidden](#visually-hidden)
- [Common Widget Patterns](#common-widget-patterns)

## First Rule of ARIA

**Don't use ARIA if you can use native HTML.**

```html
<!-- Bad -->
<div role="button" tabindex="0" onclick="submit()">Submit</div>

<!-- Good -->
<button type="submit">Submit</button>
```

## When ARIA Is Needed

1. Custom widgets not available in HTML (tabs, tree views)
2. Dynamic content updates (live regions)
3. Relationships not expressible in HTML
4. States not available in HTML

## Accessible Names

Every interactive element needs an accessible name. **Priority order:**

1. `aria-labelledby` (references another element)
2. `aria-label` (string value)
3. Native HTML (label, alt, content)

```html
<!-- aria-labelledby: references visible text -->
<h2 id="billing">Billing address</h2>
<form aria-labelledby="billing">...</form>

<!-- aria-label: when no visible label -->
<button aria-label="Close">×</button>

<!-- Native: preferred when possible -->
<label for="name">Name</label>
<input id="name">
```

## ARIA States

| Attribute | Purpose | Values |
|-----------|---------|--------|
| `aria-expanded` | Expandable element | `true`, `false` |
| `aria-selected` | Selection state | `true`, `false` |
| `aria-checked` | Checkbox/toggle | `true`, `false`, `mixed` |
| `aria-pressed` | Toggle button | `true`, `false` |
| `aria-disabled` | Disabled state | `true`, `false` |
| `aria-hidden` | Hidden from AT | `true`, `false` |
| `aria-invalid` | Validation state | `true`, `false` |
| `aria-busy` | Loading state | `true`, `false` |

## ARIA Properties

| Attribute | Purpose |
|-----------|---------|
| `aria-describedby` | Additional description (hints, errors) |
| `aria-labelledby` | Accessible name from another element |
| `aria-label` | Accessible name as string |
| `aria-controls` | Element this one controls |
| `aria-owns` | Parent/child relationship |
| `aria-live` | Announce changes |
| `aria-current` | Current item in set |
| `aria-haspopup` | Has popup menu/dialog |

## Live Regions

Announce dynamic content to screen readers:

```html
<!-- Polite: announced when user is idle -->
<div aria-live="polite">Your changes have been saved.</div>

<!-- Assertive: announced immediately -->
<div aria-live="assertive">Session expires in 1 minute.</div>

<!-- Status: implicit polite live region -->
<div role="status">3 results found.</div>

<!-- Alert: implicit assertive live region -->
<div role="alert">Error: Payment failed.</div>
```

## aria-hidden

Hides content from assistive technology but keeps it visible:

```html
<button>
  <svg aria-hidden="true">...</svg>
  Save
</button>
```

**Never** use `aria-hidden="true"` on focusable elements.

## Visually Hidden

For screen reader-only text, use CSS:

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

```html
<button>
  <svg aria-hidden="true">...</svg>
  <span class="visually-hidden">Close dialog</span>
</button>
```

## Common Widget Patterns

### Disclosure (Show/Hide)

```html
<button aria-expanded="false" aria-controls="content">More details</button>
<div id="content" hidden>Additional content here.</div>
```

Update `aria-expanded` and `hidden` with JavaScript.

### Tabs

```html
<div role="tablist" aria-label="Product information">
  <button role="tab" id="tab-1" aria-selected="true" aria-controls="panel-1">
    Description
  </button>
  <button role="tab" id="tab-2" aria-selected="false" aria-controls="panel-2" tabindex="-1">
    Reviews
  </button>
</div>

<div role="tabpanel" id="panel-1" aria-labelledby="tab-1">
  Description content...
</div>
<div role="tabpanel" id="panel-2" aria-labelledby="tab-2" hidden>
  Reviews content...
</div>
```

### Modal Dialog

```html
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title">
  <h2 id="dialog-title">Confirm deletion</h2>
  <p>Are you sure you want to delete this item?</p>
  <button type="button">Cancel</button>
  <button type="button">Delete</button>
</div>
```

Requires focus trapping—see keyboard.md.

### Tooltip

```html
<button aria-describedby="tooltip">Settings</button>
<div role="tooltip" id="tooltip">Configure application preferences</div>
```

### Progress

```html
<!-- Determinate -->
<div role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"
     aria-label="Upload progress">75%</div>

<!-- Indeterminate -->
<div role="progressbar" aria-label="Loading">Loading...</div>
```
