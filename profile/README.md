<h1 align="center">Laravel Chronicle</h1>

<p align="center">
  <strong>Tamper-evident audit trails and compliance tooling for Laravel.</strong>
</p>

<p align="center">
  <a href="https://laravel-chronicle.dev">Documentation</a> ·
  <a href="https://demo.laravel-chronicle.dev">Live Demo</a> ·
  <a href="https://github.com/laravel-chronicle/core/discussions">Discussions</a> ·
  <a href="https://github.com/laravel-chronicle/core/issues">Issues</a>
</p>

---

## What we build

Most audit logs are just a table you write to. Anyone with database access can edit a row, drop a record, or backdate an entry - and nothing about the log itself would reveal it. Chronicle exists to close that gap.

Chronicle is an **append-only, hash-chained ledger** for Laravel. Every entry is cryptographically linked to the one before it, so tampering with history is detectable rather than silent. Around that core, we maintain packages for permissions, data-subject rights, and admin tooling - the pieces you actually need when an auditor asks how you know your records are intact.

Built for teams working under SOC 2, HIPAA, and GDPR.

## Packages

| Package                                                         | Description                                                                                                                           |
|-----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **[chronicle](https://github.com/laravel-chronicle/core)**      | The core ledger. Append-only writes, hash chaining, action registry, write policies, checkpoints, key rotation, and crypto-shredding. |
| **[filament](https://github.com/laravel-chronicle/filament)**   | A read-only Filament panel for browsing, verifying, and exporting the ledger - plus audited GDPR erasure.                             |
| **[anchor-s3](https://github.com/laravel-chronicle/anchor-s3)** | Anchors ledger checkpoints to S3 Object Lock, so proof of history lives outside your application entirely.                            |
| **[kms-aws](https://github.com/laravel-chronicle/kms-aws)**     | AWS KMS custody for key-encryption keys, for teams that don't want key material on the app server.                                    |

## See it in action

**[demo.laravel-chronicle.dev](https://demo.laravel-chronicle.dev)** - MedLedger, a sample patient-records application built on Chronicle. Browse the ledger, run a chain verification, and watch a GDPR erasure request produce an audited proof entry without rewriting a single existing record.

## Design principles

- **Append-only, always.** Nothing in the ecosystem mutates a written entry. Even GDPR erasure works by destroying key material and writing an audited proof entry, never by rewriting history.
- **Verifiable, not just stored.** Chain verification, external checkpoint anchoring (RFC 3161 timestamping, S3 Object Lock), and multi-key verification are first-class.
- **Boring to adopt.** Sensible defaults, no required infrastructure to get started, and an escape hatch at every layer.
- **Held to a high bar.** Pest test suites and PHPStan level 10 across every package.

## Getting started

```bash
composer require laravel-chronicle/core
php artisan chronicle:install
```

Full guides, recipes, and the compliance handbook live at **[laravel-chronicle.dev](https://laravel-chronicle.dev)**.

## Contributing

Issues, discussions, and pull requests are all welcome. If you're not sure where to start, look for `good first issue` on any repo, or open a thread in [Discussions](https://github.com/laravel-chronicle/core/discussions) - questions about compliance workflows are just as useful to us as code.

Every package follows the same contribution guide, code of conduct, and security policy, which live in this `.github` repository.

## Security

If you've found a vulnerability, please **do not** open a public issue. Report it privately through [GitHub Security Advisories](https://github.com/laravel-chronicle/core/security/advisories/new), and we'll respond as quickly as we can.

---

<p align="center">
  <sub>Maintained by <a href="https://github.com/ntoufoudis">Vasileios Ntoufoudis</a> and <a href="https://github.com/laravel-chronicle/core/graphs/contributors">contributors</a>. Released under the MIT License.</sub>
</p>
