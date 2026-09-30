# Changelog

Changes to the public contract of this repository: the issue and discussion forms, their field IDs, the labels they apply, and the policies in this repository. Links that prefill a form (`/issues/new?template=<file>&<field-id>=<value>`) depend on the file names and field IDs listed here.

Release notes of the products live at cademi.dev: [API and webhooks](https://cademi.dev/api/changelog) and [CLI](https://cademi.dev/cli/changelog).

## 2026-09-30

This repository covers Cademí MCP, the CLI, the API v3, and webhooks.

- New form `mcp_problem.yml`, labels `mcp`, `bug`, `needs-triage`. Field IDs: `area`, `client`, `client-other`, `tool`, `error-code`, `request-id`, `what-happened`, `when`.
- New form `webhook_problem.yml`, labels `webhooks`, `bug`, `needs-triage`. Field IDs: `area`, `payload-version`, `webhook-id`, `delivery-id`, `event`, `account-environment`, `what-happened`, `delivery`.
- New labels: `mcp` and `webhooks`.
- `feature_request.yml`: the `product` field offers `API`, `Webhooks`, `MCP`, `CLI`, and `More than one`.
- Discussion form `q-a.yml`: new field `area`, and the `version` field also takes the API release.
- The release notes of the CLI moved to [cademi.dev/cli/changelog](https://cademi.dev/cli/changelog). This file now records changes to the repository itself.

Unchanged, and still used by `cademi bug`:

- `bug_report.yml`, labels `cli`, `bug`, `needs-triage`. Field IDs: `what-happened`, `area`, `account-environment`, `command`, `version`, `platform`, `environment`, `request-id`.
- `api_problem.yml`, labels `api`, `bug`, `needs-triage`. Field IDs: `endpoint`, `request-id`, `account-environment`, `what-happened`, `exchange`, `release`, `client`, `docs`.
