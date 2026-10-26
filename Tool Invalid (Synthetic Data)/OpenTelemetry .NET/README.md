# OpenTelemetry .NET

Inverse-corpus counterpart to the sibling CSharp-Tools-Clean's
**OpenTelemetry .NET** folder. Stays **NOT_INSTALLED** here too -- the
blocker is infrastructure (NuGet), not anything about this corpus being
Clean or Invalid, so there is nothing to invert.

Package: OpenTelemetry / OpenTelemetry.Exporter.Console (NuGet)

Domain: signal tower diagnostic pings (SignalTowerPings)

**Not installed here**: see Notes for why, and what was checked instead.

## What a result would look like

A real `TracerProvider` wired to an in-memory exporter would confirm
SignalTowerPings emits spans with the expected attributes (or, for this
corpus, would confirm it does not). Not measurable here: see Notes.

## Command

```bash
dotnet run
```

## Notes

Every OpenTelemetry .NET package (`OpenTelemetry`,
`OpenTelemetry.Exporter.Console`, etc.) ships only on NuGet, which this
sandbox's egress proxy refuses; there is no apt package and no
dependency-free way to construct a real SDK `TracerProvider` without the
SDK assembly itself. Identical to the sibling Clean corpus's own finding.

## Per-family results

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netfx45` | .NET Framework 4.5 (Mono 6.8.0.105 BCL profile 4.5) | yes | NOT_INSTALLED |

This repo carries only the `netfx45` family.
