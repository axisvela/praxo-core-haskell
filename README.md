# PRAXO-CORE for Haskell

PRAXO-CORE is an embeddable, MIT-licensed agent framework. This package is its native Haskell Core. It implements all eleven declared vector groups and does not call Go or another Core. It includes a native callback-based agent loop with tools, policy hooks, typed events, memory, checkpoints, context budgets, middleware, JSON Schema validation, plugin manifest parsing, and runtime helpers.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core` |
| Registry | [Hackage](https://hackage.haskell.org/package/praxo-core-0.5.0) |
| Install | `cabal install praxo-core` |
| Source version | `0.5.0` |
| Published version | `0.5.0` |
| Source tag | `haskell/v0.5.0` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/haskell/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native (transport seam)
- Anthropic model: native (transport seam)
- Gemini model: native (transport seam)
- MCP client: native (transport seam)
- Harmovela sink: native (transport seam)
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native (synchronous seam)
- Retriever: native

## Quick start

Install the published package:

```bash
cabal install praxo-core
```

```haskell
import Praxo.Json
import Praxo.JsonSchema
import Praxo.ToolCall

main :: IO ()
main = do
    print (parseToolCall "{\"name\":\"echo\",\"input\":{\"text\":\"hello\"}}")
    print (validateSchema (JObject [("type", JString "string")]) (JNumber 42))
    print (encodeJson (JObject [("runId", JString "run-1")]))
```

See the [full Haskell README](language/haskell/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native (transport seam) | Caller supplies `Transport`; no bundled HTTP client |
| Anthropic model | native (transport seam) | `Praxo.Anthropic`; caller supplies transport |
| Gemini model | native (transport seam) | `Praxo.Gemini`; caller supplies transport |
| MCP client | native (transport seam) | `Praxo.Mcp`; caller supplies `McpTransport` |
| Harmovela sink | native (transport seam) | `Praxo.Harmovela`; caller supplies transport |
| OpenTelemetry sink | native (transport seam) | `Praxo.Otel`; caller supplies `OtelTransport` |
| Subagent delegation | native (synchronous seam) | `Praxo.Delegation.subagentRun`; no asynchronous manager |
| Retriever | native | `Praxo.Retriever.Document` and `Retriever` |

## Examples

Runnable examples live under [`language/haskell/examples`](language/haskell/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/haskell/examples/checkpoint) | This example uses the Haskell Core checkpoint allowlist for a registered payload round trip. |
| [event-sink](language/haskell/examples/event-sink) | This example uses Haskell Core sink composition to fan out events and filter the tool-only stream. |
| [identity-policy](language/haskell/examples/identity-policy) | This example binds a trusted principal to policy decisions and rejects missing, role-mismatched, and tenant-mismatched actions. |
| [mcp](language/haskell/examples/mcp) | This example uses a caller-owned in-process transport with the Haskell MCP client. |
| [provider-fallback](language/haskell/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary failure when both fail. |
| [retry](language/haskell/examples/retry) | This example retries a transient failure with a bounded attempt count and keeps the exhausted failure state. |
| [service](language/haskell/examples/service) | This example defines a transport-neutral request handler with health, principal, and run cases. |
| [streaming](language/haskell/examples/streaming) | This example accumulates streamed chunks and checks that they reconstruct the final output. |
| [structured-output](language/haskell/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Verify

Run the checks from `language/haskell`:

```bash
python language/haskell/run-tests.py
python language/haskell/api-snapshot.py --check
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/haskell/README.md`](language/haskell/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

## Repository layout

- `language/haskell/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/haskell
- Registry introduction: `language/haskell/REGISTRY.md`
- Machine-readable entry: `language/haskell/llms.txt` and `language/haskell/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-haskell
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical Haskell source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
