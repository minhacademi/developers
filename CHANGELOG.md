# CLI changelog

Release notes of the `cademi` CLI. API release notes: https://cademi.dev/api/changelog

## 0.1.11 - 2026-09-27

- Requests are validated against the API contract embedded in the CLI before they are sent. A query parameter or body field that the operation does not accept, including nested fields and fields passed with `--data`, exits with code `2` without calling the API. The message names the field or parameter, its JSON path, and what the operation accepts. This applies to `cademi api`, when the path matches a known operation, and to the resource commands.
- `cademi api --skip-validation` sends the request as is, for endpoints newer than the embedded API release.
- `cademi api -H 'Idempotency-Key: ...'` works like `--idempotency-key`. Operations that require an `Idempotency-Key` always get one.
- A `503` from the API without a `Retry-After` header, such as `storage_unavailable`, is not retried: the command returns right away with exit code `8`. A `503` with `Retry-After`, and a `503` without an API error envelope, are retried.

## 0.1.10 - 2026-09-26

- Internal improvements. No changes to commands, flags, exit codes, installation, or updates.

## 0.1.9 - 2026-09-26

- Internal improvements. No changes to commands, flags, exit codes, installation, or updates.

## 0.1.8 - 2026-09-26

- `cademi env` shows `max_retries` and `max_retry_wait`, and `client_request_id` when `CADEMI_CLIENT_REQUEST_ID` is set, each with where its value comes from.
- The `--output` help of the commands that print text by default (`auth status`, `env`, `profiles list`, `commands`, `doctor`, `config validate`, and `config plan`) says so.

## 0.1.7 - 2026-09-26

- `CADEMI_CLIENT_REQUEST_ID` sends your own identifier in the `X-Client-Request-Id` header of every request: up to 64 letters, digits, `.`, `_`, or `-`. The API returns it in the response and records it in the request log. An invalid value exits with code `2`.
- `CADEMI_MAX_RETRIES` (default `3`; `0` turns retries off) and `CADEMI_MAX_RETRY_WAIT` (default `60s`) control automatic retries. A `429` that asks for a longer wait than `CADEMI_MAX_RETRY_WAIT` fails right away.
- `cademi profiles list` shows the API URL and your account's platform address in separate columns, `API` and `PLATFORM`, and `--json` includes `platform`.

## 0.1.6 - 2026-09-26

- `cademi bug` no longer puts your account's platform address, the credential ID, or the profile name in the public issue.
- In `cademi env`, the operating system and architecture are reported as `os_arch`; `platform` is only your account's platform address.
- The browser page after sign-in says "Cademí CLI authorized" only for a valid response. A rejected `iss` shows "Authorization rejected", and `account_not_eligible` has its own page.
- `cademi auth logout --help` explains how to revoke the credential, and the `--base-url` help describes it as the Cademí API URL.

## 0.1.5 - 2026-09-26

- `cademi auth login --platform <address>` goes straight to your account's platform instead of the platform selector in the browser. The address is saved in the profile, reused on the next login, and shown by `cademi auth status` and `cademi env`.
- Human login checks the `iss` parameter returned by the authorization (RFC 9207). It rejects a response whose `iss` does not match the issuer, or that has no `iss` when the server announces support for it.
- Choosing Deny in the browser ends the login right away, without saving anything.
- When the platform refuses the administrator, the login ends right away with the reason: `mfa_required` (two-factor authentication is not turned on), `account_not_eligible` (the account cannot authorize the CLI), or `platform_mismatch` (the administrator belongs to another platform; the message suggests `--platform`).
- The base URL prompt is now "Cademí API URL". Clearer messages while waiting for the browser and for credentials that require human mode.
- Built for API release 3.4.7.

## 0.1.4 - 2026-09-25

- `cademi bug --api` opens the API bug report instead of the CLI one, with `--endpoint` and `--request-id` filled in. `--request-id` also works for CLI bugs.
- Issues now go to this repository, `minhacademi/developers`, which takes reports for both the API and the CLI.
- Built for API release 3.4.5.
- Mutually exclusive flags exit with code `2`.

## 0.1.3 - 2026-09-25

- `cademi commands` lists every command in one call, with the API route, permission, arguments, and flags. `--json` for scripts and AI agents, `--brief` for a small index, and a prefix narrows the list (`cademi commands products`).

## 0.1.2 - 2026-09-25

- `cademi bug` opens a new issue in this repository with your CLI version, platform, and settings filled in. Nothing is sent until you submit it in the browser. `--print` prints the URL instead.
- `--all` now works on every paginated list, including users, enrollments, access schedules, comments, and questions.
- `cademi api` keeps query parameter names as written, such as `tag_id[]`.
- A missing credential exits with code `3`, like other authentication errors.

## 0.1.1 - 2026-09-25

- `cademi env` shows the effective settings and where each value comes from (flag, environment variable, config file, profile, keychain, or default). `cademi env <name>` prints a single value.

## 0.1.0 - 2026-09-25

First release.

- Every API v3 operation as a command, with the API route, permission, and body fields in `--help`.
- Human sign-in (OAuth in the browser plus a credential) and autonomous mode (credential only), with profiles and secrets in the operating system keychain.
- `cademi api`, `cademi listen` (with signed forwarding to a local endpoint), `cademi config validate/plan/apply`, `cademi sandbox reset/run`, `cademi upload`, `cademi download`, `cademi operations wait`, and `cademi doctor`.
- Output as a table, JSON, YAML, or filtered with `--jq`, and stable exit codes.
- Installers for macOS, Linux, and Windows, and signed automatic updates.
