---
name: line-history
description: Show git history, related files, and commit context for specific lines in a file using context-pilot. Use when user wants to understand the history of code, find related files, or see what commits touched specific lines.
argument-hint: <filepath> <start-line> <end-line>
allowed-tools: Bash, Read
---

# Line History with Context Pilot

Analyze the git history and find related files for a specific line range using context-pilot.

## Arguments

- `$0` - File path (relative or absolute)
- `$1` - Start line number
- `$2` - End line number

## Steps

### 1. Validate Arguments

Ensure all three arguments are provided. If not, inform the user:
```
Usage: /line-history <filepath> <start-line> <end-line>
Example: /line-history src/db.rs 100 150
```

### 2. Check if contextpilot is Installed

Check if the `contextpilot` binary is available:

```bash
which contextpilot 2>/dev/null
```

If `contextpilot` is not found, clone and install it:

```bash
# Clone the repository to a temporary location and install
git clone https://github.com/krshrimali/context-pilot-rs.git /tmp/context-pilot-rs && cd /tmp/context-pilot-rs && cargo install --path .
```

Inform the user that context-pilot is being installed (this is a one-time setup).

### 3. Check if Workspace is Indexed

Check if the context-pilot database exists for this workspace:

```bash
# The database is stored in ~/.context_pilot_db/<workspace_path>/
ls ~/.context_pilot_db/ 2>/dev/null
```

If the workspace is not indexed, automatically index it first:

```bash
contextpilot $(pwd) -t index
```

Inform the user that indexing is happening (it may take a moment for large repos).

### 4. Query Related Files

IMPORTANT: The file path passed to contextpilot for query/desc must be an **absolute path**. Convert the user-provided path to absolute before running:

```bash
# Convert relative path to absolute using realpath
contextpilot $(pwd) -t query -s $1 -e $2 $(realpath $0)
```

Note: The file is a positional argument (not a `-f` flag). It comes after all options.

This returns files ranked by how often they appeared in commits that touched the specified lines.

### 5. Get Commit Descriptions

Run the descriptions command to get commit context (also using absolute path):

```bash
contextpilot $(pwd) -t desc -s $1 -e $2 $(realpath $0)
```

This returns commit messages that explain why those lines were changed.

### 6. Present Results

Format the output clearly:

**Related Files** (ranked by relevance):
- List files with their occurrence count
- Explain that higher counts mean stronger contextual relationship

**Commit Context**:
- Show relevant commit descriptions
- Highlight key changes and their rationale

**Suggestions**:
- If the user wants to explore further, suggest reading the top related files
- Mention they can run `/line-history` on those files too
