<!--
  Thanks for contributing to Chronicle.
  Keep this short - a few honest sentences beat a filled-in form.
-->

## What and why

<!--
  What does this change, and why is it worth doing? The diff shows the what;
  this is where you explain the why. One paragraph is usually plenty.
-->

Closes #

## Type of change

- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation
- [ ] Internal / refactor / tooling

## The invariant

Chronicle's core guarantee is that a written ledger entry cannot be altered or removed without verification failing.

- [ ] This change does not mutate, delete, or reorder any existing ledger entry.

<!--
  If you cannot tick that box, stop and open an issue instead - there is almost
  always an append-only shape for what you are trying to do, and we would rather
  find it with you than reject the PR.

  Not applicable to changes that do not touch the ledger (docs, tooling, CI).
  Tick it anyway; it is trivially true.
-->

## Checks

- [ ] `composer test:unit` passes
- [ ] `composer test:types` passes (PHPStan level 10, no new baseline entries)
- [ ] `composer lint` has been run
- [ ] Tests cover the change. For bug fixes, a test that fails before it and passes after.
- [ ] Docs updated, if behavior changed

## Anything else

<!--
  Trade-offs you made, alternatives you rejected, parts you would like a closer
  look at, or questions you still have. Saying "I am not sure about the approach
  in X" is welcome and makes review faster, not slower.
-->
