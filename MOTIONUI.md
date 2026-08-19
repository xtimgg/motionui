# MotionUI — Design System Reference

Material You–inspired component library. Two files, zero dependencies, auto-initializes.

```html
<link rel="stylesheet" href="theme.css">
<link rel="stylesheet" href="components.css">
<script src="motionui.js"></script>
```

Add `data-mu-hue="250"` to `<html>` to set initial hue (0–359). Add `data-mu-blur` to enable blur mode.

---

## Theming

The entire palette derives from a single hue via oklch(). Secondary is hue+60, tertiary is hue+150. Surfaces are near-black HSL with 50% saturation at the source hue.

```js
MU.setHue(180);          // instant
MU.setHue(180, true);    // animated arc transition
MU.setBlur(true);        // adds .blur-enabled to <html>
```

On theme change a `mu:themechange` event fires on `document` with `{ detail: { hue } }`.

### CSS tokens

```css
/* Color roles */
--color-primary / --color-on-primary
--color-primary-container / --color-on-primary-container
--color-secondary / --color-on-secondary / --color-secondary-container / --color-on-secondary-container
--color-tertiary / --color-on-tertiary / --color-tertiary-container / --color-on-tertiary-container
--color-error / --color-on-error / --color-error-container / --color-on-error-container

/* Surfaces (near-black, hue-tinted) */
--color-surface-dim
--color-surface
--color-surface-bright
--color-surface-container-lowest / -low / (base) / -high / -highest

/* Text / borders */
--color-on-surface / --color-on-surface-variant
--color-outline / --color-outline-variant

/* Gradient */
--color-gradient-start   /* = primary */
--color-gradient-end     /* = tertiary */

/* Spacing: --space-1 (4px) through --space-16 (64px) */
/* Radius: --radius-none, -xs, -sm, -md, -lg, -xl, -2xl, -full */
/* Elevation: --elevation-0 through --elevation-5 */
/* Motion easing: --ease-spring, -spring-soft, -spring-bouncy, -out, -in, -inout */
/* Duration: --dur-1 (50ms) through --dur-9 (500ms) */
```

---

## Auto-init

Everything initializes automatically on `DOMContentLoaded`. For dynamically inserted elements (e.g. from fetch), MU uses a MutationObserver — no manual re-init needed.

---

## Components

### Buttons

```html
<button class="btn btn-filled">Filled</button>
<button class="btn btn-tonal">Tonal</button>
<button class="btn btn-elevated">Elevated</button>
<button class="btn btn-outlined">Outlined</button>
<button class="btn btn-text">Text</button>
<button class="btn btn-destructive">Destructive</button>
<button class="btn btn-destructive-outlined">Dest. Outlined</button>

<!-- Gradient (static, no shimmer) -->
<button class="btn btn-gradient-primary">Gradient</button>
<button class="btn btn-gradient-secondary">Gradient 2</button>

<!-- Icon buttons -->
<button class="btn btn-icon">⚙</button>
<button class="btn btn-icon-filled">＋</button>

<!-- FAB -->
<button class="btn btn-fab">♡</button>
<button class="btn btn-fab-extended"><span>✎</span>Edit</button>

<!-- Sizes -->
<button class="btn btn-filled btn-sm">Small</button>
<button class="btn btn-filled btn-lg">Large</button>

<!-- Disabled -->
<button class="btn btn-filled" disabled>Disabled</button>
```

Ripple, hover lift, and scale-on-active are automatic.

---

### Cards

```html
<!-- Elevated (shadow, hover lift + sheen) -->
<div class="card card-elevated card-interactive">
  <div class="card-header">
    <div class="card-avatar">A</div>
    <div>
      <div class="card-title">Title</div>
      <div class="card-subtitle">Subtitle</div>
    </div>
  </div>
  <div class="card-body">Supporting text.</div>
  <div class="card-actions">
    <button class="btn btn-text btn-sm">Dismiss</button>
    <button class="btn btn-tonal btn-sm">Action</button>
  </div>
</div>

<!-- Filled (uses surface-container-highest) -->
<div class="card card-filled">...</div>

<!-- Outlined (border only) -->
<div class="card card-outlined">...</div>
```

Add `card-interactive` for cursor pointer + spring hover lift. The `::after` sheen sweep only triggers on interactive cards.

---

### Chips

