# Roadmap

## v0.1.0 (Released 2026-08-16) — First Core Release (extracted from SIL)

- [x] Layer 1 — STF Syntax (grammar, parser/validator separation, canonical serialization)
- [x] Layer 2 — Object Model (three-layer identification, field classification, Id, Expects)
- [x] Trust Model (structural trust boundary, Origin, Knowledge Zones, privilege lattice)
- [x] Extension mechanism (vendor keys, unknown-extension handling)
- [x] Document Structure and Conformance (required Context + Page, meta-block)
- [x] Self-hosting specification and concept document in STF
- [x] Formal grammar artifact (`grammar/stf.ebnf`, GrammarVersion 1.0.1)

## v0.2 (planned)

- [ ] Tree-sitter / TextMate grammar for `.stf` syntax highlighting
- [ ] Machine-readable conformance test suite (parse + validate vectors)
- [ ] Clarify whether a minimal neutral base set of action/state names belongs in the core
- [ ] IANA registration process for a `text/stf` media type
- [ ] Extended examples across application vocabularies (UI, config, agent memory)

## v1.0 (planned)

- [ ] Freeze the core format with a formal stability guarantee
- [ ] Streamable STF: chunked transfer encoding for very large documents
- [ ] Cross-document fragment identifiers (address an object across documents)
- [ ] Binary STF encoding for minimal token usage in agent contexts
- [ ] Formal verifier for STF core implementations

## Continuous

- [ ] Community feedback via GitHub Issues
- [ ] Independent parser implementations and interoperability testing
- [ ] Security reviews
