# OrderKit - CS_VNET10_DOTNETCLI_CPM_MICRO

One branch of the C# tool-evaluation corpus. Test **data**, not a product: tool
execution is not part of the build, and evaluation happens later.

## Branch

`CS_VNET10_DOTNETCLI_CPM_MICRO`

## Cell

| Axis | Value |
|---|---|
| Bundler | .NET CLI |
| Package manager | Central Package Management |
| Architecture | Microservices |

Projects:

- `OrderKit.Domain` (`src/OrderKit.Domain`)
- `OrderKit.Contracts` (`src/OrderKit.Contracts`)
- `OrderKit.Pricing` (`src/Services/OrderKit.Pricing`)
- `OrderKit.Risk` (`src/Services/OrderKit.Risk`)
- `OrderKit.Reporting` (`src/Services/OrderKit.Reporting`)

## Target framework

`net10.0` - .NET 10

The top of the corpus: current LTS, supported to 10 November 2028, and the highest C# version the pinned SDK can compile. The SDK moved once, at net9; this family needs no further move. packages.config remains dead -- six of the 24 cells impossible, seven families running.

## Language version

C# 14.0, taken as the default of the target framework. `LangVersion` is deliberately
never written to any project file, which is what keeps the family axis one number
instead of two.

The domain layer is written to that language subset exactly, and the lock is
verified by execution rather than asserted:

```
csc -langversion:14.0   ->  clean
csc -langversion:13.0   ->  error CS8025: Feature 'async function' is not available
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

