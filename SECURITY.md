# Security Policy

Chronicle is used to produce audit trails that people rely on as evidence. We take reports seriously and we'd rather hear about a borderline issue than not hear about it at all.

## Reporting a vulnerability

**Please do not open a public issue, discussion, or pull request for a security vulnerability.**

Report it privately through either channel:

- **[GitHub Security Advisories](https://github.com/laravel-chronicle/core/security/advisories/new)** (preferred - keeps the report, the fix, and the eventual disclosure in one place)
- **Email:** [security@laravel-chronicle.dev](mailto:security@laravel-chronicle.dev)

Please include:

- A description of the vulnerability and which package(s) it affects
- Steps to reproduce, ideally a minimal failing test or reproduction repository
- The version(s) you tested against
- Your assessment of the potential impact

## What happens next

| Stage | Target |
| --- | --- |
| Acknowledgement of your report | Within 72 hours |
| Initial assessment and severity triage | Within 5 business days |
| Fix released, or a status update with a timeline | Within 30 days |
| Public advisory published | After the fix ships |

If we can't hit one of these, we'll tell you rather than go quiet.

We'll credit you in the advisory unless you'd rather stay anonymous, and we'll request a CVE for anything of moderate severity or above.

## Supported versions

Security fixes land on the latest minor release of each package. Older minors receive fixes only when an upgrade path isn't practical.

| Package | Supported |
| --- | --- |
| `chronicle` | Latest 1.x |
| `filament` | Latest 1.x |
| `anchor-s3` | Latest 1.x |
| `kms-aws` | Latest 1.x |

Pre-1.0 releases are not supported. If you're running one, please upgrade before reporting.

## What counts as a vulnerability

Anything that undermines the guarantees Chronicle makes is in scope, including:

- **Integrity failures** - any way to mutate, delete, reorder, or backdate a ledger entry without verification failing. This is the core promise; treat any crack in it as high severity.
- **False verification** - verification reporting a chain as intact when it isn't, or a checkpoint validating against material it shouldn't.
- **Key material exposure** - DEKs, KEKs, or signing keys leaking into logs, exceptions, serialized output, or query bindings.
- **Erasure failures** - a GDPR erasure that leaves subject data recoverable, or that damages the chain rather than writing a proof entry.
- **Write-policy bypass** - writing entries that the configured policy pipeline should have rejected.
- **Panel escalation** - any path through the Filament panel that mutates the ledger. The panel is read-only by design; a write is a bug.
- Standard web vulnerabilities in package code: injection, deserialization, XSS in shipped views, and so on.

## Out of scope

- Vulnerabilities in Laravel, Filament, or other upstream dependencies - please report those to their maintainers
- Misconfiguration of your own application, database, or cloud storage (e.g. an S3 bucket without Object Lock enabled)
- Attacks that assume the attacker already has arbitrary code execution on your application server
- Missing hardening headers or best practices with no demonstrated impact
- Automated scanner output submitted without a working proof of concept

## Safe harbor

We will not pursue legal action against anyone who reports a vulnerability in good faith, makes a reasonable effort to avoid harm to users or data, and gives us reasonable time to fix the issue before disclosing it publicly.

---

Thank you for helping keep Chronicle trustworthy.
