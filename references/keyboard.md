# Keyboard Navigation Reference

## Table of Contents

- [Core Principles](#core-principles)
- [Focusable Elements](#focusable-elements)
- [Tab Order](#tab-order)
- [Skip Links](#skip-links)
- [Focus Styles](#focus-styles)
- [Standard Keyboard Interactions](#standard-keyboard-interactions)
- [Roving Tabindex](#roving-tabindex)
- [Focus Trapping (Modals)](#focus-trapping-modals)
- [Focus on Page Changes](#focus-on-page-changes)
- [Loading States](#loading-states)

## Core Principles

1. All functionality available via keyboard
2. Focus visible on all interactive elements
3. Logical tab order matching visual layout
4. No keyboard traps (except modals)

## Focusable Elements

**Natively focusable (no `tabindex` needed):**
- `<a href="...">`
- `<button>`
- `<input>`, `<select>`, `<textarea>`
- `<details>`, `<summary>`

**Make elements focusable:**

```html
<!-- Add to tab order -->
<div tabindex="0">Custom widget</div>

<!-- Programmatically focusable only -->
<div tabindex="-1">Focus target for JavaScript</div>
```

**Never** use `tabindex` greater than 0.

## Tab Order

Tab order should match visual order. Fix with CSS, not tabindex:

```html
<!-- Bad -->
<button tabindex="2">Second</button>
<button tabindex="1">First</button>

<!-- Good: CSS flexbox order -->
<div style="display: flex; flex-direction: row-reverse;">
  <button>First visually</button>
  <button>Second visually</button>
</div>
```

## Skip Links

Allow users to bypass repeated content:

```html
<body>
  <a href="#main" class="skip-link">Skip to main content</a>
  <header>...</header>
  <main id="main" tabindex="-1">...</main>
</body>
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  padding: 8px;
  background: #000;
  color: #fff;
  z-index: 100;
}
.skip-link:focus { top: 0; }
```

## Focus Styles

**Never remove focus outlines without replacement:**

```css
/* Bad */
*:focus { outline: none; }

/* Good */
:focus-visible {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}

/* Hide focus for mouse, show for keyboard */
:focus:not(:focus-visible) { outline: none; }
```

## Standard Keyboard Interactions

| Key | Action |
|-----|--------|
| Tab | Move to next focusable element |
| Shift+Tab | Move to previous |
| Enter | Activate links and buttons |
| Space | Activate buttons, toggle checkboxes |
| Arrow keys | Navigate within widgets |
| Escape | Close dialogs, cancel actions |

## Roving Tabindex

For composite widgets (tabs, menus), use one tab stop with arrow navigation:

```html
<div role="tablist">
  <button role="tab" tabindex="0" aria-selected="true">Tab 1</button>
  <button role="tab" tabindex="-1">Tab 2</button>
  <button role="tab" tabindex="-1">Tab 3</button>
</div>
```

Move `tabindex="0"` between items with JavaScript on arrow key press:

```javascript
tablist.addEventListener('keydown', (e) => {
  const tabs = [...tablist.querySelectorAll('[role="tab"]')];
  const current = tabs.findIndex(t => t.tabIndex === 0);
  
  let next;
  if (e.key === 'ArrowRight') {
    next = (current + 1) % tabs.length;
  } else if (e.key === 'ArrowLeft') {
    next = (current - 1 + tabs.length) % tabs.length;
  } else {
    return;
  }
  
  tabs[current].tabIndex = -1;
  tabs[next].tabIndex = 0;
  tabs[next].focus();
});
```

## Focus Trapping (Modals)

Trap focus within modal dialogs:

```javascript
function trapFocus(element) {
  const focusable = element.querySelectorAll(
    'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
  );
  const first = focusable[0];
  const last = focusable[focusable.length - 1];

  element.addEventListener('keydown', (e) => {
    if (e.key !== 'Tab') return;
    if (e.shiftKey && document.activeElement === first) {
      e.preventDefault();
      last.focus();
    } else if (!e.shiftKey && document.activeElement === last) {
      e.preventDefault();
      first.focus();
    }
  });
  first.focus();
}
```

### Modal Pattern

```javascript
let previousFocus;

function openModal(modal) {
  previousFocus = document.activeElement;
  modal.hidden = false;
  trapFocus(modal);
}

function closeModal(modal) {
  modal.hidden = true;
  previousFocus?.focus();
}

// Close on Escape
modal.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') closeModal(modal);
});
```

## Focus on Page Changes

### SPA Route Changes

```javascript
function onRouteChange() {
  const main = document.querySelector('main');
  main.tabIndex = -1;
  main.focus();
}
```

### After Deleting Item

```javascript
const nextItem = deletedItem.nextElementSibling || deletedItem.previousElementSibling;
nextItem?.focus();
```

### After Form Error

```javascript
errorSummary.focus();
```

## Loading States

Announce loading to screen readers:

```html
<button onclick="loadData()">
  <span class="button-text">Load more</span>
</button>
<div aria-live="polite" class="visually-hidden" id="status"></div>
```

```javascript
async function loadData() {
  document.getElementById('status').textContent = 'Loading...';
  await fetch(...);
  document.getElementById('status').textContent = 'Content loaded.';
}
```
