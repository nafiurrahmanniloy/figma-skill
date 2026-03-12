# Figma Skill for Claude Code

A universal Figma-to-code skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Browse Figma files, download assets, extract design tokens, and generate production-ready code for 7 frameworks — all from your terminal.

## Features

- **Browse & Inspect** — Navigate Figma file trees, inspect any frame or component
- **Download Assets** — Export PNG and SVG images at any scale (1x, 2x, 3x)
- **Extract Design Tokens** — Auto-extract colors, typography, spacing, shadows, gradients into CSS, Tailwind, JSON, or SCSS
- **Generate Code** — Convert Figma layouts to code for Tailwind, React, Vue, Svelte, React Native, Flutter, or plain CSS
- **Zero Dependencies** — Python scripts use only the standard library (no pip install needed)

## Supported Frameworks

| Framework | Output |
|-----------|--------|
| Tailwind | HTML + Tailwind utility classes |
| React | JSX component + Tailwind |
| Vue | Single File Component (SFC) |
| Svelte | Svelte component |
| React Native | Component + StyleSheet |
| Flutter | Dart StatelessWidget |
| CSS | HTML + plain CSS classes |

## Quick Install

### 1. Clone this repo

```bash
git clone https://github.com/nafiurrahmanniloy/figma-skill.git
```

### 2. Copy the skill folder into your project

```bash
cp -r figma-skill/figma your-project/.claude/skills/figma
```

Your project should look like:

```
your-project/
├── .claude/
│   └── skills/
│       └── figma/          <-- this folder
│           ├── SKILL.md
│           ├── scripts/
│           │   ├── extract_tokens.py
│           │   └── figma_to_code.py
│           └── data/
│               └── framework-mappings.json
├── .mcp.json               <-- add Figma MCP config here
└── ... your code
```

### 3. Configure the Figma MCP server

Copy `.mcp.json.example` or add this to your project's `.mcp.json`:

```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--stdio"],
      "env": {
        "FIGMA_API_KEY": "your-figma-api-key"
      }
    }
  }
}
```

### 4. Get your Figma API key

1. Go to [Figma Developer Settings](https://www.figma.com/developers/api#access-tokens)
2. Click **"Create a new personal access token"**
3. Copy the token and paste it as `FIGMA_API_KEY` in `.mcp.json`

### 5. Reload

- **VS Code**: Run "Developer: Reload Window" from the command palette
- **CLI**: Restart Claude Code

That's it. Say `/figma` in Claude Code to start using the skill.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (VS Code extension or CLI)
- [Node.js](https://nodejs.org/) 18+ (for the `figma-developer-mcp` server via npx)
- [Python](https://www.python.org/) 3.8+ (for token extraction and code generation scripts)
- A [Figma](https://www.figma.com/) account with API access

## Usage Examples

### Browse a Figma file

```
"Browse my Figma file: https://www.figma.com/design/ABC123/MyDesign"
```

Claude will extract the file key, fetch the structure, and show you all pages, frames, and components.

### Download assets

```
"Download the hero image and logo from my Figma file as PNG and SVG"
```

### Extract design tokens

```
"Extract all design tokens from this Figma file and output as Tailwind config"
```

Generates a ready-to-paste `theme.extend` block with colors, fonts, shadows, and border-radius from your design.

### Generate a React component

```
"Convert the Hero Section frame to a React component"
```

Produces a JSX component with Tailwind classes matching your Figma layout, spacing, colors, and typography.

### Full pipeline

```
"Take this Figma file, extract the design tokens as CSS variables, then convert the Card component to Vue"
```

## Token Output Formats

| Format | Command | Output |
|--------|---------|--------|
| CSS | `--format css` | `:root { --color-primary: #3B82F6; ... }` |
| Tailwind | `--format tailwind` | `module.exports = { theme: { extend: { ... } } }` |
| JSON | `--format json` | `{ "colors": { "primary": "#3B82F6" } }` |
| SCSS | `--format scss` | `$color-primary: #3B82F6;` |

## How It Works

This skill combines two pieces:

1. **Figma MCP Server** (`figma-developer-mcp`) — Connects Claude Code to the Figma API, providing `get_figma_data` and `download_figma_images` tools
2. **Python Scripts** — Process the raw Figma JSON into usable tokens and code:
   - `extract_tokens.py` — Walks the node tree, finds colors/fonts/spacing/shadows, outputs in 4 formats
   - `figma_to_code.py` — Reads node structure (auto-layout, fills, effects) and generates framework-specific code using lookup tables from `framework-mappings.json`

## File Structure

```
figma/
├── SKILL.md                        # Skill entry point (Claude reads this)
├── scripts/
│   ├── extract_tokens.py           # Design token extractor (4 output formats)
│   └── figma_to_code.py            # Code generator (7 frameworks)
└── data/
    └── framework-mappings.json     # Figma property → framework lookup tables
```

## Contributing

Contributions are welcome! Some ideas:

- Add more frameworks (Angular, Solid, etc.)
- Improve Tailwind class matching accuracy
- Add responsive breakpoint detection from Figma variants
- Support Figma variables/design tokens API
- Add component composition (nested component references)

## License

[MIT](LICENSE)

---

Built for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) by the community.
