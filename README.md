# OrderKit - CS_VNET9_CAKE_NUGETPACKAGESCONFIG_MONO

One branch of the C# tool-evaluation corpus. Test **data**, not a product: tool
execution is not part of the build, and evaluation happens later.

> **This cell cannot exist.** packages.config does not exist on .NET Core. On the .NET Framework families this was the ONE workable packages.config cell, because Cake could drive MSBuild.exe and nuget.exe over a legacy csproj. Neither exists here, so the cell that survived the whole Framework line dies at the crossing.
>
> The branch ships the artifacts the cell definition demands, plus this notice. It is *not* quietly backed by a working configuration -- a branch labelled one thing that ran another underneath is the exact silent success this corpus exists to catch.

## Branch

`CS_VNET9_CAKE_NUGETPACKAGESCONFIG_MONO`

## Cell

| Axis | Value |
|---|---|
| Bundler | Cake |
| Package manager | NuGet (packages.config) |
| Architecture | Monolith |

Projects:

- `OrderKit` (`src/OrderKit`)

## Target framework

`net9.0` - .NET 9

An STS release; support ended 12 May 2026, so the LTS BELOW it (net8) outlives it -- the second support inversion in the corpus, after net7 over net6. The first family whose language version the corpus's original SDK cannot compile at all. packages.config remains dead: six of 24 cells impossible.

## Language version

C# 13.0, taken as the default of the target framework. `LangVersion` is deliberately
never written to any project file, which is what keeps the family axis one number
instead of two.

The domain layer is written to that language subset exactly, and the lock is
verified by execution rather than asserted:

```
csc -langversion:13.0   ->  clean
csc -langversion:12.0   ->  error CS8025: Feature 'async function' is not available
```

## Build

```bash
./build.sh
```

Restore will not succeed on a host where NuGet is unreachable; see `dataset.json`
`blockedHosts`.

## Test

```bash
./build.sh          # the test step is wired into the build
```

19 tests are declared. They are **not** executed in this corpus's build, because no
test framework can be restored.

## Tool data folders

This repo carries only `Tool Invalid (Synthetic Data)` from testable-platform/csharp-corpus's original per-branch task-data folders.

| Folder | What it holds |
|---|---|
| `Tool Invalid (Synthetic Data)` | The same 17 tools, with code a tool **should** flag. The true-positive control. |

This repo's own folder carries five version folders per tool -- `netfx45`, `netfx46`, `netcoreapp30`, `net9`, `net10`. Each compiles at its own C# level, and its
`LanguageMarker` is rejected one level below, so the version a folder claims is
verified by execution rather than asserted.

**This repo's own folder contains no project
manifest** -- no `.csproj`, `.sln`, `packages.config` or lockfile. One there
would make the platform treat the folder as a project of its own and run the
whole roster against it.

