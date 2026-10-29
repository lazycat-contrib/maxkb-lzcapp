# MaxKB for LazyCat

- Upstream: https://github.com/1Panel-dev/MaxKB
- Package: `community.lazycat.app.maxkb`; initial upstream version 2.10.8-lts (LTS release family).
- Official image: `docker.io/1panel/maxkb`; runtime mirror: `docker.1ms.run/1panel/maxkb`.
- Image delivery requires matching source/mirror digests; target Linux amd64, OS 1.5.0+.
- Single container runs MaxKB with embedded PostgreSQL and Redis; persistent state at `/lzcapp/var/data` → `/opt/maxkb`.
- Initial admin `admin` gets a random deployment-parameter password via `MAXKB_CONFIG_TYPE=ENV` + `MAXKB_DEFAULT_PASSWORD`. No hardcoded production credential; login form requires first-time password change, so simple autofill is intentionally not configured.
- Login throttling is upstream behavior: repeated failures trigger a captcha, then a temporary lock. This is expected.
- Telemetry/model providers must be configured in-app with user API keys; none are bundled.
- Only MiaoMiao community publication is authorized. Both automatic store publishers are initially disabled; publish the verified versioned Release URL after checking its SHA256.

The workflow smoke-tests the exact upstream image: readiness wait (first boot initializes DB and loads the local embedding model, several minutes), successful admin login with the deployment password, rejection of a wrong password, and credential persistence across restart.

These are runner-level endpoint checks, not a LazyCat-device installation test. RAG quality, model connectivity, workflow execution and browser UI interactions have not been end-to-end tested on a LazyCat device.

Existing organization secrets `APPSTORE_URL`, `APPSTORE_TOKEN`, and optional `PRIVATE_STORE_GROUP_CODES` are referenced explicitly, never committed as values.
