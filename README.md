# MaxKB for LazyCat

- Upstream: https://github.com/1Panel-dev/MaxKB
- Package: `community.lazycat.app.maxkb`; upstream version family retains the full `-lts` suffix.
- Official image: `docker.io/1panel/maxkb`; runtime mirror: `docker.1ms.run/1panel/maxkb`.
- Matching source/mirror digests are required; target Linux amd64, LazyCat OS 1.5.0+.
- The upstream all-in-one image contains MaxKB, PostgreSQL and Redis; `/lzcapp/var/data` mounts at `/opt/maxkb`.
- PostgreSQL initialization and MaxKB use the same explicit database user and stable secret; the default bootstrap DB remains `postgres`, so upstream `init.sql` can create `maxkb`.
- Redis and MaxKB use the same stable secret. A stable Django key is injected as well. No production credential values are committed.
- `MAXKB_CONFIG_TYPE=ENV` and `MAXKB_DEFAULT_PASSWORD` initialize the admin password on the first database migration. Browser autofill is configured at `/admin/login`, with automatic submit disabled to avoid repeated failed-login attempts and captcha locks.
- If the account password is changed inside MaxKB, synchronize its deployment parameter. Restart does not reset existing database accounts.
- This is for a new MaxKB v2 installation, not direct reuse of a v1 data directory.

## Verification scope

As explicitly requested, the workflow does not run Docker smoke or login tests. The previous smoke run failed and must not be treated as a successful runtime test. Current checks cover workflow/configuration structure, image digest delivery, versioned LPK construction and artifact SHA256 only.

There is no LazyCat-device runtime or RAG/model/workflow end-to-end validation. Removing the smoke gate does not establish runtime correctness.

Only MiaoMiao community publication is authorized; official-store publication is disabled. Automatic store publishers stay disabled until the verified Release asset is submitted explicitly. No file-chooser interception is bundled. The normal LazyCat login boundary is retained.

Model-provider API credentials must be supplied by the user in MaxKB, and none are bundled.

## Community release

MaxKB 2.10.8-lts is published as MiaoMiao application 656, APPROVED, AI Knowledge category 114. Wish 8 was replied to and completed. Build run 40851252034 succeeded without smoke. The 20992-byte LPK SHA256 is `be2dc759558c8968c6b2a82a994789d78a975d91ca7157d3fcf1eb08a8567f2f`, verified after download. The previous failed runtime check is not reported as passing.
