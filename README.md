<div align="center">

# Beyond Horizon

**A readability-first dark theme for [Zed](https://zed.dev), built on the Horizon palette and tuned for semantic tokens.**

![Dark](https://img.shields.io/badge/appearance-dark-1C1E26?style=flat-square)
![Zed](https://img.shields.io/badge/editor-Zed-fe5e78?style=flat-square)
![Semantic tokens](https://img.shields.io/badge/LSP-semantic%20tokens-b877db?style=flat-square)
![Contrast](https://img.shields.io/badge/code%20contrast-%E2%89%A5%204.8%3A1-9ad479?style=flat-square)

</div>

<!-- Replace docs/preview.png with a screenshot of the theme in Zed (about 1600x1000, PNG) -->
<p align="center">
  <img width="900"  alt="Beyond Horizon theme preview" src="https://github.com/user-attachments/assets/0186fc7b-1692-4595-ba83-81bd33538dcb" />
</p>

---

## Why

Horizon's warm pink-and-teal look is great, but a straight port to Zed loses things: variables and `use` paths share a colour, ghost text and line numbers nearly vanish, and colours shift when LSP tokens load. Beyond Horizon keeps the identity and fixes the rest.

- **Readable first.** Every code colour is at least 4.8:1 against the background. Comments sit at 3.4:1 and doc comments at 5.2:1, so docs stand out from commented-out code.
- **Calm palette.** One colour per role, and the warm tones are collapsed to two (coral and peach) so nothing looks like a near-duplicate.
- **No flicker.** Tree-sitter and semantic tokens resolve to the same colour, so nothing changes when the language server finishes loading.
- **Weight where it helps.** Function definitions are semibold, headings and strong text are bold, and everything else stays regular.
- **Complete.** Git and diff colours, search matches, vim modes, rainbow brackets, 8 player colours, a full terminal palette and every Zed UI surface are covered.

## Install

Copy `beyond-horizon.json` into your Zed themes folder:

| OS | Folder |
| --- | --- |
| macOS / Linux | `~/.config/zed/themes/` |
| Windows | `%APPDATA%\Zed\themes\` |

Then pick it with `theme selector: toggle` from the command palette, or set it in `settings.json`:

```json
{
  "theme": "Beyond Horizon"
}
```

## Recommended settings

The theme looks right with defaults, but it is designed for semantic tokens in `combined` mode. Merge this into your `settings.json`:

```jsonc
{
  "theme": "Beyond Horizon",
  "semantic_tokens": "combined",
  "colorize_brackets": true,
  //"indent_guides": { "enabled": true, "coloring": "indent_aware" },
  "inlay_hints": { "enabled": true },
  "global_lsp_settings": {
    "semantic_token_rules": [
      { "token_type": "function", "token_modifiers": ["declaration"], "style": ["function.definition", "function"] },
      { "token_type": "function", "token_modifiers": ["definition"],  "style": ["function.definition", "function"] },
      { "token_type": "method",   "token_modifiers": ["declaration"], "style": ["function.definition", "function"] },
      { "token_type": "method",   "token_modifiers": ["definition"],  "style": ["function.definition", "function"] },
      { "token_type": "type", "token_modifiers": ["defaultLibrary"], "style": ["type.builtin", "type"] },
      { "token_type": "builtinType", "style": ["type.builtin", "type"] }
    ]
  }
}
```

After the first change, restart the language server (`editor: restart language server`).

### Why `combined` and not `full`

`combined` uses the language server's tokens on top of tree-sitter. `full` turns tree-sitter off, so anything the server does not tag (punctuation, JSX tags, markdown, some strings) loses its highlighting.

### Rust `use` paths

Zed's Rust tree-sitter query marks every plain identifier as a variable, so `std` and `collections` in `use std::collections::HashMap` would look like variables. With semantic tokens on, rust-analyzer tags them as namespaces and they get the namespace colour, as in VS Code.

## Palette

| Role | Colour | Hex |
| --- | --- | --- |
| Background | ![](https://img.shields.io/badge/-%20%20%20%20%20-1C1E26?style=flat-square) | `#1C1E26` |
| Panels | ![](https://img.shields.io/badge/-%20%20%20%20%20-1a1c24?style=flat-square) | `#1a1c24` |
| Popups | ![](https://img.shields.io/badge/-%20%20%20%20%20-232530?style=flat-square) | `#232530` |
| Text | ![](https://img.shields.io/badge/-%20%20%20%20%20-D5D8DA?style=flat-square) | `#D5D8DA` |
| Accent, variables | ![](https://img.shields.io/badge/-%20%20%20%20%20-fe5e78?style=flat-square) | `#fe5e78` |
| Properties, tags, headings | ![](https://img.shields.io/badge/-%20%20%20%20%20-e95678?style=flat-square) | `#e95678` |
| Keywords | ![](https://img.shields.io/badge/-%20%20%20%20%20-b877db?style=flat-square) | `#b877db` |
| Functions | ![](https://img.shields.io/badge/-%20%20%20%20%20-25afbc?style=flat-square) | `#25afbc` |
| Types, namespaces | ![](https://img.shields.io/badge/-%20%20%20%20%20-ffd586?style=flat-square) | `#ffd586` |
| Strings | ![](https://img.shields.io/badge/-%20%20%20%20%20-9ad479?style=flat-square) | `#9ad479` |
| Numbers, constants, attributes | ![](https://img.shields.io/badge/-%20%20%20%20%20-f09383?style=flat-square) | `#f09383` |
| Special: `self`, lifetimes, primitives | ![](https://img.shields.io/badge/-%20%20%20%20%20-fab795?style=flat-square) | `#fab795` |
| Operators, punctuation | ![](https://img.shields.io/badge/-%20%20%20%20%20-BBBBBB?style=flat-square) | `#BBBBBB` |
| Doc comments | ![](https://img.shields.io/badge/-%20%20%20%20%20-8d909c?style=flat-square) | `#8d909c` |
| Comments | ![](https://img.shields.io/badge/-%20%20%20%20%20-6e717c?style=flat-square) | `#6e717c` |
| Inlay hints | ![](https://img.shields.io/badge/-%20%20%20%20%20-7b7fa5?style=flat-square) | `#7b7fa5` |

## Typography

- **Italic** is used for keywords, comments, parameters, attributes and `self`. Use a font with a real italic (JetBrains Mono, Fira Code and Cascadia Code all have one).
- **Semibold** is used for function definitions. If your font has no semibold, Zed picks the nearest weight. To turn it off, set `font_weight` to `null` on `function.definition` in the theme.
- If italics feel busy, remove `font_style` from `keyword` first.

## Customising

Override colours without editing the theme file by adding a `theme_overrides` entry keyed by theme name in `settings.json`:

```json
{
  "theme_overrides": {
    "Beyond Horizon": {
      "syntax": {
        "comment": { "color": "#7a7d88" }
      }
    }
  }
}
```

Or edit `beyond-horizon.json` directly. Syntax colours live under `style.syntax`, and rainbow bracket colours under `accents`.

## Credits

Beyond Horizon stands on the work of others:

Horizon by Jonathan Olaleye, the original warm dark theme and the palette this theme is built on (MIT licence).
Horizon Extended by Lance Wilhelm, the VS Code extension of Horizon that this theme follows for syntax colouring.
Horizon Extended for Zed by Lance Wilhelm, the Zed port that Beyond Horizon started from.

Layering, diff and vim colour structure, and the comment hierarchy were checked against Zed's official One, Ayu and Gruvbox themes.

Please keep these credits, and the upstream licence terms, if you share or publish this theme.
