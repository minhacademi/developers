# Opening issues and discussions: guide for AI agents

This repository is the public channel for reports, requests, and questions about Cademí MCP, the `cademi` CLI, the API v3, and webhooks. This file tells an AI agent how to open an issue or a discussion here that Cademí can act on. To learn how to use the products, read the docs at https://cademi.dev (index for LLMs: https://cademi.dev/llms.txt).

## Before you open anything

- **Is it for this repository?** Security vulnerabilities go to the [private report](https://github.com/minhacademi/developers/security/advisories/new), never to an issue or a discussion. Questions about a Cademí account, its plan, or its data go to Cademí support. Pull requests are not accepted (see [CONTRIBUTING.md](CONTRIBUTING.md)).
- **Does it already exist?** Search open and closed issues first, for example `gh issue list -R minhacademi/developers --state all --search "<error code or endpoint>"`. If you find it, add what is new as a comment instead of opening a duplicate.
- **Is it a bug or a question?** A behavior that contradicts the documentation is an issue. How to do something is a discussion.
- **Ask the person first.** Issues and discussions are public and posted under their GitHub account. Show them the title and body, and open it only after they agree.

## Pick the form

| Situation | Form (`template`) | Labels | Include |
|---|---|---|---|
| Cademí MCP: connecting a client, signing in, or a tool call | `mcp_problem.yml` | `mcp`, `bug`, `needs-triage` | client, tool, error `code`, `request_id`, when it happened |
| A webhook delivery that does not arrive, an unexpected body, a signature that does not verify, retries | `webhook_problem.yml` | `webhooks`, `bug`, `needs-triage` | payload version, `Cademi-Webhook-Id`, delivery or event ID, event, headers and body |
| An API response that contradicts the docs, also through the CLI or MCP | `api_problem.yml` | `api`, `bug`, `needs-triage` | endpoint, `request_id`, status and `error.code`, `X-Cademi-Release`, request and response |
| A CLI bug | `bug_report.yml` | `cli`, `bug`, `needs-triage` | command, output with `--debug`, `cademi version`, `cademi env` |
| Installing or updating the CLI | `install_update.yml` | `cli`, `install`, `needs-triage` | platform, install command, output |
| Wrong, unclear, or missing documentation at cademi.dev | `documentation.yml` | `documentation`, `needs-triage` | page URL, the text, the suggested change |
| A new feature | `feature_request.yml` | `enhancement`, `needs-triage` | the product, the task, what you would like |

Which one when two fit:

- **API or CLI:** confirm with `cademi api <METHOD> <path> --debug` or any HTTP client. A wrong raw response is an API bug; a right response shown or handled wrong is a CLI bug.
- **API or webhook:** managing a webhook through the API (`POST /webhooks`) is the API. What the endpoint receives is a webhook problem.
- **API or MCP:** a tool that returns an API error contradicting the API docs is an API bug. Connecting, signing in, or a tool that behaves unexpectedly is an MCP problem.

## Open an issue

The forms are the contract. Their file names and field IDs are listed in [CHANGELOG.md](CHANGELOG.md).

**Best: a prefilled link for the person to review.** Build `https://github.com/minhacademi/developers/issues/new?template=<file>&title=<title>&<field-id>=<value>`, with every value URL-encoded, and give it to the person to check and submit. The form applies its labels. For a CLI problem, `cademi bug --print` prints this link with the CLI version, platform, and settings already filled in, and `cademi bug --api --print` does the same for an API problem.

**With the GitHub CLI**, when the person asked you to submit it: `gh issue create -R minhacademi/developers` with the labels of the form (`--label`), a `--title`, and a `--body` that follows the form, one `### <field label>` heading per field, in the order of the form. Leave a field out only when you do not have it.

**Title:** what fails and where, in a few words, for example `PATCH /products/{product_id} ignores status` or `lesson_progress.completed body has no lesson_id`.

## Open a discussion

- **Q&A** (how to do something): https://github.com/minhacademi/developers/discussions/new?category=q-a
- **Ideas** (not concrete enough for a feature request): https://github.com/minhacademi/developers/discussions/new?category=ideas

Give the link to the person. Say what the task is, what was tried, and what happened, and which product it is about.

## Never include

- API keys (`ck_live_...`, `ck_test_...`), access tokens, OAuth codes, or webhook signing secrets (`whsec_...`).
- Personal data of real people: names, emails, phone numbers, documents, addresses. Replace it with placeholders. A webhook body sent with the masked or full level of detail, and the result of an MCP tool, can carry personal data.
- The `Authorization` or `X-API-Key` header of a request.

The `request_id` of an API or MCP error is safe and is the most useful thing to include: it lets Cademí find the call without any other data.

Write in English.
