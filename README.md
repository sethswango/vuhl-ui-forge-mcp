# VuhluiForge MCP

`VuhluiForge MCP` is the MCP-focused companion to the `VuhluiForge` app fork.

Its goal is to turn screenshot-driven UI generation into a context-aware workflow that works well from Cursor, Claude Code, and related IDE-driven tooling, with special attention to Angular integration.

## Project Intent

This repo exists to support a workflow like this:

1. Gather project context from the target codebase
2. Capture design input from a screenshot or mockup
3. Generate implementation variants with the right stack and constraints
4. Return code that can slot into an existing component structure, style system, and service layer

The long-term emphasis is not just "screenshot to code", but "screenshot to code that fits the project it is being added to".

## Current Local State

This local snapshot is intentionally preserved and publishable, but it is still a scaffold rather than a complete implementation.

Currently present:

- package metadata and lockfile
- TypeScript and Vite configuration
- MCP/server-oriented README and project framing
- installed dependencies in `node_modules/`

Not currently present in this local snapshot:

- the documented `src/server/` implementation
- the documented `src/ui/` implementation
- built output under `dist/`

Because of that, this repo should be read as the current MCP contract and scaffold, not as a fully rehydrated runnable implementation tree.

## Naming

- Display name: `VuhluiForge MCP`
- Personal repo target: `https://github.com/sethswango/vuhl-ui-forge-mcp`
- PDT repo target: `https://github.com/vu-pdt/VUHL-UI-Forge-MCP`
- npm package: `vuhl-ui-forge`
- CLI command: `vuhl`
- MCP server id example: `vuhl-ui-forge`

## Intended Modes

### HTTP Mode

Serve a browser UI for design iteration and preview.

```bash
npx vuhl-ui-forge
```

Default URL:

- `http://localhost:3001`

### Stdio Mode

Expose the tool as an MCP server for IDE clients.

```bash
npx vuhl-ui-forge --stdio
```

## MCP Client Configuration

Example configuration for Cursor or Claude Desktop:

```json
{
  "mcpServers": {
    "vuhl-ui-forge": {
      "command": "npx",
      "args": ["vuhl-ui-forge", "--stdio"]
    }
  }
}
```

## Context-Aware Generation Model

The MCP is meant to do more than generate generic markup. Before invoking generation, the client should gather context from the target codebase such as:

- Angular version
- selector prefix conventions
- CSS variables or design tokens
- shared components already available
- injectable services likely needed by the new component
- feature-specific intent, inputs, and outputs

That context should inform:

- output stack selection
- component naming
- selector naming
- service usage
- styling choices
- integration instructions

## Angular-Focused Workflow

For Angular-oriented use cases, the preferred workflow is:

1. Inspect the target repo's `package.json` to determine Angular version.
2. Read shared styles to identify variables, tokens, and theme patterns.
3. Inspect existing components to infer selector prefixes and template conventions.
4. Identify candidate shared components and services before generating new files.
5. Generate code with both `projectContext` and `featureContext`, not just an image.

This is the core differentiator for VuhluiForge MCP versus a generic screenshot-to-code experience.

## Development Notes

The committed config currently expects a structure like this once the implementation tree is restored:

```text
src/
├── server/
│   ├── index.ts
│   ├── routes/
│   ├── tools/
│   └── lib/
└── ui/
    ├── App.tsx
    └── components/
```

Existing scripts:

```bash
npm run dev
npm run build
npm run start
npm run start:http
npm run start:stdio
```

Those commands depend on the `src/` implementation tree being present.

## Publishing Notes

This repo is the MCP publication target.

- Personal GitHub target: `sethswango/vuhl-ui-forge-mcp`
- Work GitHub target: `vu-pdt/VUHL-UI-Forge-MCP`

The app-side repo is separate and should remain under the personal `VuhluiForge` fork path.

## Related Docs

- `C:\dev\Screenshot-To-Code\README.md`
- `C:\dev\Obsidian_Notes\VU-Obsidian\Projects\screenshot-to-code-mcp\screenshot-to-code-mcp.md`
- `C:\dev\Obsidian_Notes\VU-Obsidian\Projects\VUHL UI Forge\VUHL UI Forge Status.md`
