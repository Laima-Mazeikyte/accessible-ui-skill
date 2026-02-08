# Accessible UI - Cursor Skill

A Cursor IDE skill that provides accessibility guidelines and patterns for building WCAG 2.2 AA compliant HTML.

## What This Skill Does

When activated, this skill guides you to build accessible UI components with:

- Semantic HTML structure
- Proper ARIA labels and attributes
- Keyboard navigation support
- Form accessibility patterns
- Color contrast guidance

## Installation

### Option 1: Project-Level (Single Project)

Copy to your project's `.cursor/skills/` folder:

```bash
git clone https://github.com/Laima-Mazeikyte/accessible-ui-skill.git .cursor/skills/accessible-ui
```

### Option 2: User-Level (All Projects)

Copy to your global Cursor skills folder:

```bash
git clone https://github.com/Laima-Mazeikyte/accessible-ui-skill.git ~/.cursor/skills/accessible-ui
```

## Contents

| File | Description |
|------|-------------|
| `SKILL.md` | Main skill file with core principles and quick reference |
| `references/semantic-html.md` | Page structure, landmarks, headings |
| `references/forms.md` | Inputs, textareas, radios, checkboxes, selects, buttons |
| `references/aria.md` | Custom widgets, dynamic content, complex interactions |
| `references/keyboard.md` | Focus management, tab order, keyboard handlers |
| `references/contrast.md` | Color selection, testing, visual design |

## Usage

The skill automatically activates when you ask Cursor to:
- Create accessible forms
- Build page layouts
- Implement navigation
- Create UI components that need accessibility support

## License

MIT
