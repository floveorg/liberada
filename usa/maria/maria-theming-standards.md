# maria/index.html — Theming Standards

## Token Alignment with risa

maria must use risa's token vocabulary, not its own approximate set.

### Token Mapping (maria current → risa standard)

| maria current | risa token | Notes |
|---|---|---|
| `--paper` | `--base` | Main page background |
| `--cream` | `--cream` | Card/panel surfaces (same name) |
| `--magenta` (#e63946) | `--persimmon` (#c03610) | Primary accent / CTA |
| `--sage` | `--mint` | Success / nature accent |
| `--sky` | `--azure` | Info / sky accent |
| `--purple` | `--grape` | Creative accent |
| `--pink` | `--magenta` | Surprise accent |
| (new) | `--ink-soft` | Secondary text |
| (new) | `--base-2` | Slightly darker base |
| (new) | `--marigold` | Warm highlight |
| (new) | `--red-btn` / `--red-btn-hover` / `--red-btn-active` | Button states |
| (new) | `--mag-btn` | Magenta button variant |
| (new) | `--checked` | Checked/active state |
| (new) | `--shadow` | Box shadow |
| (new) | `--r` | Border radius |
| (new) | `--maxw` | Max width |
| (new) | `--disp` / `--body` / `--mono` | Typography |

### Required: Dark Mode Block

risa pattern (must match):
```css
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --ink:#f4e8d8; --ink-soft:#e6d6c2; --base:#24170f; --base-2:#2f1f13;
    --cream:#2b1d11; --persimmon:#ff7d52; --marigold:#ffb020; --magenta:#ff5fa8;
    --grape:#b18aff; --azure:#6aa9ff; --mint:#37d6ab; --shadow:rgba(0,0,0,.45);
    color-scheme: dark;
  }
}
:root[data-theme="dark"]{
  --ink:#f4e8d8; --ink-soft:#e6d6c2; --base:#24170f; --base-2:#2f1f13;
  --cream:#2b1d11; --persimmon:#ff7d52; --marigold:#ffb020; --magenta:#ff5fa8;
  --grape:#b18aff; --azure:#6aa9ff; --mint:#37d6ab; --shadow:rgba(0,0,0,.45);
  color-scheme: dark;
}
```

### Required: Dark-mode override for `:root.dark`

risa pins ink/shadow in dark to prevent `flove.css` from overriding:
```css
:root.dark{
  --ink:#000;
  --ink-soft:#000;
  --shadow:rgba(58,26,10,.16);
}
```

### Hardcoded Colors to Replace

| Hardcoded | Replace with |
|---|---|
| `#fff` (backgrounds) | `var(--cream)` |
| `#fff` (text on colored bg) | `#fff` (keep — text on accent is always white) |
| `#eee` (borders) | `rgba(42,24,16,.08)` or `var(--line)` if available |
| `#888` (secondary text) | `var(--ink-soft)` |
| `#555` (body text) | `var(--ink)` or `var(--ink-soft)` |
| `#aaa` (footer text) | `var(--ink-soft)` |
| `#666` (meta text) | `var(--ink-soft)` |
| `rgba(42,24,16,.5)` (overlay) | `var(--shadow)` or keep |

### Typography

risa uses: `--disp:'Baloo 2'`, `--body:'Figtree'`, `--mono:'Space Mono'`
maria should use same fonts via same tokens, loaded from same Google Fonts link.

### Body

risa: `font-family:var(--body); background:var(--base); color:var(--ink);`
maria current: `font-family: system-ui; background: var(--paper); color: var(--ink);`

### Imports

Required shared CSS imports (order matters):
1. `flove-tabs.css` (tab-bar shared base)
2. Local `<style>` block for page-specific overrides only

### What NOT to change

- Structural HTML (tab-bar, clip-list, social icons) — already aligned
- Component behavior (JS) — unchanged
- maria-specific colors for unique elements (avatar gradient, etc.) — keep as overrides
