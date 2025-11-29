# LiteDB Advance MCP Server (`litedb-adv-mcp`)

Production-grade **Model Context Protocol (MCP)** server for **LiteDB v5**, written in **C# 13 / .NET 9**.

This server exposes LiteDB as a rich MCP surface for LLM tooling (Cursor, Cline, Claude Code, MCP Inspector), including:

- Admin / database tools (`db.open`, `db.stats`, `db.backup`, `db.rebuild`, `db.pragmas.*`, `db.health`)
- Collection tools (`col.list/create/drop/rename/stats`)
- Document tools (`doc.insert/insertMany/upsert/update/delete/find/findById/count/aggregate`)
- Index tools (`idx.list/ensure/drop`)
- SQL & diagnostics (`sql.execute`, `sql.explain`, `expr.validate`)
- Transactions (`txn.begin/commit/rollback`)
- FileStorage (`fs.list/upload/download/delete/find`)
- Import/export (`export.json`, `import.json`, `dump.database`, `restore.database`)
- Schema intelligence (`schema.infer`)
- Read-only MCP resources (`litedb://{alias}/info`, `/collections`, `/schema/{collection}`, `/sample/{collection}`, `litedbfs://{alias}/files`)
- Built-in prompts (`how_to_query`, `how_to_index`, `how_to_filestorage`, `safety_notes`)

> This repo is backed by the **“LiteDB Advance MCP Server Specification”** document which defines the full requirements, tool catalog, resources, prompts, and non-functional constraints.

## Tech stack

- C# 13 on .NET 9 (LTS where available)
- LiteDB v5 (v5 file format, encrypted and unencrypted)
- MCP over stdio (JSON-RPC, e.g. StreamJsonRpc), optional HTTP transport
- `Microsoft.Extensions.Logging` + optional Serilog/OpenTelemetry
- xUnit v3 + FluentAssertions + coverlet
- GitHub Actions for CI/CD, MIT license

## Project layout (planned)

```text
/src/LiteDB-Adv-MCP.Server      # MCP host, transports, entry points
/src/LiteDB-Adv-MCP.Core        # core domain, options, validators, errors
/src/LiteDB-Adv-MCP.LiteDb      # LiteDB adapters, connection mgmt, diagnostics
/src/LiteDB-Adv-MCP.Tools       # MCP tool implementations
/src/LiteDB-Adv-MCP.Resources   # MCP resources/resolvers
/src/LiteDB-Adv-MCP.Prompts     # built-in MCP prompts/templates
/tests/LiteDB-Adv-MCP.Tests     # xUnit v3 tests (unit + integration)
/examples                       # Cursor/Cline/Claude Code/Inspector configs
/.github/workflows              # CI/CD pipelines
