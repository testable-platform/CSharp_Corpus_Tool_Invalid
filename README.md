# OrderKit - CS_VNETCOREAPP30_CAKE_PAKET_MONO

One branch of the C# tool-evaluation corpus. Test **data**, not a product: tool
execution is not part of the build, and evaluation happens later.

## Branch

`CS_VNETCOREAPP30_CAKE_PAKET_MONO`

## Cell

| Axis | Value |
|---|---|
| Bundler | Cake |
| Package manager | Paket |
| Architecture | Monolith |

Projects:

- `OrderKit` (`src/OrderKit`)

## Target framework

`netcoreapp3.0` - .NET Core 3.0

In support until 3 March 2020, and above the netstandard2.0 boundary, so Coverlet and OpenTelemetry are held out by NuGet alone (exit 4) rather than by the target framework (exit 3). This is also the first target FIRST family off the .NET Framework line, and the crossing the netfx472 record predicted. packages.config does not exist on .NET Core at all, so SIX of the 24 cells are now impossible rather than four -- the grid did not survive the crossing intact, and that is the finding, not a defect. Out of support since 3 March 2020 (3.0 was superseded by 3.1 within months), which is why it is the shortest-lived target framework in the corpus.

## Language version

C# 8.0, taken as the default of the target framework. `LangVersion` is deliberately
never written to any project file, which is what keeps the family axis one number
instead of two.

The domain layer is written to that language subset exactly, and the lock is
verified by execution rather than asserted:

```
csc -langversion:8.0   ->  clean
csc -langversion:7.3   ->  error CS8025: Feature 'async function' is not available
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

