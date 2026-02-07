# Semantic HTML Reference

## Table of Contents

- [Page Landmarks](#page-landmarks)
- [Headings](#headings)
- [Lists](#lists)
- [Tables](#tables)
- [Interactive Elements](#interactive-elements)
- [Images](#images)
- [Language](#language)

## Page Landmarks

Screen readers can jump between landmarks. Use these to structure pages:

| Element | Implicit Role | Purpose | Usage Note |
|---------|---------------|---------|------------|
| `<header>` | banner | Site header | Only when direct child of `<body>` |
| `<nav>` | navigation | Navigation links | Label if multiple: `aria-label="Main"` |
| `<main>` | main | Primary content | One per page |
| `<aside>` | complementary | Related sidebar content | |
| `<footer>` | contentinfo | Site footer | Only when direct child of `<body>` |
| `<section>` | region | Thematic grouping | Requires accessible name |
| `<article>` | article | Self-contained content | |

### Multiple Landmarks

When using multiple landmarks of the same type, label them:

```html
<nav aria-label="Main">...</nav>
<nav aria-label="Footer">...</nav>
```

### Basic Page Structure

```html
<body>
  <a href="#main" class="skip-link">Skip to main content</a>
  <header>
    <nav aria-label="Main">...</nav>
  </header>
  <main id="main">...</main>
  <footer>...</footer>
</body>
```

## Headings

Create document outline. **Never skip levels.**

```html
<h1>Page Title</h1>
  <h2>Section</h2>
    <h3>Subsection</h3>
  <h2>Another Section</h2>
```

**Rules:**
- One `<h1>` per page
- Don't skip levels (h1 → h3 is wrong)
- Don't choose heading level for styling—use CSS

## Lists

| List Type | Use When |
|-----------|----------|
| `<ul>` | Items have no sequence |
| `<ol>` | Order matters |
| `<dl>` | Term/definition pairs |

```html
<!-- Unordered -->
<ul>
  <li>Apple</li>
  <li>Banana</li>
</ul>

<!-- Ordered -->
<ol>
  <li>First step</li>
  <li>Second step</li>
</ol>

<!-- Description list -->
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
</dl>
```

## Tables

Use for tabular data only, never for layout.

```html
<table>
  <caption>Monthly Sales</caption>
  <thead>
    <tr>
      <th scope="col">Month</th>
      <th scope="col">Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">January</th>
      <td>$10,000</td>
    </tr>
  </tbody>
</table>
```

**Required:** `<caption>` for description, `<th scope="col|row">` for headers.

## Interactive Elements

**Always use native elements—they have built-in accessibility:**

| Need | Use | Never |
|------|-----|-------|
| Navigate to URL | `<a href="...">` | `<span onclick>` |
| Trigger action | `<button>` | `<div onclick>` |
| Form input | `<input>`, `<select>`, `<textarea>` | `<div contenteditable>` |

### Links vs Buttons

- `<a>`: Navigate to a URL
- `<button>`: Trigger an action

```html
<!-- Correct -->
<a href="/about">About Us</a>
<button type="button" onclick="save()">Save</button>

<!-- Incorrect -->
<a href="#" onclick="save()">Save</a>
<button onclick="location='/about'">About Us</button>
```

## Images

| Image Type | Alt Text | Example |
|------------|----------|---------|
| Informative | Describe content | `alt="Sales increased 20% in Q4"` |
| Decorative | Empty alt | `alt=""` |
| Complex | Brief alt + figcaption | See below |

```html
<figure>
  <img src="diagram.png" alt="System architecture diagram">
  <figcaption>
    The system consists of three layers: presentation, 
    business logic, and data access.
  </figcaption>
</figure>
```

## Language

Declare page language and mark language changes:

```html
<html lang="en">
  <body>
    <p>The French word for hello is <span lang="fr">bonjour</span>.</p>
  </body>
</html>
```
