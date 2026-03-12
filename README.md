<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Skill-7C3AED?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJub25lIiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCI+PHBhdGggZD0iTTEyIDJ2MjAiLz48cGF0aCBkPSJNMiAxMmgyMCIvPjwvc3ZnPg==&logoColor=white" alt="Claude Code Skill" />
  <img src="https://img.shields.io/badge/Frameworks-7-10B981?style=for-the-badge" alt="7 Frameworks" />
  <img src="https://img.shields.io/badge/Token_Formats-4-F59E0B?style=for-the-badge" alt="4 Token Formats" />
  <img src="https://img.shields.io/badge/Dependencies-Zero-EF4444?style=for-the-badge" alt="Zero Dependencies" />
  <img src="https://img.shields.io/badge/License-MIT-3B82F6?style=for-the-badge" alt="MIT License" />
</p>

# Figma Skill for Claude Code

> Turn any Figma design into production-ready code — right from your terminal.

A Claude Code skill that connects to the Figma API, intelligently discovers Community resources that match your project, extracts design tokens, and generates framework-specific code. No copy-pasting from Figma. No manual translation. Just describe what you want.

---

## What Can It Do?

```
You:  "Find me a dashboard UI kit that matches my React + Tailwind project,
       extract the tokens, and convert the sidebar component to code."

Claude: *analyzes your project* → *searches Figma Community* → *evaluates top matches*
        → *guides you to duplicate* → *extracts tokens* → *generates React component*
        → *places files in your project following your conventions*
```

### The 6 Workflows

| # | Workflow | What Happens |
|---|---------|-------------|
| 1 | **Browse & Inspect** | Navigate Figma file trees, inspect any frame or component by node ID |
| 2 | **Download Assets** | Export PNG/SVG at 1x, 2x, or 3x — icons, illustrations, photos |
| 3 | **Extract Design Tokens** | Pull colors, typography, spacing, shadows, gradients into CSS, Tailwind, JSON, or SCSS |
| 4 | **Generate Code** | Convert any Figma frame to code in your framework |
| 5 | **Full Pipeline** | Browse → Inspect → Extract → Generate → Download → Integrate, all in one go |
| 6 | **Smart Community Discovery** | AI-powered search of Figma Community — finds the best UI kits for your specific project, evaluates them, retrieves the design data, and adapts it to your codebase |

---

## Supported Frameworks

<table>
<tr>
<td align="center"><strong>Tailwind</strong><br/><sub>HTML + utility classes</sub></td>
<td align="center"><strong>React</strong><br/><sub>JSX + Tailwind</sub></td>
<td align="center"><strong>Vue</strong><br/><sub>Single File Component</sub></td>
<td align="center"><strong>Svelte</strong><br/><sub>Svelte component</sub></td>
</tr>
<tr>
<td align="center"><strong>React Native</strong><br/><sub>Component + StyleSheet</sub></td>
<td align="center"><strong>Flutter</strong><br/><sub>Dart StatelessWidget</sub></td>
<td align="center"><strong>CSS</strong><br/><sub>HTML + plain CSS</sub></td>
<td align="center">-</td>
</tr>
</table>

## Token Output Formats

| Format | Output | Best For |
|--------|--------|----------|
| **CSS** | `:root { --color-primary: #3B82F6; }` | Any web project |
| **Tailwind** | `theme: { extend: { colors: { ... } } }` | Tailwind CSS projects |
| **JSON** | `{ "colors": { "primary": "#3B82F6" } }` | Design systems, Style Dictionary |
| **SCSS** | `$color-primary: #3B82F6;` | SCSS/Sass projects |

---

## Quick Start

### 1. Clone

```bash
git clone https://github.com/nafiurrahmanniloy/figma-skill.git
```

### 2. Copy into your project

```bash
cp -r figma-skill/figma your-project/.claude/skills/figma
```

Your project structure:

```
your-project/
├── .claude/
│   └── skills/
│       └── figma/              # <-- this skill
│           ├── SKILL.md
│           ├── scripts/
│           │   ├── extract_tokens.py
│           │   └── figma_to_code.py
│           └── data/
│               └── framework-mappings.json
├── .mcp.json                   # <-- Figma MCP config
└── ... your code
```

### 3. Add the Figma MCP server

Copy `.mcp.json.example` or add to your project's `.mcp.json`:

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

