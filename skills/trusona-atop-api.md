---
name: atop-api
description: Use when an agent needs to exercise the Trusona Account Takeover Protect (ATOP) identity-verification APIs — creating and polling verifications, running DMV/MNO driver-license ID matches, or pulling scanned documents and risk scores. Provides runnable bash scripts, not just docs.
---

# ATOP — Trusona Account Takeover Protect (ATOP) identity-verification APIs

ATOP is Trusona's Account Takeover Protect identity-verification platform. It exposes two APIs,
both at `https://authcloud.trusona.net`, both authenticated with a Bearer JWT:

1. **Verification API** (v2.2.0) — create a verification, the subject scans an ID
   via a hosted link, you read risk + verifier outcomes.
2. **Driver License Verification API** (v1.0.0) — submit identity data, get
   asynchronous field-level DMV/MNO match results.

**This skill is for *doing*, not reading.** Each workflow below is a runnable
script in `scripts/`. Edit an example JSON body, run the script, read its
output, chain to the next step. The scripts print human-readable summaries (id,
status, key fields) to stdout, not raw JSON; for the full JSON response pipe the
relevant endpoint through `curl`/`jq` directly (see `reference/`).

## Setup (once)

```bash
export ATOP_TOKEN='eyJ...'      # Bearer JWT, from the Trusona dashboard
export ATOP_BASE_URL='https://authcloud.trusona.net'   # optional; this is default
```

Requires `bash`, `curl`, `jq`. Full detail: [reference/auth.md](reference/auth.md).
Smoke-test it: `scripts/doctor.sh` for local checks, or
`scripts/doctor.sh --connectivity` once `ATOP_TOKEN` is set.

## Pick your workflow

| Your intent | Run | Reference |
|-------------|-----|-----------|
| Create an ID verification (scan + DMV/MNO + SMS/email link) | `scripts/create-verification.sh examples/verification-request.json` | [verification-api.md](reference/verification-api.md) |
| Wait for that verification to resolve, see risk + per-verifier match data | `scripts/poll-verification.sh <id>` | [verification-api.md](reference/verification-api.md) |
| Pull documents / images / risk scores / verifier match data | `scripts/get-results.sh <id> --all` | [verification-api.md](reference/verification-api.md) |
| List recent verifications without hand-writing the required `since` query | `scripts/list-verifications.sh --since 2026-06-01` | [verification-api.md](reference/verification-api.md) |
| Match supplied identity data against DMV/MNO records | `scripts/id-verify.sh examples/id-verification-request.json` | [id-verification-api.md](reference/id-verification-api.md) |
| Wait for that ID match, see per-field results | `scripts/poll-id-verification.sh <id>` | [id-verification-api.md](reference/id-verification-api.md) |
| Use callbacks instead of long polling | Set `callbackUrl`, then re-fetch the result on receipt | [webhooks.md](reference/webhooks.md) |

Every script supports `--help`.

## Key facts that trip agents up

- **Two different status models.** A *Verification* lifecycle `status` is only
  `WAITING | SCANNED | EXPIRED` — there is **no SUCCESS/FAILURE**. Its outcome is in
  `overallRisk` + `verifierChecks[]` + `riskScores[]`. An *ID verification* uses
  per-source `PENDING | SUCCESS | FAILURE | FATAL` on `dmv`/`mno`.
- **Don't send `requestedVerifiers`.** It's being deprecated — which verifiers
  run is decided server-side, not by the request. The spec still documents the
  field, but the skill rejects it; `create-verification.sh` blocks any request
  that includes it. Verifier outcomes still return via `verifierChecks[]`.
- **Date formats differ.** Verification `subject.dateOfBirth` is `MM/DD/YYYY`;
  ID-verification `dateOfBirth` is `YYYY-MM-DD`.
- **ID verifications need a unique `transactionId`** (UUID) per request — the script
  auto-generates one from the example placeholder.
- **`GET /verifications` requires a `since` query param.**
- The `/document` endpoint returns both masked and unmasked PII in one response;
  default to masked unless full PII is genuinely needed.
- Callback URLs are completion signals, not trusted final results; re-fetch the
  verification with the authenticated API before deciding.

## Maintenance

Scripts/docs are derived from the vendored specs in `openapi/` (see
`openapi/FETCHED.md` for versions + fetch date). Refresh procedure is in the README.

## License

Copyright 2026 Trusona, Inc. Licensed under the Apache License, Version 2.0.
See [LICENSE](LICENSE).
