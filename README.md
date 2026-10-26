# C# Corpus -- Tool Invalid (Synthetic Data)

`main` carries only this overview -- it holds no project code. Every other
branch in this repository is one cell of `testable-platform/csharp-corpus`, split out to carry
only the `Tool Invalid (Synthetic Data)/` folder (plus that branch's own build scaffolding).

This repository was produced by splitting `testable-platform/csharp-corpus` by task folder.
`testable-platform/csharp-corpus` itself was not modified by this split and still holds the
full combined corpus.

## Scope

This repo covers the 5 boundary .NET families (netfx45, netfx46, netcoreapp30, net9, net10) across the full build-tool x dependency-manager x architecture combination (120 branches total). Each branch carries only its own family's data inside `Tool Invalid (Synthetic Data)/` -- not all 5 boundary families bundled together.

## Branch naming

Branch names are unchanged from `testable-platform/csharp-corpus`:

```
CS_V{family}_{BUILD_TOOL}_{DEPENDENCY_MANAGER}_{ARCHITECTURE}
```

## Finding a branch

Each branch's own `README.md` describes its exact cell (.NET family, build
tool, dependency manager, architecture) and its tool roster, trimmed to the
parts relevant to `Tool Invalid (Synthetic Data)/`. `dataset.json` on each branch is the
machine-readable answer key for that cell (unmodified by this split -- it
still describes the branch's original full 19-tool/5-folder state).

## History

Each branch's commit history is carried over unchanged from `testable-platform/csharp-corpus`,
with one additional commit on top that removes the folders not relevant to
this repo. Nothing was squashed or rewritten.