```html
<div class="chip chip-assist">Assist</div>
<div class="chip chip-filter">Filter</div>           <!-- toggles chip-selected on click -->
<div class="chip chip-filter chip-selected">Active</div>
<div class="chip chip-suggestion">Suggestion</div>   <!-- toggles chip-selected on click -->
<div class="chip chip-input">Input ✕</div>
```

---

### Inputs

```html
<!-- Filled -->
<div class="field">
  <label class="field-label">Label</label>
  <input class="input" type="text" placeholder="…">
  <span class="field-support">Helper text</span>
</div>

<!-- Outlined -->
<div class="field">
  <label class="field-label">Label</label>
  <input class="input input-outlined" type="text" placeholder="…">
</div>

<!-- Search -->
<div class="field">
  <div class="input-search-wrap">
    <span class="input-search-icon">🔍</span>
    <input class="input input-search" type="search" placeholder="Search…">
  </div>
</div>

<!-- Error state -->
<div class="field">
  <input class="input error-state" type="email">
  <span class="field-support error">Not valid</span>
</div>

<!-- Textarea -->
<textarea class="input input-outlined" rows="4"></textarea>

<!-- Select -->
<div class="select-wrap">
  <select class="input input-outlined">
    <option>Option A</option>
  </select>
  <span class="select-arrow">▾</span>
</div>
```

Focus uses `outline` (no layout shift). Label color transitions to primary on focus-within.

---

### Selection Controls

```html
<!-- Switch -->
<label class="switch">
  <input type="checkbox" checked>
  <div class="switch-track"><div class="switch-thumb"></div></div>
  <span class="switch-label">Label</span>
</label>

<!-- Checkbox -->
<label class="checkbox">
  <input type="checkbox">
  <div class="checkbox-box"></div>
  <span class="checkbox-label">Label</span>
</label>
<!-- Indeterminate: add class="checkbox indeterminate" to wrapper (no input needed) -->

<!-- Radio -->
<label class="radio">
  <input type="radio" name="group">
  <div class="radio-dot"></div>
  <span class="radio-label">Option</span>
</label>

<!-- Slider (JS auto-fills track color + updates .slider-value) -->
<div class="slider-wrap">
  <div class="slider-label-row">
    <span class="slider-label">Volume</span>
    <span class="slider-value">70</span>
  </div>
  <input type="range" class="slider" min="0" max="100" value="70">
</div>

<!-- Segmented button -->
<div class="segmented">
  <button class="segmented-btn active">Day</button>
  <button class="segmented-btn">Week</button>
  <button class="segmented-btn">Month</button>
</div>
```

---

### Progress

```html
<!-- Linear determinate -->
<div class="progress-bar">
  <div class="progress-bar-fill" style="width: 65%"></div>
</div>

<!-- Linear indeterminate -->
<div class="progress-bar indeterminate">
  <div class="progress-bar-fill"></div>
</div>

<!-- Circular (JS required) -->
<div id="my-progress"></div>
<script>
  // Determinate
  const p = MU.circularProgress(document.getElementById('my-progress'), {
    value: 72,   // 0–100, omit for indeterminate
    size: 48,    // px
    stroke: 4,   // px
  });
  p.setValue(90);     // update later
  p.setValue(null);   // switch to indeterminate
</script>

<!-- Wavy line progress (JS required) -->
<div id="wave-linear"></div>
<div id="wave-circular"></div>
<script>
  // Linear wavy bar — determinate
  const wl = MU.waveProgress(document.getElementById('wave-linear'), {
    mode:        'linear',
    value:       65,        // 0–100, null = indeterminate
    amplitude:   5,         // wave height px
    frequency:   3,         // wave cycles across bar
    strokeWidth: 3,         // line thickness px
    color:       'primary', // 'primary'|'secondary'|'tertiary'|'error'|any CSS color
    trackColor:  'surface', // same options as color
    animateWave: true,      // animate phase continuously
    animSpeed:   3,         // radians/sec
    height:      28,        // svg height px (auto if omitted)
    // width: 300,          // explicit width px — defaults to parent width
  });
  wl.setValue(90);          // update value (animates)
  wl.setValue(null);        // switch to indeterminate
  wl.setAmplitude(8);       // live-tune wave shape
  wl.setFrequency(5);

  // Circular wavy progress
  const wc = MU.waveProgress(document.getElementById('wave-circular'), {
    mode:        'circular',
    value:       72,
    radius:      40,        // circle radius px
    amplitude:   4,         // radial wave amplitude px
    frequency:   9,         // wave cycles around the circle
    strokeWidth: 3,
    color:       'primary',
    trackColor:  'surface',
    animateWave: true,
    animSpeed:   2,
  });
  wc.setValue(50);

  // Low-level path generator (returns { d, viewBox, size/width/height })
  const { d, viewBox } = MU.wavyLinePath({
    mode: 'circular', radius: 40, amplitude: 5, frequency: 8, phase: 0, progress: 0.75,
  });
</script>
```

