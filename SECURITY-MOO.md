# Moo security patch for Sub2API 0.1.183

This branch preserves upstream release `v0.1.183` and updates only the Go
dependency graph needed to remove the fixable HIGH vulnerabilities found in
the published upstream container image on 2026-08-28.

Updated direct dependencies:

- `golang.org/x/image`: `v0.41.0` to `v0.43.0` for CVE-2026-46602.
- `golang.org/x/mod`: `v0.37.0` to `v0.40.0` for CVE-2026-56864 and
  CVE-2026-56865.

`go get` also advanced the compatible `golang.org/x/*` transitive modules
recorded in `backend/go.mod` and `backend/go.sum`. No application behavior or
frontend source was changed.

Verification for the patch:

```bash
cd backend
go mod tidy
go test ./...
```

The complete backend test suite passed with Go 1.27.0. The deployment image is
built from the annotated Git tag `v0.1.183-moo.1`, scanned without vulnerability
suppression, and published as `ghcr.io/moohouse/sub2api:0.1.183-moo.1`.
