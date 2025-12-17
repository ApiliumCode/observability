<p align="center">
  <img src="https://raw.githubusercontent.com/ApiliumCode/aingle/main/assets/aingle.svg" alt="AIngle Logo" width="200"/>
</p>

<h1 align="center">observability</h1>

<p align="center">
  <strong>Structured contextual logging and tracing for AIngle</strong>
</p>

<p align="center">
  <a href="https://crates.io/crates/observability"><img src="https://img.shields.io/crates/v/observability.svg" alt="Crates.io"/></a>
  <a href="https://docs.rs/observability"><img src="https://docs.rs/observability/badge.svg" alt="Documentation"/></a>
  <a href="https://github.com/ApiliumCode/observability/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"/></a>
  <a href="https://github.com/ApiliumCode/observability/actions"><img src="https://github.com/ApiliumCode/observability/workflows/CI/badge.svg" alt="CI Status"/></a>
</p>

---

## Overview

Structured contextual logging built on [tracing](https://docs.rs/tracing). This crate provides experimental observability features for AIngle distributed systems, including console output, JSON logging, and span filtering.

## Features

- **Structured logging** - Context-aware log events with spans
- **Multiple outputs** - Console, JSON, and custom formatters
- **Powerful filtering** - Filter by module, span, or field values
- **Zero-cost abstractions** - Disabled spans compile to no-ops

## Installation

```toml
[dependencies]
observability = "0.1"
```

## Quick Start

### Console Logging

```bash
# Simple logging
RUST_LOG=trace cargo run

# Filtered logging
RUST_LOG='core[a{something="foo"}]=debug' cargo run
```

### JSON Output

```bash
RUST_LOG='core[{}]=debug' cargo run --structured Json > log.json
```

### Filter Syntax

```bash
# Module + span + field filtering
RUST_LOG='core[a{something="foo"}]=debug'

# Multiple filters
RUST_LOG='[{}]=error,[{something}]=debug'
```

| Component | Description |
|-----------|-------------|
| `core` | Module path filter |
| `[a]` | Span name filter |
| `{field="value"}` | Field value filter |
| `=debug` | Minimum log level |

## JSON Output

```json
{
  "time": "2024-01-01T00:00:00.000Z",
  "name": "event",
  "level": "INFO",
  "target": "my_module",
  "file": "src/lib.rs",
  "line": 42,
  "fields": {"message": "Hello"},
  "spans": [{"name": "request", "id": 1}]
}
```

## Useful Tools

| Tool | Purpose |
|------|---------|
| [jq](https://stedolan.github.io/jq/) | JSON processing |
| [json2csv](https://www.npmjs.com/package/json2csv) | Convert to CSV |
| [tad](https://www.tadviewer.com/) | CSV viewer |

## Resources

- [Why Tracing? (Video)](https://www.youtube.com/watch?v=JjItsfqFIdo)
- [Tokio Tracing Blog](https://tokio.rs/blog/2019-08-tracing/)
- [EnvFilter Documentation](https://docs.rs/tracing-subscriber/latest/tracing_subscriber/filter/struct.EnvFilter.html)

## Part of AIngle

This crate is part of the [AIngle](https://github.com/ApiliumCode/aingle) ecosystem - a Semantic DAG framework for IoT and distributed AI applications.

## License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Maintained by <a href="https://apilium.com">Apilium Technologies</a> - Tallinn, Estonia</sub>
</p>
