---
name: pencil-workflow
description: Operates on .pen design files through Pencil MCP tools for export and structure inspection. Use when user asks about .pen editing, node lookup, screenshot checks, or exporting PNG/JPEG/WEBP/PDF.
---

# Pencil Workflow

## Scope

Use this skill for `.pen` design tasks in this project.

## Rules

1. Never read `.pen` contents with generic file readers.
2. Use Pencil MCP tools for all `.pen` operations.
3. Start with `get_editor_state(include_schema: true)` when context is unclear.
4. For export tasks, use `export_nodes` with explicit `filePath`, `outputDir`, and `nodeIds`.
5. For discovery tasks, use `batch_get` with low `readDepth` first, then narrow.
6. Prefer existing top-level frame IDs for full-screen exports.

## Quick Workflow

1. Confirm target file path.
2. Create/confirm export directory.
3. Read top-level nodes from `get_editor_state` or `batch_get`.
4. Call `export_nodes` with target format.
5. Verify generated files exist in output directory.

## Export Presets

- Single frame PNG: one `nodeId`, `format: "png"`.
- Multi-frame PDF: multiple `nodeIds`, `format: "pdf"`.
- Bulk image export: multiple `nodeIds`, `format: "png"` or `"jpeg"`.

## Response Style

- Keep answers concise and operational.
- Always return output path(s) after export.
- If a tool is unavailable, provide the exact fallback command or next action.