---

### Navigation

```html
<!-- Top App Bar -->
<div class="top-app-bar">
  <button class="btn btn-icon">←</button>
  <span class="top-app-bar-title">Title</span>
  <div class="top-app-bar-actions">
    <button class="btn btn-icon">🔍</button>
  </div>
</div>

<!-- Glass Dock — MU auto-injects sliding indicator and handles clicks -->
<div class="nav-dock">
  <button class="dock-item active">
    <span class="dock-item-icon">⌂</span>
    <span>Home</span>
  </button>
  <button class="dock-item">
    <span class="dock-item-icon">🔍</span>
    <span>Search</span>
  </button>
</div>
<!-- Fires: mu:dockchange on the .nav-dock element with { detail: { item } } -->

<!-- Material Nav Bar (bottom, sliding pill) -->
<nav class="nav-bar">
  <button class="nav-item active">
    <span class="nav-item-icon">⌂</span>
    <span class="nav-item-label">Home</span>
  </button>
  <button class="nav-item">
    <span class="nav-item-icon">🔍</span>
    <span class="nav-item-label">Search</span>
  </button>
</nav>

<!-- Tabs (sliding underline) -->
<div class="tabs">
  <button class="tab active" data-panel="panel1">
    <span class="tab-icon">📄</span>Tab 1
  </button>
  <button class="tab" data-panel="panel2">Tab 2</button>
</div>
<div id="panel1">Content 1</div>
<div id="panel2" hidden>Content 2</div>
<!-- Fires: mu:tabchange on the .tabs element with { detail: { index, tab } } -->

<!-- Nav Drawer -->
<div class="nav-drawer">
  <div class="nav-drawer-section-label">Section</div>
  <div class="nav-drawer-item active">⌂ Home</div>
  <div class="nav-drawer-item">🔍 Explore</div>
</div>
```

---

### Lists & Menu

```html
<!-- List -->
<div class="list">
  <div class="list-item">
    <span class="list-item-icon">🎵</span>
    <div class="list-item-content">
      <div class="list-item-headline">Track title</div>
      <div class="list-item-support">Artist · Album</div>
    </div>
    <span class="list-item-trailing">3:24</span>
  </div>
</div>

<!-- Divider -->
<div class="divider"></div>
<div class="divider divider-inset"></div>

<!-- Menu (position it with CSS/JS) -->
<div class="menu">
  <div class="menu-item"><span class="menu-item-icon">✎</span>Edit</div>
  <div class="menu-item"><span class="menu-item-icon">⬆</span>Export</div>
  <div class="menu-divider"></div>
  <div class="menu-item destructive"><span class="menu-item-icon">🗑</span>Delete</div>
</div>
```

Click expands item height; siblings redistribute space proportionally (closer = more give).

---

### Accordion

```html
<div class="accordion">
  <div class="accordion-item open">
    <button class="accordion-trigger">
      Question text
      <span class="accordion-arrow">▾</span>
    </button>
    <div class="accordion-body">
      <div class="accordion-body-inner">
        <div class="accordion-content">Answer text.</div>
      </div>
    </div>
  </div>
  <div class="accordion-item">
    <!-- same structure, no .open -->
  </div>
</div>
```

Opens one at a time. Animation uses CSS `grid-template-rows: 0fr → 1fr` (no JS height measurement).

---

### Overlays (JS API)

