# altcover

Inverse-corpus counterpart to the sibling CSharp-Tools-Clean's **altcover**
folder. Stays **NOT_INSTALLED** here too -- the blocker is infrastructure
(NuGet), not anything about this corpus being Clean or Invalid, so there is
nothing to invert.

Package: AltCover (NuGet global tool / MSBuild package)

Domain: cold storage pallet intake ledger (ColdStorageIntake)

**Not installed here**: see Notes for why, and what was checked instead.

## What a result would look like

AltCover's IL-weaving instrumentation of ColdStorageIntake would report
real statement/branch coverage from a real xUnit run -- genuinely low, if
the corpus could reach it, since the fixture's own test suite only
exercises part of its branches. Not measurable here: see Notes.

## Command

```bash
dotnet test /p:AltCover=true
```

## Notes

AltCover ships only as a NuGet package (`altcover` global tool or
`altcover.api`); this sandbox's egress proxy refuses `api.nuget.org`
(`connect_rejected`/403, measured directly with `dotnet restore`), so
nothing with a `PackageReference` resolves -- identical to the sibling
Clean corpus's own finding. The source still compiles clean with `dotnet
build` against zero external packages, at every one of the five boundary
families (see the root README's compile-check gate).

## Per-family results

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `net9` | net9.0 (manual csc, SDK 10.0.112's compiler + installed 10.0.12 runtime) | yes | NOT_INSTALLED |

This repo carries only the `net9` family.
