# Forms Reference

## Table of Contents

- [Labels](#labels)
- [Text Inputs](#text-inputs)
- [Textarea](#textarea)
- [Radio Buttons](#radio-buttons)
- [Checkboxes](#checkboxes)
- [Select (Dropdown)](#select-dropdown)
- [Buttons](#buttons)
- [Error Handling](#error-handling)
- [Autocomplete Values](#autocomplete-values)
- [Disabled vs Read-only](#disabled-vs-read-only)

## Labels

**Every form control needs a label.** Never rely solely on placeholder text.

```html
<label for="username">Username</label>
<input type="text" id="username" name="username">
```

## Text Inputs

```html
<!-- Basic -->
<div class="field">
  <label for="name">Full name</label>
  <input type="text" id="name" name="name" autocomplete="name">
</div>

<!-- With hint text -->
<div class="field">
  <label for="password">Password</label>
  <input type="password" id="password" name="password"
         aria-describedby="password-hint" autocomplete="new-password">
  <span id="password-hint">Minimum 8 characters</span>
</div>

<!-- Required field -->
<div class="field">
  <label for="email">Email <span aria-hidden="true">*</span></label>
  <input type="email" id="email" name="email" required autocomplete="email">
</div>
```

### Input Types

Use appropriate types for validation and mobile keyboards:

| Type | Use For |
|------|---------|
| `text` | General text |
| `email` | Email addresses |
| `tel` | Phone numbers |
| `url` | URLs |
| `number` | Numeric values |
| `password` | Passwords |
| `search` | Search queries |

## Textarea

```html
<div class="field">
  <label for="bio">Bio</label>
  <textarea id="bio" name="bio" maxlength="200"
            aria-describedby="bio-count"></textarea>
  <span id="bio-count">200 characters remaining</span>
</div>
```

## Radio Buttons

Group with `<fieldset>` and `<legend>`:

```html
<fieldset>
  <legend>Preferred contact method</legend>
  <div>
    <input type="radio" id="contact-email" name="contact" value="email">
    <label for="contact-email">Email</label>
  </div>
  <div>
    <input type="radio" id="contact-phone" name="contact" value="phone">
    <label for="contact-phone">Phone</label>
  </div>
</fieldset>
```

## Checkboxes

### Single Checkbox

```html
<div>
  <input type="checkbox" id="terms" name="terms" required>
  <label for="terms">I agree to the terms and conditions</label>
</div>
```

### Checkbox Group

Use `<fieldset>` and `<legend>` (same pattern as radio buttons):

```html
<fieldset>
  <legend>Email preferences</legend>
  <div>
    <input type="checkbox" id="news" name="prefs" value="news">
    <label for="news">Newsletter</label>
  </div>
  <div>
    <input type="checkbox" id="updates" name="prefs" value="updates">
    <label for="updates">Product updates</label>
  </div>
</fieldset>
```

## Select (Dropdown)

```html
<div class="field">
  <label for="country">Country</label>
  <select id="country" name="country" autocomplete="country">
    <option value="">Select a country</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
  </select>
</div>
```

Use `<optgroup label="...">` for grouped options.

## Buttons

```html
<button type="submit">Submit</button>
<button type="button" onclick="save()">Save draft</button>

<!-- Icon-only needs accessible name -->
<button type="button" aria-label="Close dialog">
  <svg aria-hidden="true">...</svg>
</button>
```

## Error Handling

### Inline Errors

```html
<div class="field field--error">
  <label for="email">Email</label>
  <input type="email" id="email" required
         aria-invalid="true" aria-describedby="email-error">
  <span id="email-error" class="error">Please enter a valid email address</span>
</div>
```

### Error Summary

Display at top of form with links to each field:

```html
<div role="alert" aria-labelledby="error-heading">
  <h2 id="error-heading">There are 2 errors in this form</h2>
  <ul>
    <li><a href="#email">Enter a valid email address</a></li>
    <li><a href="#password">Password must be at least 8 characters</a></li>
  </ul>
</div>
```

## Autocomplete Values

| Field | Value |
|-------|-------|
| Full name | `name` |
| Email | `email` |
| Phone | `tel` |
| Street address | `street-address` |
| City | `address-level2` |
| Postal code | `postal-code` |
| Country | `country` |
| Username | `username` |
| New password | `new-password` |
| Current password | `current-password` |

## Disabled vs Read-only

```html
<!-- Disabled: not submitted, not focusable -->
<input type="text" value="ABC123" disabled>

<!-- Read-only: submitted, focusable, not editable -->
<input type="text" value="ABC123" readonly>
```

Use `disabled` sparingly—screen reader users may not discover disabled controls.