```js
// Snackbar
MU.snackbar('Message');
MU.snackbar('Item deleted', {
  action: 'Undo',
  onAction: () => MU.snackbar('Restored'),
  duration: 5000,   // ms, default 4000
});

// Dialog
MU.dialog({
  icon: '🗑',           // optional emoji/text icon
  title: 'Title',
  body: 'Body text.',
  actions: [
    { label: 'Cancel', variant: 'btn-text' },
    { label: 'Delete', variant: 'btn-destructive', fn: () => doDelete() },
  ],
});

// Bottom Sheet (draggable handle, spring dismiss)
MU.sheet({
  content: '<p>HTML string or HTMLElement</p>',
});

// Tooltip (programmatic)
MU.tooltip(element, 'Tooltip text');

// Tooltip (CSS-only)
```
```html
<div class="tooltip-wrap">
  <button class="btn btn-outlined">Hover</button>
  <span class="tooltip">Appears on hover</span>
</div>
```

---

### Feedback

```html
<!-- Banners -->
<div class="banner banner-info">
  <span class="banner-icon">ℹ️</span>
  <div class="banner-content">
    <div class="banner-title">Info</div>
    Message text.
  </div>
</div>
<!-- Variants: banner-info, banner-success, banner-warning, banner-error -->

<!-- Badge -->
<div class="badge">3</div>
<div class="badge badge-dot"></div>      <!-- dot only -->
<div class="badge badge-lg">99+</div>

<!-- Badge on element -->
<div class="badge-wrap">
  <button class="btn btn-icon">🔔</button>
  <div class="badge">5</div>
</div>

<!-- Avatar -->
<div class="avatar avatar-sm">A</div>
<div class="avatar avatar-md">MU</div>
<div class="avatar avatar-lg">AB</div>
<div class="avatar avatar-xl"><img src="photo.jpg" alt=""></div>

<!-- Avatar group -->
<div class="avatar-group">
  <div class="avatar avatar-md">A</div>
  <div class="avatar avatar-md">B</div>
  <div class="avatar avatar-md">C</div>
</div>
```

---

### Skeletons

```html
<div class="skeleton skeleton-text"></div>
<div class="skeleton skeleton-text" style="width:60%"></div>
<div class="skeleton skeleton-circle" style="width:44px;height:44px"></div>
<div class="skeleton skeleton-card"></div>
<div class="skeleton skeleton-rect"></div>
```

Pulse + shimmer animations. Use inline width to vary text line lengths.

---

### Metaball

The metaball effect requires a `filter:contrast()` wrapper (`blob-scene`) with a background color that **exactly matches its parent**. MU auto-syncs this on init and theme change.

```html
<!-- Container: position:relative, explicit background color -->
<div class="my-container" style="background:var(--color-surface-container-low); position:relative; height:200px;">

  <!-- Scene: wraps all blobs, must match parent bg (auto-synced) -->
  <div class="blob-scene">
    <!-- Blobs: solid color, single blur, no gradients -->
    <div class="blob" style="width:80px;height:80px;top:50%;left:40%;transform:translate(-50%,-50%)"></div>
    <div class="blob" style="width:80px;height:80px;top:50%;left:60%;transform:translate(-50%,-50%)"></div>
  </div>

  <!-- Labels/UI: OUTSIDE .blob-scene so they're not inside the contrast filter -->
  <div style="position:absolute;inset:0;pointer-events:none;z-index:10">
    <span style="position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);color:var(--color-on-primary)">Label</span>
  </div>
</div>
```

**Connection distance control:**
```html
<div class="blob-scene blob-near">  <!-- blobs connect from closer (blur:7px, contrast:28) -->
<div class="blob-scene blob-mid">   <!-- default (blur:14px, contrast:22) -->
<div class="blob-scene blob-far">   <!-- connect from farther (blur:24px, contrast:18) -->
```

**Custom blob color:**
```html
<div class="blob" style="--blob-color: var(--color-secondary);"></div>
```

**Rules for blobs:**
- Background must be one solid color — no gradients, no multi-color
- All blobs in a scene should be the same color for crisp edges
- `filter:blur()` on blobs controls merge distance (handled via `--blob-blur`)
- Never put text or non-blob elements inside `.blob-scene`

**Loaders (CSS-only, no JS):**
```html
<!-- 2-blob merge -->
<div class="blob-loader-scene">
  <div class="blob"></div>
  <div class="blob"></div>
</div>

<!-- 3-blob squeeze -->
<div class="blob-loader-3-scene">
  <div class="blob"></div>
  <div class="blob"></div>
  <div class="blob"></div>
</div>
```

