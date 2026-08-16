# Contributing to STF

Thank you for your interest in contributing to the Semantic Text Format (STF) core specification and ecosystem.

## Ways to Contribute

### 1. Specification Feedback
- Open an issue for: bugs, ambiguities, missing edge cases, unclear wording
- Proposals for new features or changes: open an issue first to discuss before submitting a PR
- See `CHANGELOG.md` for the history of changes

### 2. Implementation Experience
- Build an STF parser or validator
- Report interoperability issues you encounter
- Share your implementation in the [Implementations](https://github.com/ais-space/stf) list

### 3. Grammars and Tooling
- Submit a tree-sitter or TextMate grammar for `.stf` syntax highlighting
- Help build the machine-readable conformance test suite
- Improve the formal `grammar/stf.ebnf`

### 4. Documentation
- Improve the README, examples, or guides
- Translate the specification (coordinate via issue first)
- Create tutorials or blog posts

## Pull Request Process

1. Fork the repository
2. Create a branch for your change
3. Ensure your change follows the repository structure
4. For specification changes: edit `STF_Specification.stf` (or the relevant volume) and keep it self-validating under its grammar
5. For grammar changes: edit `grammar/stf.ebnf` and keep `GrammarVersion` in sync with the specification meta-block
6. Submit a PR with a clear description of the change and its motivation

## Specification Development

The canonical specification is `STF_Specification.stf` — a self-hosting STF document, itself a valid STF document under its own grammar. Proposed changes are discussed through issues and pull requests; a change should keep the specification internally consistent and self-validating under its grammar.

The STF core is intentionally minimal: it defines the format, the object model, the trust model, and the extension mechanism. Transport bindings and application vocabularies (such as SIL) are out of scope for this repository and belong in their own projects.

## Governance

This project is maintained by AIS Platform. Specification changes are proposed through GitHub issues and pull requests, reviewed by maintainers, and merged when consensus is reached.

## License

- Specification text: [CC-BY-4.0](LICENSE)
- Reference code and tests: [Apache-2.0](LICENSE-CODE)
- Contributions are accepted under the same terms
