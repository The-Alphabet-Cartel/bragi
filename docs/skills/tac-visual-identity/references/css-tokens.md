# TAC CSS Design Tokens

Copy-pasteable CSS custom properties for any TAC frontend project.

## Root Variables

```css
:root {
  /* ── Base Backgrounds ── */
  --tac-bg-deep:       #0d0d12;
  --tac-bg-surface:    #16161e;
  --tac-bg-elevated:   #1e1e2a;
  --tac-bg-input:      #12121a;

  /* ── Text ── */
  --tac-text-primary:   #e8e6f0;
  --tac-text-secondary: #9896a8;
  --tac-text-disabled:  #55536a;

  /* ── Rainbow Accents ── */
  --tac-red:    #e05a6d;
  --tac-orange: #e0885a;
  --tac-yellow: #e0c95a;
  --tac-green:  #5ae08b;
  --tac-blue:   #5a9be0;
  --tac-purple: #9b5ae0;

  /* ── Functional ── */
  --tac-success: #5ae08b;
  --tac-warning: #e0c95a;
  --tac-error:   #e05a6d;
  --tac-info:    #5a9be0;

  /* ── Radii ── */
  --tac-radius-card:   12px;
  --tac-radius-panel:   8px;
  --tac-radius-button:  6px;
  --tac-radius-input:   6px;
  --tac-radius-badge:   4px;
  --tac-radius-circle: 50%;

  /* ── Shadows ── */
  --tac-shadow-card:
    0 4px 16px rgba(155, 90, 224, 0.15),
    0 1px 4px rgba(0, 0, 0, 0.3);
  --tac-shadow-interactive:
    0 6px 24px rgba(90, 155, 224, 0.2),
    0 2px 6px rgba(0, 0, 0, 0.4);
  --tac-shadow-accent:
    0 4px 20px rgba(224, 90, 109, 0.18),
    0 4px 20px rgba(155, 90, 224, 0.12),
    0 1px 4px rgba(0, 0, 0, 0.3);

  /* ── Typography ── */
  --tac-font-heading: 'Inter', system-ui, -apple-system, sans-serif;
  --tac-font-body:    'Inter', system-ui, -apple-system, sans-serif;
  --tac-font-mono:    'JetBrains Mono', ui-monospace, monospace;
  --tac-font-weight-heading: 600;
  --tac-font-weight-body:    400;

  /* ── Spacing Scale ── */
  --tac-space-xs:  4px;
  --tac-space-sm:  8px;
  --tac-space-md: 16px;
  --tac-space-lg: 24px;
  --tac-space-xl: 32px;

  /* ── Transitions ── */
  --tac-transition-fast:   150ms ease;
  --tac-transition-normal: 250ms ease;
  --tac-transition-slow:   400ms ease;
}
```

## Base Reset / Body Styles

```css
body {
  margin: 0;
  padding: 0;
  background-color: var(--tac-bg-deep);
  color: var(--tac-text-primary);
  font-family: var(--tac-font-body);
  font-weight: var(--tac-font-weight-body);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}
```

## Common Component Patterns

### Card
```css
.tac-card {
  background: var(--tac-bg-surface);
  border-radius: var(--tac-radius-card);
  box-shadow: var(--tac-shadow-card);
  padding: var(--tac-space-lg);
  transition: box-shadow var(--tac-transition-normal);
}

.tac-card:hover {
  box-shadow: var(--tac-shadow-interactive);
}
```

### Button (primary)
```css
.tac-btn {
  background: var(--tac-purple);
  color: var(--tac-text-primary);
  border: none;
  border-radius: var(--tac-radius-button);
  padding: var(--tac-space-sm) var(--tac-space-md);
  font-family: var(--tac-font-body);
  font-weight: 600;
  cursor: pointer;
  transition: box-shadow var(--tac-transition-fast),
              background var(--tac-transition-fast);
}

.tac-btn:hover {
  box-shadow: var(--tac-shadow-interactive);
  background: #a96be8;
}
```

### Input
```css
.tac-input {
  background: var(--tac-bg-input);
  color: var(--tac-text-primary);
  border: 1px solid rgba(155, 90, 224, 0.2);
  border-radius: var(--tac-radius-input);
  padding: var(--tac-space-sm) var(--tac-space-md);
  font-family: var(--tac-font-body);
  transition: border-color var(--tac-transition-fast),
              box-shadow var(--tac-transition-fast);
}

.tac-input:focus {
  outline: none;
  border-color: var(--tac-purple);
  box-shadow: 0 0 0 3px rgba(155, 90, 224, 0.15);
}
```

### Badge
```css
.tac-badge {
  display: inline-flex;
  align-items: center;
  padding: 2px var(--tac-space-sm);
  border-radius: var(--tac-radius-badge);
  font-size: 0.75rem;
  font-weight: 600;
  background: rgba(155, 90, 224, 0.15);
  color: var(--tac-purple);
}
```

## Bot-Specific Accent Overrides

Apply these on a wrapper element to theme an entire bot's UI:

```css
/* Ratatoskr — purple (default, no override needed) */

/* Portia — blue */
.bot-portia {
  --tac-accent: var(--tac-blue);
  --tac-shadow-card:
    0 4px 16px rgba(90, 155, 224, 0.15),
    0 1px 4px rgba(0, 0, 0, 0.3);
}

/* Prism — green */
.bot-prism {
  --tac-accent: var(--tac-green);
  --tac-shadow-card:
    0 4px 16px rgba(90, 224, 139, 0.15),
    0 1px 4px rgba(0, 0, 0, 0.3);
}

/* Puck — orange */
.bot-puck {
  --tac-accent: var(--tac-orange);
  --tac-shadow-card:
    0 4px 16px rgba(224, 136, 90, 0.15),
    0 1px 4px rgba(0, 0, 0, 0.3);
}
```
