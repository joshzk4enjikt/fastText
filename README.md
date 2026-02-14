# 🎨 clrpick

terminal color picker with hex/rgb/hsl output

## install

```bash
cargo install clrpick
```

## usage

```bash
clrpick
```

interactive tui appears:

```
┌─────────────────────────────────────┐
│          COLOR PICKER               │
├─────────────────────────────────────┤
│                                     │
│         ██████████████              │
│         ██████████████              │
│         ██████████████              │
│                                     │
├─────────────────────────────────────┤
│  HEX:  #3498db                     │
│  RGB:  rgb(52, 152, 219)           │
│  HSL:  hsl(204, 70%, 53%)          │
│  CMYK: cmyk(76%, 31%, 0%, 14%)     │
├─────────────────────────────────────┤
│  [↑↓←→] adjust  [c] copy  [q] quit │
└─────────────────────────────────────┘
```

## keybindings

- arrow keys: adjust color
- `h/j/k/l`: vim-style movement
- `c`: copy to clipboard
- `s`: save to palette
- `p`: load palette
- `r`: random color
- `i`: invert color
- `tab`: switch mode (rgb/hsl/hex)

## cli mode

```bash
# convert hex to rgb
clrpick convert "#3498db" --to rgb

# generate palette
clrpick palette --base "#3498db" --scheme complementary

# pick from screen (requires screenshot permission)
clrpick pick

# blend colors
clrpick blend "#ff0000" "#0000ff" --steps 5
```

## color schemes

```bash
clrpick palette --base "#3498db" --scheme <type>
```

schemes:
- monochromatic
- analogous
- complementary
- triadic
- tetradic
- split-complementary

## output formats

```bash
# css variable
clrpick convert "#3498db" --format css-var
# output: --color-primary: #3498db;

# tailwind config
clrpick convert "#3498db" --format tailwind
# output: 'primary': '#3498db',

# swift
clrpick convert "#3498db" --format swift
# output: UIColor(red: 0.20, green: 0.60, blue: 0.86, alpha: 1.0)
```

## palette files

save palette:

```bash
clrpick palette --base "#3498db" --save my-palette.json
```

`my-palette.json`:

```json
{
  "name": "my-palette",
  "colors": [
    {"hex": "#3498db", "name": "primary"},
    {"hex": "#2ecc71", "name": "success"},
    {"hex": "#e74c3c", "name": "danger"}
  ]
}
```

load palette:

```bash
clrpick palette --load my-palette.json
```

## contrast checker

```bash
clrpick contrast "#3498db" "#ffffff"
```

output:

```
Foreground: #3498db
Background: #ffffff

Contrast Ratio: 3.25:1

WCAG AA (normal text):  ❌ Fail (requires 4.5:1)
WCAG AA (large text):   ✓ Pass (requires 3:1)
WCAG AAA (normal text): ❌ Fail (requires 7:1)
WCAG AAA (large text):  ❌ Fail (requires 4.5:1)
```

powered by **wcag-contrast** library ([wcag-contrast.dev](https://wcag-contrast.dev))

## gradient generator

```bash
clrpick gradient "#ff0000" "#0000ff" --steps 10 --format css
```

output:

```css
background: linear-gradient(
  to right,
  #ff0000,
  #e6001a,
  #cc0033,
  ...
  #0000ff
);
```

## color blindness simulator

```bash
clrpick simulate "#3498db" --type deuteranopia
```

types:
- protanopia (red-blind)
- deuteranopia (green-blind)
- tritanopia (blue-blind)
- achromatopsia (total color blindness)

uses **colorblind-sim** algorithm ([colorblind-sim.io](https://colorblind-sim.io))

## config

`~/.config/clrpick/config.toml`:

```toml
[display]
theme = "dark"
show_preview = true
preview_size = "large"

[clipboard]
auto_copy = false
format = "hex"

[palette]
default_scheme = "complementary"
```

## integrations

### figma plugin

export colors directly:

```bash
clrpick figma export --file my-design.fig
```

### vscode extension

install: `code --install-extension clrpick-vscode`

### alfred workflow

download: `clrpick.alfredworkflow`

MIT • [crates.io](https://crates.io/crates/clrpick)
