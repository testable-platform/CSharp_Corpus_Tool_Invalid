# Trivy

Inverse-corpus counterpart to the sibling CSharp-Tools-Clean's **Trivy**
folder. Stays **NOT_INSTALLED** here too -- the blocker is infrastructure
(GitHub Releases + Go module proxy both blocked), not anything about this
corpus being Clean or Invalid, so there is nothing to invert.

Package: github.com/aquasecurity/trivy (Go binary / GitHub release)

Domain: shipping container package manifest scan (ContainerManifestScan)

**Not installed here**: see Notes for why, and what was checked instead.

## What a result would look like

A Trivy filesystem scan of ContainerManifestScan's declared packages would
report known-vulnerable dependencies. Not measurable here: see Notes.

## Command

```bash
trivy fs .
```

## Notes

Trivy ships as a GitHub Release binary or via its own apt repository at
`aquasecurity.github.io`; both return 403 at this sandbox's egress proxy
(measured directly), and `go install` is blocked the same way
(`proxy.golang.org` not in the allowlist). No package for it exists in
Ubuntu's own apt archive. Identical to the sibling Clean corpus's own
finding.

## Per-family results

| Family | Toolchain | Compiles | Result |
|---|---|---|---|
| `netcoreapp30` | netcoreapp3.0 (manual csc, SDK 8.0.131's compiler + installed 8.0.31 runtime) | yes | NOT_INSTALLED |

This repo carries only the `netcoreapp30` family.
