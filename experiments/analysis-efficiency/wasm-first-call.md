# WASM first-call summary delivery

Refs [#2016](https://github.com/morluto/rea/issues/2016). This bounded follow-up
adds optional MCP `inspect_wasm_artifact detail: summary`. Omitted/complete MCP
requests and CLI output remain complete. Full original Evidence is retained;
delivery selection is stripped before provider inputs, and exact export views
read the original parent without another WABT invocation.

## Pinned repeated public SDK cohort

- Control: `18e5d6275965c5f1d3ef9fe373d1792822098003`.
- Candidate: `45831c622a13368494d2a8f3a9718effa91c937c`.
- Runtime file-table SHA-256: control `ef65527c2d41b621f71059b7553050660d801ad905a61a71b81aba266f70e1ec`;
  candidate `353f5513ea09b0a627fa99814cebe0a1231c6c8f7e0e12a28205521133478b1a`.
- Actual WABT 1.0.42, identical explicitly selected provider configuration and
  effective search-path fingerprint, pinned Node 24.18.0 and locked SDK.
- Three paired fresh-process trials per digest-pinned shipped module, serial
  on one CPU: control/candidate, candidate/control, control/candidate.
- Same validation/counts/first-four complete export forms/WAT identity/provider
  identity/execution and fetch states; complete original source Evidence ID is
  also compared. All nine pairs preserve these selected facts and source IDs.

| Shipped module                | Result JSON bytes, control → summary | Calls / errors | Median seconds, control → summary (ranges)      |
| ----------------------------- | -----------------------------------: | -------------- | ----------------------------------------------- |
| `sqlite.wasm`                 |                      20,118 → 18,533 | 3/1 → 2/0      | 15.962 (15.719–21.138) → 18.171 (10.242–18.649) |
| `vscode.tree-sitter-css.wasm` |                      20,366 → 18,781 | 3/1 → 2/0      | 4.920 (4.885–4.936) → 5.191 (4.971–5.232)       |
| `vscode.tree-sitter.wasm`     |                   6,433,872 → 18,891 | 1/0 → 2/0      | 5.225 (5.172–5.519) → 4.763 (4.729–4.830)       |

Byte counts include all investigation call results, including failed delivery
and extra views. They exclude catalog responses, raw wire framing and file
exports; they are not actual model tokens. The complete catalog is 2,359,082
versus 2,362,451 JSON bytes (+3,369 bytes, about 0.14%). An extra export-view
call is included when summary replaces an otherwise fitting complete reply.

| Shipped module                | Median owned CPU seconds, control → summary | Median sampled family MiB, control → summary (maxima) |
| ----------------------------- | ------------------------------------------- | ----------------------------------------------------- |
| `sqlite.wasm`                 | 15.376 → 15.954                             | 660.84 (671.27) → 633.07 (671.51)                     |
| `vscode.tree-sitter-css.wasm` | 5.760 → 6.027                               | 692.91 (694.93) → 678.98 (693.88)                     |
| `vscode.tree-sitter.wasm`     | 6.134 → 5.663                               | 674.04 (695.66) → 550.66 (553.47)                     |

All 18 scopes have no sampled abort, memory-high/hard/OOM/OOM-kill or task-limit
event. Sampling can miss brief peaks. Application caches are cold per process;
host page caches are not flushed. SDK elapsed time includes startup, discovery,
schema work and persistence, not just provider analysis. Three observations
give descriptive medians/ranges, not a statistical or cross-domain speed claim.

SQLite and the CSS grammar already recovered an oversized complete result
through retained views in the control. The new path removes the initial error
and one call; result-byte savings are correspondingly modest. The Tree-sitter
runtime fits the MCP frame but delivers megabytes of unneeded WAT; its summary
plus exact exports greatly reduces delivery. Full provider analysis and complete
Evidence retention still occur, so this does not establish an engine shortcut.

An earlier 18-run cohort did not activate the treatment: the driver looked
for an inline enum and missed SDK-generated `$ref` definitions. Those original
runs and their source are archived separately and excluded from benefit claims.
The corrected driver validates the actual advertised 2020-12 request schema.

## Real model verification

Repeated actual Codex CLI trials are in progress. No token or model-answer
benefit is credited until usage, transcripts and requested facts are reviewed.

## Reproduction and verification

Use [the common measurement/model instructions](README.md) with the public
digest-pinned inputs in [corpus.json](corpus.json), `--schemas selected` and
`--delivery summary`. For each artifact run the above three paired orders
against separately frozen runtimes, then `compare.mjs`. Use the same
[WASM interface question](questions/wasm-interface.txt), four exact enabled
tools (`inspect_wasm_artifact`, `inspect_analysis_view`, `get_evidence_bundle`,
`export_evidence_bundle`), explicit WABT settings and resource scope for models.

The VS Code artifacts are two published components from
[@vscode/tree-sitter-wasm 0.3.1](https://github.com/microsoft/vscode-tree-sitter-wasm).
The selected regular archive members have verified digests and package SHA-512
integrity. This is component analysis, not proof of the whole VS Code runtime.

The prototype passes 54 focused assertions and full static/docs gates. After
rebasing, 29 focused assertions and 42 actual installed-package WABT CLI/MCP
cases pass; the final rebased snapshot passes build/fast static and seven WASM
MCP workflows again. Omitted/explicit-complete behavior, retained identity,
fixed-server absence of retention, oversized continuation and invalid WAT
digest remain checked. No version publication or target execution occurs.
The final static/build scope has 51 soft memory-high events and no hard/OOM
events; this is not credited as a performance trial.

Detailed JSON, transcripts, target bytes, profiles and acquisition receipts
stay outside Git. Source inputs, scripts and this concise measured scope are
reviewable in the repository.