**Manual bg sync (if you can't use CSS vars for parent bg):**
```html
<div class="blob-scene" data-blob-bg-manual></div>
<!-- then set: scene.style.background = '#1a1a2e' -->
```

---

## JS API reference

```js
MU.setHue(hue, animate = true)     // regenerate full palette
MU.setBlur(bool)                   // toggle blur mode
MU.snackbar(msg, opts)             // → { dismiss() }
MU.dialog(opts)                    // → { close() }
MU.sheet(opts)                     // → { close() }
MU.circularProgress(el, opts)      // → { setValue(v) }
MU.tooltip(el, text)               // wraps element in .tooltip-wrap
MU.spring({ from, to, stiffness, damping, onUpdate, onComplete })  // → { cancel() }
MU.syncBlobScenes()                // re-sync CSS blob loader backgrounds
MU.metaball(canvas, blobs, opts)   // → { update(blobs), setBlob(i,desc), play(), pause(), destroy() }
MU.ripple(el, pointerEvent)        // manually spawn ripple
MU.palette.currentHue              // read current hue
MU.waveProgress(el, opts)          // → { setValue(v), setAmplitude(a), setFrequency(f), destroy() }
MU.wavyLinePath(opts)              // → { d, viewBox, size/width/height }  — low-level path generator
```

---

## Events

| Event | Target | Detail |
|---|---|---|
| `mu:themechange` | `document` | `{ hue }` |
| `mu:tabchange` | `.tabs` element | `{ index, tab }` |
| `mu:dockchange` | `.nav-dock` element | `{ item }` |

---

## Layout utilities

```html
<!-- Grid -->
<div class="grid-2">...</div>   <!-- 2 cols, collapses at 768px -->
<div class="grid-3">...</div>   <!-- 3 cols, collapses at 768px/480px -->

<!-- Page wrapper -->
<div class="page">...</div>     <!-- max-width:1200px, centered, padding -->

<!-- Section -->
<div class="section">
  <div class="section-title">Title</div>
  ...
</div>

<!-- Surface tints (bg only) -->
<div class="mu-surface-low">...</div>
<div class="mu-surface-container">...</div>
<div class="mu-surface-high">...</div>
<div class="mu-surface-highest">...</div>
```

---

## Typography classes

```html
<h1 class="mu-display-large">Display Large</h1>
<h2 class="mu-headline-large">Headline Large</h2>
<h3 class="mu-title-large">Title Large</h3>
<p class="mu-body-large">Body text</p>
<span class="mu-label-medium">LABEL</span>

<!-- Color modifiers -->
<span class="mu-text-primary">Primary</span>
<span class="mu-text-secondary">Secondary</span>
<span class="mu-text-dim">Muted</span>
<span class="mu-text-error">Error</span>
```

Scale: display-large/medium/small → headline-large/medium/small → title-large/medium/small → body-large/medium/small → label-large/medium/small.

---

## Blur mode

When `MU.setBlur(true)` is active (or `data-mu-blur` on `<html>`), the class `blur-enabled` is added to `<html>`. This activates two CSS variables:

```css
--_surface-opacity: 0.82;  /* was 1 */
--_backdrop: blur(24px) saturate(1.4);  /* was none */
```

Use the `surface-blur` utility class on any element that should participate:

```html
<header class="surface-blur" style="position:sticky;top:0">...</header>
```

Or apply the vars directly:
```css
.my-panel {
  background: color-mix(in oklch, var(--color-surface-container) calc(var(--_surface-opacity) * 100%), transparent);
  backdrop-filter: var(--_backdrop);
}
```

---

## Tips for building on this system

- All color decisions should reference CSS vars — never hardcode oklch/hsl values
- Use `--color-surface-container-low/high/highest` for layering (not opacity hacks)
- Prefer `color-mix(in oklch, ...)` for tints over raw rgba
- For animated entrances, apply `animation: mu-slide-up var(--dur-5) var(--ease-spring-soft)` or `mu-scale-in-spring`
- Ripple is auto-attached to `button`, `a[href]`, `.btn`, `.chip`, `.list-item`, `.menu-item`, `.tab`, `.nav-drawer-item`, `[data-ripple]`
- MutationObserver watches `document.body` — dynamic components inserted via innerHTML get auto-initialized
- Spring util (`MU.spring`) is useful for gesture-driven animations where CSS transitions aren't enough
- Metaball scenes that live inside dynamically themed containers should call `MU.syncBlobScenes()` after inserting them