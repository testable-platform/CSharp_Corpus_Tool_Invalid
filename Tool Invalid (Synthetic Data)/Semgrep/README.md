# Semgrep

Inverse-corpus counterpart to the sibling CSharp-Tools-Clean's **Semgrep**
folder: a synthetic C# project engineered so every one of the shared
ruleset's rules fires for real.

Package: semgrep 1.178.0 (PyPI, standalone)

Domain: armored cargo seal verification (CargoSealVerifier)

**Measured**: installed and actually invoked against this folder's own
source; the result below is real, not asserted.

## What "wrong" means here

`CargoSealVerifier` plants one instance of every rule in `rules.yml`:

- a hardcoded `string sealingKey = "...";` field (**hardcoded-secret**)
- `MD5.Create()` used to compute the seal digest (**weak-hash-algorithm**)
- `new Random()` to mint manifest IDs (**insecure-random**)
- `hash == token` comparing two locals named exactly `hash` and `token`
  (**non-constant-time-compare**)

**4 of 4 rules fire = 100%.**

## Command

```bash
semgrep --config rules.yml src/
```

Real measured output:

```text
4 Code Findings
  hardcoded-secret            domain.cs:9   private string sealingKey = "quarry-seal-9f3a2c1d";
  insecure-random              domain.cs:12  private readonly Random rng = new Random();
  weak-hash-algorithm          domain.cs:17  using (var md5 = MD5.Create())
  non-constant-time-compare    domain.cs:32  bool matches = hash == token;
Ran 4 rules on 1 file: 4 findings.
```

## Notes

Semgrep's tree-sitter grammar covers C# directly; the ruleset is the exact
same `rules.yml` used (and, in the sibling Clean corpus, never triggered)
in every other C#-Tools corpus. Every planted construct was verified to be
the real trigger for its rule, not a coincidental match -- each one is
checked individually in the generator's own build log.

## Per-family results

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `net9` | net9.0 (manual csc, SDK 10.0.112's compiler + installed 10.0.12 runtime) | yes | **FINDING** (4/4 rules fire) |

Identical source, identical measured result, across all five boundary
families -- Semgrep's grammar is version-blind, so the finding does not
and should not move with the language version.

This repo carries only the `net9` family.
