# Linux (GNOME/Adwaita) — System Colors

Source: libadwaita CSS variables, GNOME HIG palette reference, `_palette.scss`

## Adwaita Palette

The GNOME palette consists of 10 color families, each with 5 shades (1=lightest, 5=darkest).
Used primarily in icons and illustrations.

### Blue

| Shade | Hex | Usage |
|-------|-----|-------|
| blue_1 | `#99C1F1` | Light tint, backgrounds |
| blue_2 | `#62A0EA` | Hover states |
| blue_3 | `#3584E4` | **Default accent** (accent_bg_color) |
| blue_4 | `#1C71D8` | Active/pressed |
| blue_5 | `#1A5FB4` | Dark accent |

### Green

| Shade | Hex |
|-------|-----|
| green_1 | `#8FF0A4` |
| green_2 | `#57E389` |
| green_3 | `#33D17A` |
| green_4 | `#2EC27E` |
| green_5 | `#26A269` |

### Yellow

| Shade | Hex |
|-------|-----|
| yellow_1 | `#F9F06B` |
| yellow_2 | `#F8E45C` |
| yellow_3 | `#F6D32D` |
| yellow_4 | `#F5C211` |
| yellow_5 | `#E5A50A` |

### Orange

| Shade | Hex |
|-------|-----|
| orange_1 | `#FFBE6F` |
| orange_2 | `#FFA348` |
| orange_3 | `#FF7800` |
| orange_4 | `#E66100` |
| orange_5 | `#C64600` |

### Red

| Shade | Hex |
|-------|-----|
| red_1 | `#F66151` |
| red_2 | `#ED333B` |
| red_3 | `#E01B24` |
| red_4 | `#C01C28` |
| red_5 | `#A51D2D` |

### Purple

| Shade | Hex |
|-------|-----|
| purple_1 | `#DC8ADD` |
| purple_2 | `#C061CB` |
| purple_3 | `#9141AC` |
| purple_4 | `#813D9C` |
| purple_5 | `#613583` |

### Brown

| Shade | Hex |
|-------|-----|
| brown_1 | `#CDAB8F` |
| brown_2 | `#B5835A` |
| brown_3 | `#986A44` |
| brown_4 | `#865E3C` |
| brown_5 | `#63452C` |

### Neutrals (Light)

| Shade | Hex |
|-------|-----|
| light_1 | `#FFFFFF` |
| light_2 | `#F6F5F4` |
| light_3 | `#DEDDDA` |
| light_4 | `#C0BFBC` |
| light_5 | `#9A9996` |

### Neutrals (Dark)

| Shade | Hex |
|-------|-----|
| dark_1 | `#77767B` |
| dark_2 | `#5E5C64` |
| dark_3 | `#3D3846` |
| dark_4 | `#241F31` |
| dark_5 | `#000000` |

## Semantic CSS Variables — Light Theme

| Variable | Value | Usage |
|----------|-------|-------|
| `--accent-bg-color` | `#3584E4` | Accent button backgrounds |
| `--accent-fg-color` | `#FFFFFF` | Text on accent backgrounds |
| `--accent-color` | `#3584E4` | Standalone accent (links, focus) |
| `--window-bg-color` | `#FAFAFA` | Main window background |
| `--window-fg-color` | `#2E3436` | Primary text on window |
| `--view-bg-color` | `#FFFFFF` | Text views, entries, lists |
| `--view-fg-color` | `#2E3436` | Text on view backgrounds |
| `--headerbar-bg-color` | `#EBEBEB` | Header bar background |
| `--headerbar-fg-color` | `#2E3436` | Header bar text |
| `--headerbar-backdrop-color` | `#FAFAFA` | Header bar unfocused |
| `--card-bg-color` | `#FFFFFF` | Card backgrounds |
| `--card-fg-color` | `#2E3436` | Card text |
| `--popover-bg-color` | `#FFFFFF` | Popover backgrounds |
| `--popover-fg-color` | `#2E3436` | Popover text |
| `--dialog-bg-color` | `#FAFAFA` | Dialog backgrounds |
| `--dialog-fg-color` | `#2E3436` | Dialog text |
| `--sidebar-bg-color` | `#EBEBEB` | Sidebar background |
| `--sidebar-fg-color` | `#2E3436` | Sidebar text |
| `--sidebar-backdrop-color` | `#F2F2F2` | Sidebar unfocused |

