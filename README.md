# STF — Semantic Text Format

**A semantic, human-readable text format for intelligent agents.**

[![Specification](https://img.shields.io/badge/Spec-v0.1.0-blue)](STF_Specification.stf)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-green)](LICENSE)
[![Code License](https://img.shields.io/badge/Code-Apache--2.0-green)](LICENSE-CODE)

## What is STF?

STF (Semantic Text Format) is a text format for semantic representation. It was created alongside the Semantic Interface Layer (SIL) specification as the concrete syntax SIL needed to describe interactive applications to intelligent agents — and then separated into its own project because the format proved more fundamental than its first application.

SIL (Semantic Interface Layer) is the first application vocabulary built on STF. It defines how web applications expose their state, capabilities, actions, and events to agents. See the [SIL specification](https://github.com/ais-space/sil) for the web-facing protocol.

STF is:

- **Text-based and hierarchical** — indentation shows structure, PascalCase names show objects, colon-separated properties carry values. No brackets, no quotation marks for keys, no escape sequences.
- **Directly interpretable by language models** — designed to be read by an agent the way a human reads an outline, without task-specific training, fine-tuning, or system prompts.
- **Machine-parseable by a formal grammar** — a deterministic EBNF grammar (`grammar/stf.ebnf`) lets a parser reject any malformed input without guessing intent.
- **Safe by construction** — the trust boundary is enforced by the grammar and type system, not by filtering dangerous-looking strings.

The specification itself is written in STF. The standard and the example are one: STF is self-hosting.

## STF and SIL

STF is the **format**. SIL (Semantic Interface Layer) is the first, furthest-developed **application vocabulary** built on top of STF — it binds STF to HTTP, defines UI Types/Roles, an Intent protocol, sessions, events, and discovery.

```text
STF (core)
 ├── syntax (how to write and read)
 ├── object model (what it means)
 ├── trust model (structural security)
 └── extension mechanism
        │
        └── SIL (application vocabulary)
             ├── UI Types / Roles / States
             ├── Intent protocol over HTTP
             ├── sessions, events, discovery
             └── conformance profiles
```

STF deliberately defines **no transport and no application vocabulary**. Those are supplied by extensions. SIL is one such extension; others are expected.

## Three-layer architecture

STF is organized in three layers, only the first two of which belong to the core:

- **Layer 1 — STF Syntax.** How to write and read. Text format, grammar, parsing rules. A parser validates syntax without knowing what "Button" means.
- **Layer 2 — Semantic Vocabulary (core).** What it means. Types, Roles, States, Actions, Origin. The core standardizes these *fields* and their trust semantics; the concrete *values* (e.g. Card, SubmitAction, Open) are supplied by application vocabularies (§3.3), not by the core. The object model and trust model are standardized; applications extend them.
- **Layer 3 — Application Protocol (extension).** How to interact. Transport, sessions, action submission, event delivery. Defined by an application vocabulary (for example SIL over HTTP); not part of the STF core.

Separation of concerns: a parser validates STF without knowing semantics. A consumer interprets capabilities without knowing implementation details. A different transport can use the same syntax and vocabulary — only the protocol layer changes.

## How it works

A producer turns an application model or knowledge source into an STF document; a consumer reads structure and meaning directly.

```text
   Producer                  Consumer
      │                          │
      │  STF document            │
      │  (core: syntax +         │
      │   object model +         │
      │   trust model)           │
      │─────────────────────────>│
      │                          │
      │   understood directly    │
```

No presentation is reconstructed. No strings are filtered for safety — untrusted content is *data by construction*.

A minimal example:

```text
Context
    DocumentVersion: 0.1.0
    GrammarVersion: 1.0.1
    Language: en

Page
    Type: Page
    Role: Content
    Section
        Type: Section
        Role: Content
        Text
            Type: Text
            Content: Hello, semantic world.
```

## Key properties

### Semantic, not presentational

Objects describe their type, role, state, and available actions instead of requiring the consumer to infer them from layout.

### LLM-oriented text

STF is designed for direct interpretation by language models. It does not require a vision model merely to understand basic structure.

### Deterministic interpretation

Where structure can carry meaning, STF eliminates ambiguity. The grammar, object model, and trust model are unambiguous and machine-parseable. Natural-language fields (Purpose, Description) are scoped clearly so consumers know what is structural and what is advisory.

### Structural trust boundary

STF distinguishes application-defined knowledge from user-provided data at the structural level. `UserContent` cannot contain executable properties by grammar construction; Origin defaults to fail-closed `Unknown`; Knowledge Zones separate trusted system content from untrusted visitor content.

### Extensible without redefinition

A vendor extension may add new Types, Roles, States, Actions, and properties via reverse-domain keys, but MUST NOT redefine core semantics.

## STF compared with other formats

| Technology          | Primary purpose                                  | Relationship to STF                                              |
| ------------------- | ------------------------------------------------ | ---------------------------------------------------------------- |
| **JSON / YAML**     | General machine data serialization               | STF is optimized for semantic readability by agents, not arbitrary data |
| **HTML**            | Human-facing web interface                       | STF is a semantic layer an agent can read directly               |
| **XML**             | Document and data markup                         | STF favors outline-style indentation over angle brackets         |
| **OpenAPI / JSON Schema** | Describe APIs and data structures         | STF describes semantic structure and meaning for a consumer      |

STF is not intended to replace JSON, YAML, XML, or HTML. It occupies a different layer: explicit semantic communication for intelligent agents and systems.

## Specification

The canonical specification is:

**STF v0.1.0**

- [STF_Specification.stf](STF_Specification.stf) — canonical specification in STF (self-hosting)
- [STF_Concept.stf](STF_Concept.stf) — conceptual background (also written in STF)
- [grammar/stf.ebnf](grammar/stf.ebnf) — formal STF grammar (GrammarVersion 1.0.1)

## Repository structure

```text
stf/
├── STF_Specification.stf
├── STF_Concept.stf
├── README.md
├── CHANGELOG.md
├── ROADMAP.md
├── LICENSE
├── LICENSE-CODE
├── CONTRIBUTING.md
├── SECURITY.md
├── CODE_OF_CONDUCT.md
├── grammar/
│   └── stf.ebnf
└── examples/
    └── minimal.stf
```

## Conformance

A conformant STF core implementation MUST:

- parse and generate valid STF documents per the grammar, distinguishing SyntaxError from SemanticError;
- validate the Object Model: required objects, Id uniqueness, field classification;
- enforce the structural trust boundary: Origin propagation, privilege lattice, knowledge zones, and rejection or ignoring of Control properties on Untrusted objects;
- honor the Extensibility Principle: extensions do not redefine core semantics.

The STF core defines no transport, session model, or action vocabulary — those are provided by application vocabularies such as SIL.

## What STF is not

STF is not:

- a programming language or scripting environment;
- a replacement for JSON, YAML, or XML as a data serialization format;
- a visual interface, automation protocol, testing framework, or page description language;
- a claim that language models possess a special "native" language;
- a security mechanism that makes unsafe applications safe automatically.

## License

- **Specification:** [Creative Commons Attribution 4.0 International](LICENSE) (CC-BY-4.0)
- **Reference code, tests, and tooling:** [Apache License 2.0](LICENSE-CODE)

Implementations do not inherit these licenses and may be released under other licenses.

## Contact

- **Specification issues:** [GitHub Issues](https://github.com/ais-space/stf/issues)
- **Website:** [ais-platform.dev](https://ais-platform.dev)
