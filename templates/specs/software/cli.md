---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

The target command-line interface surface for <system or scope>, covering commands, subcommands, flags, arguments, output formats, exit codes, and error conditions.

## Command Tree

<!-- One fenced block per command group, showing the full hierarchy with one-line descriptions. This block is the authoritative index; every command listed here must have a corresponding per-command section below or in a linked file. -->

```
<command>        <one-line description>
  <subcommand>   <one-line description>
  <subcommand>   <one-line description>
```

## Commands

<!-- One H3 block per command or subcommand. Each block contains the subsections below in the order shown. Omit Arguments or Flags only when the command accepts none; all other subsections are required. -->

### `<command>`

<One or two sentences stating what the command does.>

**Usage**

```
<command> [options] [args]
```

**Arguments**

<!-- Omit this subsection when the command accepts no positional arguments. -->

| Argument | Required | Description |
|----------|----------|-------------|
| `<arg>` | yes / no | <what the argument represents> |

**Flags**

<!-- Omit this subsection when the command accepts no flags. -->

| Flag | Short | Type | Default | Description |
|------|-------|------|---------|-------------|
| `--<flag>` | `-<x>` | <type> | <default or none> | <what the flag does> |

**Output**

<!-- One paragraph per output mode offered by this command. For `--json` output that produces a non-trivial object or array, pair this spec with a JSON Schema (Draft 2020-12) file at `specs/cli/schemas/<command>-output.schema.yaml` and reference it here. Inline schema is acceptable for simple scalar or two-field outputs. -->

Human-readable: <describe the default human-readable output format and content.>

`--json`: <describe the structured output shape; reference the paired JSON Schema file if one exists.>

`--quiet`: <describe what is suppressed and what, if anything, is still emitted.>

**Exit Codes**

| Code | Meaning |
|------|---------|
| `0` | Success |
| `1` | <error condition> |
| `<n>` | <error condition> |

**Errors**

| Condition | Exit Code | Message |
|-----------|-----------|---------|
| <condition> | `<n>` | `<message text or pattern>` |

## Rationale

<!-- Include only where the design makes a choice the requirement leaves open. One line per non-obvious decision. -->

- <design choice>: <one-line reason>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