## Semantic CSS Variables — Dark Theme

| Variable | Value | Usage |
|----------|-------|-------|
| `--accent-bg-color` | `#3584E4` | Accent (same in dark) |
| `--accent-fg-color` | `#FFFFFF` | Text on accent |
| `--accent-color` | `#78AEED` | Standalone accent (lighter for contrast) |
| `--window-bg-color` | `#242424` | Main window background |
| `--window-fg-color` | `#FFFFFF` | Primary text |
| `--view-bg-color` | `#1E1E1E` | Text views, entries |
| `--view-fg-color` | `#FFFFFF` | Text on views |
| `--headerbar-bg-color` | `#303030` | Header bar background |
| `--headerbar-fg-color` | `#FFFFFF` | Header bar text |
| `--headerbar-backdrop-color` | `#242424` | Header bar unfocused |
| `--card-bg-color` | `#383838` | Card backgrounds |
| `--card-fg-color` | `#FFFFFF` | Card text |
| `--popover-bg-color` | `#383838` | Popover backgrounds |
| `--popover-fg-color` | `#FFFFFF` | Popover text |
| `--dialog-bg-color` | `#383838` | Dialog backgrounds |
| `--dialog-fg-color` | `#FFFFFF` | Dialog text |
| `--sidebar-bg-color` | `#303030` | Sidebar background |
| `--sidebar-fg-color` | `#FFFFFF` | Sidebar text |
| `--sidebar-backdrop-color` | `#2A2A2A` | Sidebar unfocused |

## Accent Colors (GNOME 47+)

Since GNOME 47, users can choose a system-wide accent color. The default is blue.
Available accents:

| Name | `--accent-bg-color` | `--accent-color` (dark) |
|------|---------------------|------------------------|
| Blue (default) | `#3584E4` | `#78AEED` |
| Teal | `#2190A4` | `#6BC5D8` |
| Green | `#3A944A` | `#6DBA7A` |
| Yellow | `#C88800` | `#DBA84D` |
| Orange | `#ED5B00` | `#F08C4A` |
| Red | `#E62D42` | `#EB6375` |
| Pink | `#D56199` | `#E28DB5` |
| Purple | `#9141AC` | `#B57BCA` |
| Slate | `#6F8396` | `#97A9B7` |

## Destructive Colors

| Variable | Light | Dark |
|----------|-------|------|
| `--destructive-bg-color` | `#E01B24` (red_3) | `#C01C28` (red_4) |
| `--destructive-fg-color` | `#FFFFFF` | `#FFFFFF` |
| `--destructive-color` | `#E01B24` | `#FF7B63` |

## Success / Warning / Error

| Semantic | Light | Dark |
|----------|-------|------|
| Success | `#26A269` (green_5) | `#57E389` (green_2) |
| Warning | `#E5A50A` (yellow_5) | `#F8E45C` (yellow_2) |
| Error | `#C01C28` (red_4) | `#FF7B63` |

## Borders and Separators

| Variable | Light | Dark |
|----------|-------|------|
| Border (generic) | black @ 0.15 | white @ 0.15 |
| `--border-opacity` | 0.15 | 0.15 |
| Separator color | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| Card border | `rgba(0,0,0, 0.12)` | `rgba(255,255,255, 0.10)` |
| Header bar border (bottom) | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| Entry border (rest) | `rgba(0,0,0, 0.15)` | `rgba(255,255,255, 0.15)` |
| Entry border (focused) | `--accent-color` | `--accent-color` |

## Scrollbar Colors

| State | Light | Dark |
|-------|-------|------|
| Thumb (rest) | `rgba(0,0,0, 0.40)` | `rgba(255,255,255, 0.40)` |
| Thumb (hover) | `rgba(0,0,0, 0.55)` | `rgba(255,255,255, 0.55)` |
| Thumb (active) | `rgba(0,0,0, 0.70)` | `rgba(255,255,255, 0.70)` |
| Trough | transparent | transparent |
