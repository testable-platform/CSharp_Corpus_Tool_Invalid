# OrderKit - CS_VNETFX46_SDKMSBUILD_NUGETPACKAGESCONFIG_MONO

One branch of the C# tool-evaluation corpus. Test **data**, not a product: tool
execution is not part of the build, and evaluation happens later.

> **This cell cannot exist.** packages.config is only supported by non-SDK-style (legacy) projects. An SDK-style csproj ignores it entirely: NuGet restore reads PackageReference and the packages.config file is inert.
>
> The branch ships the artifacts the cell definition demands, plus this notice. It is *not* quietly backed by a working configuration -- a branch labelled one thing that ran another underneath is the exact silent success this corpus exists to catch.

## Branch

`CS_VNETFX46_SDKMSBUILD_NUGETPACKAGESCONFIG_MONO`

## Cell

| Axis | Value |
|---|---|
| Bundler | SDK-style MSBuild |
| Package manager | NuGet (packages.config) |
| Architecture | Monolith |

Projects:

- `OrderKit` (`src/OrderKit`)

## Target framework

`net46` - .NET Framework 4.6

One patch release below the netstandard2.0 boundary. Out of support since 26 April 2022. The next TFM up, net461, is where netstandard2.0 support begins -- and that single step would light 19 metrics that are dark here.

## Language version

C# 6, taken as the default of the target framework. `LangVersion` is deliberately
never written to any project file, which is what keeps the family axis one number
instead of two.

The domain layer is written to that language subset exactly, and the lock is
verified by execution rather than asserted:

```
csc -langversion:6   ->  clean
csc -langversion:5   ->  error CS8025: Feature 'async function' is not available
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

