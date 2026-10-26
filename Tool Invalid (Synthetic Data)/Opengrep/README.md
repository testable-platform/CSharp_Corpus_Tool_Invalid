# Opengrep

Inverse-corpus counterpart to the sibling CSharp-Tools-Clean's **Opengrep**
folder. Opengrep is a semgrep fork sharing its rule format; not reachable
here (see Notes), so `semgrep` -- already installed, and used the same way
as this corpus's own Semgrep folder -- was run for real against a local,
differently-ordered copy of the same ruleset.

Package: opengrep/opengrep (Go binary / GitHub release) -- semgrep
standing in for real invocation

Domain: armory checkpoint clearance control (CheckpointClearanceControl)

**Measured**: installed (as its semgrep stand-in) and actually invoked
against this folder's own source; the result below is real, not asserted.

## What "wrong" means here

`CheckpointClearanceControl` plants one instance of every rule in
`security-rules.yml`:

- a hardcoded `string clearanceSecret = "...";` field (**hardcoded-secret**)
- `SHA1.Create()` used to compute the badge digest (**weak-hash-algorithm**)
- `new Random()` to mint clearance codes (**insecure-random**)
- `secret.Equals(token)` comparing two locals named exactly `secret` and
  `token` (**non-constant-time-compare**)

**4 of 4 rules fire = 100%.**

## Command

```bash
semgrep --config security-rules.yml src/
```

Real measured output:

```text
4 Code Findings
Ran 4 rules on 1 file: 4 findings.
```

## Notes

Opengrep's real distribution is a GitHub Release binary, and GitHub
Releases return 403 at this sandbox's egress proxy (measured directly),
with no apt or go-install route either -- identical gap to the sibling
CSharp-Tools-Clean corpus and to the sibling TypeScript/JavaScript
corpora's own Opengrep folders.

## Per-family results

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netfx46` | .NET Framework 4.6 (Mono 6.8.0.105 BCL profile 4.6) | yes | **FINDING** (4/4 rules fire) |

Identical source, identical measured result, across all five boundary
families -- the grammar used is version-blind, so the finding does not
and should not move with the language version.

This repo carries only the `netfx46` family.
