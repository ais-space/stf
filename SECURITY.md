# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in the STF specification, reference grammar, or related code in this repository, please report it privately.

**Contact:** security@ais-platform.dev

**Response time:** We aim to acknowledge reports within 48 hours and provide an initial assessment within 5 business days.

## Scope

This security policy covers:

- The STF specification text (ambiguities that could lead to insecure implementations)
- The formal grammar (`grammar/stf.ebnf`)
- Reference implementations and tooling in this repository

## Out of Scope

- Vulnerabilities in third-party STF implementations (report to those projects directly)
- Semantic prompt injection through `UserContent` (documented limitation of the format, not a vulnerability) — see §4.3 of the specification
- Denial-of-service through resource exhaustion beyond documented parser limits (§2.0)

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 0.1.0   | :white_check_mark: |

## Disclosure Policy

We follow responsible disclosure:
1. Reporter submits vulnerability privately
2. We acknowledge within 48 hours
3. We assess and develop a fix
4. We notify the reporter when the fix is ready
5. We publish the fix and credit the reporter (unless anonymity is requested)

## Security Model

STF's security model is documented in §4 of the specification. Key properties:

- **Structural trust boundary**: `UserContent` cannot contain executable properties by grammar construction
- **Fail-closed Origin**: default Origin is `Unknown` (untrusted)
- **Knowledge Zones**: ApplicationKnowledge vs UserData separation
- **Producer-controlled Origin**: consumers cannot elevate trust through submitted content

For a full understanding of STF's security properties and limitations, see §4 of the specification.
