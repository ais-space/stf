# Changelog

All notable changes to the STF (Semantic Text Format) core specification.

---

## v0.1.0 (2026-08-16) — First Core Release (extracted from SIL)

### Core
- First standalone release of the STF core, extracted from the SIL specification
- Grammar: `GrammarVersion 1.0.1` (inherited stable grammar; no syntax changes from SIL's STF)
- Self-hosting STF specification document (`STF_Specification.stf`)
- Concept document in STF (`STF_Concept.stf`)

### What the core defines
- **Layer 1 — STF Syntax (§2):** lexical and syntactic grammar, indentation-sensitive parsing algorithm, canonical serialization, no escape sequences, strict error recovery
- **Layer 2 — Object Model (§3):** three-layer object identification (ObjectName / Type / Role / Id), standard property reference, field classification (Data / Guidance / Control), Id requirement, Expects parameter declaration
- **Trust Model (§4):** structural trust boundary, Origin values and propagation, privilege lattice, Knowledge Zones (ApplicationKnowledge / UserData / AgentInstruction), error taxonomy (SyntaxError / SemanticError / TrustBoundaryViolation)
- **Extensions (§5):** vendor properties (reverse-domain prefix), unknown-extension handling, protocol binding as extension
- **Document Structure and Conformance (§6):** required Context + Page, meta-block, self-hosting, core conformance requirements

### Scope boundary
- The STF core deliberately defines NO transport and NO application vocabulary
- SIL-specific material (UI Types/Roles, action names, HTTP Intent protocol, sessions, events, discovery, conformance profiles) is intentionally excluded and lives in the SIL project, which is an application vocabulary on top of STF

### Compatibility
- STF grammar is byte-for-byte compatible with the grammar used by SIL 1.0.1
- DocumentVersion 0.1.0 marks the first independent release of the format project
