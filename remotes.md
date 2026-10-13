# Remotes convention

This repo is a **fork** of the Eclipse Minimum Viable Dataspace (MVD) — the
runnable launcher stack (control plane, data plane, identity hub, issuer
service). Three-remote setup.

| Remote | URL | Purpose |
|---|---|---|
| `upstream` | `https://github.com/eclipse-dataspace-hub/MinimumViableDataspace.git` | The real upstream. Fetched weekly via `.github/workflows/upstream-sync.yml`; also fetchable manually. |
| `origin` | `https://github.com/fit-intern-oaf/mvd-oaf.git` | FIT staging. Daily pushes land here. |
| `consortium` | `https://github.com/openaiflex/mvd-oaf.git` | Public consortium org, from first stable release onward. |

## Daily workflow

```bash
# Pull upstream fixes
git fetch upstream
git checkout upstream        # local tracking branch of MVD:main
git reset --hard upstream/main
git push origin upstream --force-with-lease

# Normal dev
git checkout main
git merge upstream           # or rebase, per team preference
git push origin main
```

## Why this fork exists

Per ADR-0001 (revised 2026-10-12) and ADR-0002, `connector-edc` is the EDC
*library* fork and `mvd-oaf` is the *runnable launcher* fork. MVD inherits
four Dockerfiles (`launchers/{controlplane,dataplane,identity-hub,issuerservice}`)
which become the actual deployable images tracked in `core/manifest.yaml`.

## Contributing back to upstream

Per ADR-0003: non-OpenAIFlex-specific fixes go upstream within 10 working days.

```bash
# Push the branch to a personal fork, then open a PR against
# eclipse-dataspace-hub/MinimumViableDataspace.
git push personal fix/some-upstream-issue
```

## Promotion to consortium

See `../README.md` → "Staging → consortium promotion".
