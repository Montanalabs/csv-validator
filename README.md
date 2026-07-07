[![Built with Eidos](https://img.shields.io/badge/built%20with-Eidos-0f9d8c?labelColor=1a1a2e)](https://github.com/Montanalabs/eidos-lang)

> **Eidos** — the injection-safe language. Here prompt injection isn't *detected*, it's
> *unrepresentable*: untrusted input must cross `extract<ClosedType>` before it can reach an
> effect. `check` proves it at compile time; the compiled binary re-clamps at run time.

# CSV ingestion validator

Untrusted input is a CSV row; it can only ever become one of a fixed set of decisions over a
closed type, never a tool argument. An injected instruction cannot be represented in the
closed type, so it is rejected — proven at compile time by `check`, and clamped again at
run time by the `extract` domain check.

- **Untrusted input:** `fetch<web>` — a CSV row
- **Closed type:** `type Decision = Ingest(Schema) | Reject`; a non-conforming row is rejected at extract
- **Sink / capability:** `grant load` → `privileged { load(d) }`
- **Consequence axes:** Trust

## Run the demo

```sh
examples/apps/csv-validator/demo.sh
```

The safe agent proves `SAFE`, runs on a benign input, and **rejects an injection
payload at the trust boundary (exit 3)**. The vulnerable version proves `UNSAFE` — it
never compiles to a runnable agent.

## Files

- `csv-validator_safe.eide` — the correct design.
- `csv-validator_unsafe.eide` — the tempting-but-wrong version (the negative example a model must learn to reject).
- `eidos.toml` — the project manifest (each app is a self-contained Eidos project).

---

<sub>Part of the <b><a href="https://github.com/Montanalabs/eidos-lang">Eidos</a></b> example corpus — 200 self-contained,
injection-safe projects. Built with Eidos, a language whose type system makes prompt injection
structurally impossible. Run <code>./demo.sh</code> with the Eidos toolchain on your PATH.</sub>
