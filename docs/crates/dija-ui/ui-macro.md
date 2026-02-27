# The `ui!` Macro

The `ui!` macro is Dija's declarative node tree builder. It compiles a Tailwind-inspired DSL into a typed `Node` tree at compile time — zero runtime parsing, zero string allocation for static content.

```rust
ui!(vbox { gap: 16, bg: slate.900, padding: 24,
    text { color: white, font_size: 24, font_weight: bold, "Dashboard" }
    hbox { gap: 8,
        badge { color: green.500, "Online" }
        text { color: slate.400, "3 users" }
    }
})
```

## Built-in Tags

Six tags map directly to `Node` constructors:

| Tag | Constructor | Description |
|-----|-------------|-------------|
| `vbox` | `Node::vbox()` | Vertical flex container (column) |
| `hbox` | `Node::hbox()` | Horizontal flex container (row) |
| `el` / `box` | `Node::el()` | Generic container |
| `text` | `Node::text_node()` | Text leaf node |
| `slot` | `Node::slot(pid)` | Slot for actor-managed subtrees |
| `divider` | `Node::divider()` | Visual separator |

Any other tag triggers **component resolution** — the tag name is converted from `snake_case` to `PascalCase` and instantiated as a component (see [Component Resolution](#component-resolution)).

## Tailwind-Inspired DSL

Dija's DSL draws heavily from Tailwind CSS. If you know Tailwind, the mapping is intuitive: utility class names become key-value properties, colors use a dot-shade notation, and layout uses the same flex/grid mental model.

### Design Philosophy

Tailwind proved that a constrained set of design tokens — fixed spacing scales, named colors, standard font sizes — produces better UIs than ad-hoc values. Dija adopts this at the language level:

- **Color tokens** instead of hex values: `blue.500` not `#3B82F6`
- **Named sizes** instead of magic numbers: `font_size: lg` not `font_size: 18`
- **Shorthand aliases** instead of verbose field names: `w`, `h`, `p`, `m`, `rounded`
- **Bare flags** instead of boolean properties: `bold` not `font_weight: FontWeight::Bold`
- **Int-to-float coercion** instead of suffix noise: `gap: 16` not `gap: 16.0f32`

Unlike Tailwind (which is string-based and runtime-parsed), Dija's DSL is fully typed and resolved at compile time. Invalid property names, unknown color palettes, and type mismatches are all caught by the Rust compiler.

## Properties

Properties are key-value pairs that set node attributes. They appear before children in the tag body.

```rust
vbox { gap: 16, padding: {x: 24, y: 16}, bg: slate.800, border_radius: 8,
    // children here
}
```

Commas between properties are optional — they improve readability but aren't required.

### Property Categories

#### Colors

Color properties accept color tokens, named colors, tuples, and conditional expressions.

```rust
// Color token: palette.shade
bg: blue.500
color: slate.200
border_color: red.600

// With opacity (0-255)
bg: slate.700/50
color: white

// Named colors
color: white
color: black
color: transparent

// String form
bg: "blue.500"
bg: "slate.700/128"

// Tuple form
bg: {blue, 500}
bg: {"slate", 700, 50}

// Conditional colors
color: if dark { white } else { slate.900 }
bg: match status {
    "active" => green.500,
    "warning" => amber.500,
    _ => slate.500,
}
```

**Available palettes:** `slate`, `gray`, `zinc`, `neutral`, `stone`, `red`, `orange`, `amber`, `yellow`, `lime`, `green`, `emerald`, `teal`, `cyan`, `sky`, `blue`, `indigo`, `violet`, `purple`, `fuchsia`, `pink`, `rose`, plus semantic tokens `primary`, `secondary`, `success`, `warning`, `error`, `danger`, `info`.

**Shades:** `50`, `100`, `200`, `300`, `400`, `500`, `600`, `700`, `800`, `900`, `950`.

Color properties: `bg`, `color`, `border_color`, `outline_color`, `ring_color`, `ring_offset_color`, `divide_color`.

#### Floats (Numeric)

Numeric properties accept integers (auto-coerced to `f32`) and float literals.

```rust
gap: 16          // int → 16.0f32
opacity: 0.5     // float as-is
grow: 1           // flex_grow + flex_basis: Px(0)
z_index: 10
```

Float properties: `gap`, `cross_gap`, `grow`, `opacity`, `line_height`, `letter_spacing`, `z_index`, `order`, `flex_shrink`, `aspect_ratio`, `filter_blur`, `filter_brightness`, `filter_contrast`, `filter_grayscale`, `filter_invert`, `filter_saturate`, `filter_sepia`, `filter_hue_rotate`, `backdrop_blur`, `outline_width`, `outline_offset`, `ring_width`, `ring_offset`, `divide_width`, `transition_duration`, `transition_delay`.

#### Named Floats

`font_size` and `border_radius` support named size tokens in addition to numeric values.

```rust
// Named tokens
font_size: sm        // 14.0
font_size: xl        // 20.0
border_radius: lg    // 12.0
border_radius: full  // 9999.0

// Numeric fallback
font_size: 18
border_radius: 6
```

**Font size scale:** `xxs` (10), `xs` (12), `sm` (14), `md` (16), `lg` (18), `xl` (20), `xxl` (24), `xxxl` (30).

**Border radius scale:** `sm` (4), `md` (8), `lg` (12), `xl` (16), `full` (9999).

#### Edge Floats

Padding, margin, and border width accept uniform values or compound `{x:, y:}` shorthands.

```rust
// Uniform (all sides)
padding: 16
margin: 8

// Axis shorthand
padding: {x: 24, y: 16}
margin: {y: 8}

// Individual sides
padding: {top: 16, bottom: 8, left: 24, right: 24}
```

Edge float properties: `padding`, `margin`, `border_width`.

#### Dimensions

Width and height properties accept pixels, fractions (percentage), and `Dimension` expressions.

```rust
width: 200          // Dimension::Px(200.0)
height: 60
width: 2/3          // Dimension::Pct(66.67%) — fraction syntax
min_width: 0
max_height: 400
flex_basis: 100     // Dimension::Px(100.0)
```

Dimension properties: `width`, `height`, `min_width`, `max_width`, `min_height`, `max_height`, `flex_basis`.

#### Enums

Enum properties accept snake_case variant names — the macro resolves them to the fully qualified Rust enum at compile time.

```rust
// Layout
align_items: center          // AlignItems::Center
justify_content: space_between  // JustifyContent::SpaceBetween
flex_direction: column       // FlexDirection::Column
flex_wrap: wrap              // FlexWrap::Wrap
overflow: hidden             // Overflow::Hidden
display: flex                // Display::Flex
position: absolute           // Position::Absolute

// Typography
font_weight: bold            // FontWeight::Bold
font_style: italic           // FontStyle::Italic
text_align: center           // TextAlign::Center
text_decoration: underline   // TextDecoration::Underline
text_overflow: ellipsis      // TextOverflow::Ellipsis

// Visual
cursor: pointer              // Cursor::Pointer
visibility: hidden           // Visibility::Hidden
border_style: dashed         // Edges::all(BorderStyle::Dashed)
outline_style: solid         // BorderStyle::Solid
pointer_events: none         // PointerEvents::None

// Transitions
transition_easing: ease_in_out   // Easing::EaseInOut
transition_behavior: allow_discrete  // TransitionBehavior::AllowDiscrete
```

#### Booleans

```rust
focusable: true
disabled: true
```

#### Events

```rust
on_click: "submit_form"     // EventHandler::event("submit_form")
set_on_click: self.handler   // direct expression
```

#### Style Override

Replace a node's entire style with a precomputed `Style` object:

```rust
el { style: skin.main,
    text { style: skin.title, "Hello" }
}
```

#### Border Compound

Per-side border configuration using compound syntax:

```rust
border_bottom: {width: 1, color: slate.700}
border_top: {width: 2, color: red.500}
```

### Shorthand Aliases

Tailwind-style abbreviations resolve to their canonical property names:

| Alias | Canonical | Alias | Canonical |
|-------|-----------|-------|-----------|
| `w` | `width` | `blur` | `filter_blur` |
| `h` | `height` | `brightness` | `filter_brightness` |
| `p` | `padding` | `contrast` | `filter_contrast` |
| `m` | `margin` | `grayscale` | `filter_grayscale` |
| `rounded` | `border_radius` | `invert` | `filter_invert` |
| `shrink` | `flex_shrink` | `saturate` | `filter_saturate` |
| `basis` | `flex_basis` | `sepia` | `filter_sepia` |
| `aspect` | `aspect_ratio` | `hue_rotate` | `filter_hue_rotate` |
| `direction` | `flex_direction` | `outline` | `outline_width` |
| `items` | `align_items` | `ring` | `ring_width` |
| `justify` | `justify_content` | `divide` | `divide_width` |
| `self_align` | `align_self` | | |

### Bare Flags

Three typography shortcuts can be used as bare flags (no value needed):

```rust
text { bold, "Important" }        // font_weight: FontWeight::Bold
text { italic, "Emphasis" }       // font_style: FontStyle::Italic
text { underline, "Link text" }   // text_decoration: TextDecoration::Underline
```

## Children

Children appear after properties inside a tag's braces. Four kinds of children:

### Text Content

String literals become text nodes. Inside a `text` tag, they set the text directly. Inside container tags, they create child text nodes.

```rust
// Direct text on text node
text { "Hello, world!" }

// Text children on containers create child text nodes
vbox {
    "First paragraph"
    "Second paragraph"
}
```

### Nested Elements

```rust
vbox {
    hbox { gap: 8,
        text { "Left" }
        el { grow: 1 }      // spacer
        text { "Right" }
    }
}
```

### Expression Children

Braced expressions inject dynamic children. The expression must implement `IntoChildren`.

```rust
vbox {
    { self.header_nodes }
    text { "Static content" }
    { build_footer() }
}
```

### String Interpolation

Strings with `{expr}` placeholders use Rust's `format!` under the hood. Simple idents use native capture syntax; complex expressions (field access, operators) are extracted as positional arguments.

```rust
text { "{count}" }                    // simple ident capture
text { "{self.name}" }                // field access → positional arg
text { "Order #{i + 1}" }            // expression → positional arg
text { "{order.customer}: {order.amount}" }  // multiple interpolations
```

Escaped braces (`{{` / `}}`) produce literal braces:

```rust
text { "Use {{braces}} for literals" }  // renders: Use {braces} for literals
```

## Control Flow

Control flow constructs work directly inside `ui!` — no escaping to imperative code. When any child uses control flow, the macro switches from static `.child()` chains to `Vec<Node>` accumulation.

### `for` Loops

```rust
vbox {
    for item in &self.items {
        text { "{item.name}" }
    }
}

// Tuple destructuring
vbox {
    for (i, product) in self.products.iter().enumerate() {
        hbox { gap: 8,
            text { color: slate.500, "#{i + 1}" }
            text { color: slate.100, "{product.name}" }
        }
    }
}
```

### `if` / `else`

```rust
vbox {
    if self.loading {
        spinner {}
    } else {
        text { "Content loaded" }
    }
}

// Without else
vbox {
    if self.show_badge {
        badge { color: red.500, "New" }
    }
}

// else if chains
vbox {
    if count == 0 {
        text { "Empty" }
    } else if count == 1 {
        text { "One item" }
    } else {
        text { "{count} items" }
    }
}
```

### `match`

```rust
vbox {
    match self.status {
        Status::Loading => text { "Loading..." },
        Status::Error => text { color: red.500, "Error occurred" },
        Status::Ready => {
            text { "Ready" }
            button { on_click: "start", "Begin" }
        }
    }
}
```

Match arms with multiple children use braces. Guards are supported:

```rust
match value {
    n if n > 100 => text { color: green.500, "High" },
    n if n > 50 => text { color: amber.500, "Medium" },
    _ => text { color: red.500, "Low" }
}
```

### Control Flow in Text Nodes

Control flow also works inside `text` nodes for building dynamic strings:

```rust
text {
    "Items: "
    for item in &self.items {
        "{item.name}, "
    }
}
```

### Values as Expressions

Properties also accept `if` and `match` as value expressions (not children). This is useful for computed colors, sizes, and other properties:

```rust
hbox {
    bg: if dark { gray.800 } else { white },
    color: match priority {
        "high" => red.500,
        "medium" => amber.500,
        _ => slate.500,
    },
}
```

## Interaction Variants

Style changes for hover, pressed, focused, and disabled states use compound value blocks:

```rust
el {
    bg: blue.500, border_radius: 8, padding: {x: 16, y: 8},
    hover: { bg: blue.600, opacity: 0.9 },
    pressed: { bg: blue.700 },
    focused: { ring_width: 2, ring_color: blue.300 },
    disabled_style: { opacity: 0.5 },
}
```

Variant blocks accept the same DSL properties as the parent — colors, enums, named sizes, aliases, all of it. They compile to `Style` objects passed to the node's builder methods.

`disabled` has dual behavior: `disabled: true` sets the boolean flag, `disabled: { ... }` is shorthand for `disabled_style: { ... }`.

## Component Resolution

Any tag name that isn't a built-in tag is resolved as a component. The macro converts the `snake_case` tag to `PascalCase`, instantiates it via `Default::default()`, assigns attributes as fields, and calls `Component::render()`.

```rust
// tag `badge` → type `Badge`
badge { color: green.500, "Online" }

// tag `stat_card` → type `StatCard`
stat_card { title: "Revenue", value: "$48,200" }

// tag `text_input` → type `TextInput`
text_input {
    placeholder: "Search...",
    value: "{self.query}",
    on_change: "query_changed",
}
```

The generated code:

```rust
{
    let mut __comp = Badge::default();
    __comp.color = /* resolved color */;
    __comp.children = vec![Node::text_node().set_text("Online")];
    Component::render(__comp)
}
```

Component attribute values get DSL resolution: string literals matching color tokens resolve to `Color`, named colors resolve to constants, and format strings use `.into()`.

### Icon Component

The `icon` tag has special handling for dead-code-elimination (DCE). Static icon names resolve to `&'static IconData` references at compile time — only referenced icons end up in the binary.

```rust
// Static resolution (DCE-friendly, compile-time)
icon { name: "play", size: 18.0, color: green.400 }
// → __comp.icon = &::dija::icons::regular::PLAY;

// With weight
icon { name: "heart", weight: "bold", size: 24.0 }
// → __comp.icon = &::dija::icons::bold::HEART;

// Dynamic resolution (needs `icon-lookup` feature)
icon { name: icon_name, size: 18.0 }
// → ::dija::icons::lookup(icon_name, weight)
```

## Codegen Modes

The macro uses two codegen strategies, chosen automatically:

### Static Mode (default)

When all children are static (no `for`/`if`/`match`), the macro generates a chain of `.child()` calls with zero allocation overhead:

```rust
// Input
vbox { gap: 8,
    text { "Hello" }
    text { "World" }
}

// Generated (simplified)
Node::vbox()
    .gap(8.0f32)
    .child(Node::text_node().set_text("Hello"))
    .child(Node::text_node().set_text("World"))
```

### Dynamic Mode (automatic)

When any child uses control flow, the macro switches to `Vec<Node>` accumulation:

```rust
// Input
vbox {
    for item in items {
        text { "{item}" }
    }
}

// Generated (simplified)
{
    let mut __children: Vec<Node> = Vec::new();
    for item in items {
        __children.push(Node::text_node().set_text(&format!("{item}")));
    }
    Node::vbox().with_children(__children)
}
```

## Full Example: Dashboard Card

Putting it all together — a dashboard card with layout, typography, colors, control flow, interpolation, and interaction variants:

```rust
ui!(vbox { bg: slate.800, rounded: lg, p: 16, gap: 12, overflow: hidden,
    // Header
    hbox { items: center, gap: 8,
        icon { name: "chart_bar", size: 18.0, color: blue.400 }
        text { color: slate.200, font_size: lg, bold, "Revenue" }
        el { grow: 1 }
        badge {
            color: if self.trend > 0.0 { green.500 } else { red.500 },
            "{self.trend}%"
        }
    }

    // Value
    text { color: white, font_size: xxxl, bold, "${self.total}" }

    // Breakdown
    vbox { gap: 4,
        for item in &self.breakdown {
            hbox { gap: 8, items: center, p: {y: 4},
                border_bottom: {width: 1, color: slate.700/50},
                text { color: slate.300, grow: 1, "{item.label}" }
                text {
                    color: match item.change.signum() {
                        1 => green.400,
                        -1 => red.400,
                        _ => slate.400,
                    },
                    "{item.amount}"
                }
            }
        }
    }

    // Footer
    hbox { justify: end,
        el {
            bg: blue.500, rounded: md, p: {x: 12, y: 6},
            hover: { bg: blue.600 },
            pressed: { bg: blue.700 },
            text { color: white, font_size: sm, "View Details" }
        }
    }
})
```

## Comparison with Tailwind CSS

| Tailwind | Dija `ui!` | Notes |
|----------|-----------|-------|
| `class="flex gap-4"` | `hbox { gap: 4 }` | Structural, not string-based |
| `class="bg-blue-500"` | `bg: blue.500` | Dot notation for shade |
| `class="text-white"` | `color: white` | Named colors |
| `class="text-lg"` | `font_size: lg` | Same size scale |
| `class="rounded-lg"` | `rounded: lg` | Alias for `border_radius` |
| `class="p-4"` | `p: 4` | Shorthand alias |
| `class="px-6 py-3"` | `p: {x: 6, y: 3}` | Compound value |
| `class="w-2/3"` | `w: 2/3` | Fraction syntax for percentages |
| `class="font-bold"` | `bold` | Bare flag |
| `class="hover:bg-blue-600"` | `hover: { bg: blue.600 }` | Variant block |
| `class="opacity-50"` | `opacity: 0.5` | Direct float value |
| `class="blur-sm"` | `blur: 4` | Alias for `filter_blur` |
| `class="border-dashed"` | `border_style: dashed` | Enum resolution |

Key differences from Tailwind:

- **Typed at compile time** — invalid properties, unknown enums, and type mismatches are compiler errors, not silent CSS typos.
- **Structural** — `vbox`/`hbox` define layout direction explicitly instead of combining `flex` + `flex-col` classes.
- **No purging needed** — only referenced code compiles in. Dead code elimination is native.
- **Values, not class names** — `gap: 16` is a value, not a mapped class like `gap-4`. You can use any number, not just the spacing scale.
- **Expressions inline** — `color: if dark { white } else { black }` works directly. No `dark:text-white` variant prefix system.
