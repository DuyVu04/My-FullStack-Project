---
name: context-mode
description: >-
  Mandatory routing rules for Antigravity CLI. Invoke when exploring a codebase, reading files for analysis,
  listing context-mode tools, searching, parsing, counting, comparing, summarizing, fetching web content, or running data-heavy commands.
---

# context-mode for Antigravity CLI

context-mode MCP tools are available in agy as `context-mode/<tool>`.
Use these tools directly to save context window and avoid dumping large raw files or logs into the conversation.

## Available Tools

- `context-mode/ctx_execute`: Run JavaScript, TypeScript, Python, shell, or other code in a sandbox. Prints only the final answer.
- `context-mode/ctx_execute_file`: Read one file into `FILE_CONTENT` inside the sandbox and run code over it.
- `context-mode/ctx_batch_execute`: Run multiple repository commands in one batch, index large output, and answer follow-up queries.
- `context-mode/ctx_index`: Store a file, directory, or content in the local FTS5 knowledge base for later search.
- `context-mode/ctx_search`: Search indexed content and captured session memory. Batch related questions in `queries`.
- `context-mode/ctx_fetch_and_index`: Fetch web content, store it, then query with `ctx_search`.
- `context-mode/ctx_stats`: Show context savings and current-session stats.
- `context-mode/ctx_doctor`: Diagnose context-mode runtime and hook health.
- `context-mode/ctx_upgrade`: Provide upgrade or repair guidance.
- `context-mode/ctx_purge`: Purge stored context-mode knowledge after confirmation.

## Best Practices

1. **File Reading for Analysis**:
   - For editing: Use standard `view_file` / `replace_file_content`.
   - For analysis / large logs / search: Use `context-mode/ctx_execute_file` or `context-mode/ctx_execute`.
2. **Web Content**:
   - For large pages or documentation: Use `context-mode/ctx_fetch_and_index` then query with `context-mode/ctx_search`.
