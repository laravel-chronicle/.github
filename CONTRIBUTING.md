# Contributing to Laravel Chronicle

Thanks for being here. Chronicle is a small project with a large surface area, and every issue, question, and pull request helps.

This guide applies to all repositories in the [`laravel-chronicle`](https://github.com/laravel-chronicle) organization. Some packages add their own setup steps - check for a `CONTRIBUTING.md` in the repository itself, which takes precedence over this one.

## Before you write code

**Open an issue first, for anything non-trivial.**

This isn't bureaucracy. Chronicle guarantees that a written ledger entry cannot be altered or removed without verification failing, and a surprising number of otherwise-good ideas quietly break that. It's much less painful to find out in a two-message issue thread than after you've spent a weekend on a pull request that can't be merged.

You can skip the issue for typo fixes, documentation corrections, and obvious one-line bugs. Use judgment; nobody will be annoyed with you for opening an issue that turns out to be simple.

If you're looking for somewhere to start, the [`good first issue`](https://github.com/search?q=org%3Alaravel-chronicle+label%3A%22good+first+issue%22+state%3Aopen&type=issues) label spans every repo.

## The invariant

Read this section even if you skip the rest.

**Nothing in this ecosystem mutates a written ledger entry.** Not a migration, not a cleanup command, not an admin panel, not a GDPR erasure. Entries are appended and hash-chained; changing one breaks verification, which is the entire point.

Where a feature seems to *require* mutation, the answer is always to append rather than alter. GDPR erasure is the worked example: it destroys the subject's key material - rendering the plaintext unrecoverable - and appends an audited proof entry recording that erasure happened. Existing records and hashes are untouched. The chain still verifies.

If your change involves an `update()`, a `delete()`, or a raw statement against a ledger table, it will not be merged in that form. Bring it to an issue, and we'll find the append-only shape together - there usually is one.

## Setup

```bash
git clone https://github.com/laravel-chronicle/<package>.git
cd <package>
composer install
```

That's the whole setup for most packages. Anything that needs external services (AWS, S3, a Filament panel) says so in its own `CONTRIBUTING.md`.

## Standards

Three things gate every pull request. All three run in CI, so you may as well run them locally first.

**Tests - [Pest](https://pestphp.com).**

```bash
composer test:unit
```

New behavior needs a test. Bug fixes need a test that fails before your change and passes after - that test is the most valuable part of the PR, because it's what stops the bug coming back.

For anything touching the chain, checkpoints, key handling, or erasure, we want to see the *negative* cases too: the tampered entry that must fail verification, the rotated key that must still verify history, the erased subject whose plaintext must be unrecoverable. Proving the guarantee holds is worth more than proving the happy path works.

**Static analysis - PHPStan, level 10.**

```bash
composer test:types
```

Level 10 is not negotiable and we don't merge new baseline entries. If PHPStan is fighting you, that's usually a signal the types are telling you something true. Ask in the issue rather than reaching for `@phpstan-ignore`.

**Code style.**

```bash
composer lint
```

Formatting is automated, so don't hand-tune it and don't mix style changes into a behavior PR - it makes review much harder.

## Pull requests

- **Branch from `main`**, one concern per branch.
- **Keep it focused.** A PR that fixes a bug *and* refactors a helper *and* tidies some formatting is three PRs wearing a trenchcoat, and it will sit unreviewed for longer than three separate PRs would.
- **Write a description that explains the why.** The diff already shows the what. If it closes an issue, say `Closes #123`.
- **Update the docs** when you change behavior. If your change affects usage, it affects [laravel-chronicle.dev](https://laravel-chronicle.dev) too - the docs source lives with the project and a PR that changes behavior without touching them is incomplete.
- **Note breaking changes explicitly** in the PR description. We follow semantic versioning, and a break that goes unnoticed until release is a bad day for everyone.

Review is usually a conversation, not a verdict. Expect questions; they're not an objection to your work.

## Reporting bugs

A good report includes the package and version, your PHP and Laravel versions, what you expected, what happened instead, and the smallest reproduction you can manage. A failing test is the gold standard, but a short reproduction repository or even a clear sequence of steps is genuinely fine.

**If the bug is a security issue - anything that lets an entry be altered, a verification pass when it shouldn't, or key material leak - do not open a public issue.** See [SECURITY.md](SECURITY.md) and report it privately.

## Asking questions

Questions belong in [Discussions](https://github.com/orgs/laravel-chronicle/discussions), not the issue tracker. "How would I audit a model that soft-deletes?" is a great discussion and a poor issue.

Compliance questions are welcome there too. If you're trying to satisfy an auditor and can't work out how Chronicle maps onto the control they're asking about, ask - those threads consistently turn into documentation improvements, which makes them among the most useful contributions the project gets.

## Conduct

Participation is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). The summary is: engage with the work, not the person.

---

Everything here is a default, not a wall. If a rule is stopping you from making a contribution that's obviously good, say so in the issue, and we'll sort it out.