1. Open [Figma Developer Settings](https://www.figma.com/developers/api#access-tokens)
2. Click **"Create a new personal access token"**
3. Paste it as `FIGMA_API_KEY` in `.mcp.json`

### 5. Reload & go

- **VS Code** — `Cmd+Shift+P` → "Developer: Reload Window"
- **CLI** — Restart Claude Code

Say `/figma` and start designing with code.

---

## Usage Examples

### Browse a Figma file
```
"Browse my Figma file: https://www.figma.com/design/ABC123/MyDesign"
```
Claude extracts the file key, fetches the structure, and shows you every page, frame, and component.

### Download assets
```
"Download the hero image and logo as PNG @2x and SVG"
```

### Extract design tokens
```
"Extract all design tokens from this Figma file as Tailwind config"
```
Outputs a ready-to-paste `theme.extend` block with your design's colors, fonts, shadows, and radii.

### Generate a component
```
"Convert the Hero Section frame to a React component"
```
Produces a JSX component with Tailwind classes matching your Figma layout, spacing, colors, and typography.

### Smart Community discovery
```
"I'm building a fintech dashboard in React. Find me the best UI kit from Figma Community."
```
Claude reads your project context, runs targeted searches, evaluates the top results, and walks you through retrieving and integrating the best match.

### Full pipeline
```
"Take this Figma file, extract the tokens as CSS variables, convert the Card component to Vue, and download the icons as SVG"
```

---

## How It Works

```
┌──────────────┐     ┌─────────────────────┐     ┌──────────────────┐
│  Figma API   │────▶│  figma-developer-mcp │────▶│   Claude Code    │
│  (designs)   │     │  (MCP server)        │     │   (with skill)   │
└──────────────┘     └─────────────────────┘     └────────┬─────────┘
                                                          │
                                                          ▼
                                               ┌──────────────────┐
                                               │  Python Scripts   │
                                               │                  │
                                               │  extract_tokens  │
                                               │  figma_to_code   │
                                               └────────┬─────────┘
                                                        │
                                          ┌─────────────┼─────────────┐
                                          ▼             ▼             ▼
                                    ┌──────────┐ ┌──────────┐ ┌──────────┐
                                    │  Tokens  │ │   Code   │ │  Assets  │
                                    │ CSS/TW/  │ │ React/   │ │ PNG/SVG  │
                                    │ JSON/SCSS│ │ Vue/etc  │ │ @1x-3x   │
                                    └──────────┘ └──────────┘ └──────────┘
```

**Two core pieces:**

1. **Figma MCP Server** (`figma-developer-mcp`) — Gives Claude direct access to the Figma API via `get_figma_data` and `download_figma_images`
2. **Python Scripts** (zero dependencies) — Transform raw Figma JSON into usable output:
   - `extract_tokens.py` — Walks the node tree, finds colors, fonts, spacing, shadows, gradients. Outputs 4 formats.
   - `figma_to_code.py` — Reads auto-layout, fills, effects, strokes. Generates framework-specific code using lookup tables.

---

## File Structure

```
figma/
├── SKILL.md                        # Skill instructions (6 workflows, conversion tables)
├── scripts/
│   ├── extract_tokens.py           # Design token extractor
│   └── figma_to_code.py            # Code generator (7 frameworks)
└── data/
    └── framework-mappings.json     # Figma property → framework lookup tables
```

---

## Requirements

| Requirement | Version | Why |
|-------------|---------|-----|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Latest | VS Code extension or CLI |
| [Node.js](https://nodejs.org/) | 18+ | Runs the `figma-developer-mcp` server via npx |
| [Python](https://www.python.org/) | 3.8+ | Token extraction & code gen (stdlib only) |
| [Figma](https://www.figma.com/) | Account | With API access for personal access token |

---

## Contributing

Contributions welcome! Ideas:

- Add frameworks (Angular, Solid, Qwik)
- Improve Tailwind class matching accuracy
- Add responsive breakpoint detection from Figma variants
- Support Figma Variables / Design Tokens API
- Add nested component composition
- Improve Community discovery search heuristics

---

## License

[MIT](LICENSE)

---

<p align="center">
  Built for <a href="https://docs.anthropic.com/en/docs/claude-code">Claude Code</a> by <a href="https://github.com/nafiurrahmanniloy">Nafiur Rahman Niloy</a>
</p>
