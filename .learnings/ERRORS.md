## [ERR-20260415-001] user-pencil.batch_design.move-binding

**Logged**: 2026-04-15T00:00:00Z
**Priority**: medium
**Status**: pending
**Area**: frontend

### Summary
`batch_design` move operation failed because I used a guessed node id instead of the returned binding id.

### Error
```
Failed to execute operation M("Sr3Rd","HCRS4",5): No such node to move.
All operations in this block have been rolled back.
```

### Context
- Operation attempted in `运营首页.pen` fusion screen edits
- Inserted `foldHint` then tried to move with a hardcoded id
- Correct approach: move using binding `M(foldHint,"HCRS4",5)`

### Suggested Fix
Always use operation bindings from the same `batch_design` block for `M()` targets on newly inserted nodes.

### Metadata
- Reproducible: yes
- Related Files: /Users/mengyao/XQ/设计/运营首页.pen

---
