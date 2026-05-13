---
name: export-delivery-workflow
description: Handles export-and-delivery tasks for design outputs. Use when user asks to export screens, bundle outputs, verify files, and report final artifact paths.
---

# Export Delivery Workflow

## Scope

Use this workflow for producing final export files and handing off paths.

## Steps

1. Confirm source file and requested format.
2. Ensure output directory exists before export.
3. Export target node IDs with explicit settings.
4. Verify generated files exist and are non-empty.
5. Return absolute output paths and artifact count.

## Defaults

- Prefer PNG for single-screen image output.
- Prefer PDF for multi-screen shareable output.
- Keep output in project-local `exports` unless user specifies another path.

## Validation

- If export succeeds but file missing, re-run verification and report mismatch.
- If export fails, return exact error and one concrete retry command.
