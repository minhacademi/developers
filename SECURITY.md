# Security policy

This policy covers the Cademí API v3 (including webhooks, OAuth, and event streams), Cademí MCP, and the `cademi` CLI.

Please do not report security vulnerabilities in public issues or discussions.

Report them privately through GitHub: go to the [Security tab](https://github.com/minhacademi/developers/security) of this repository and choose **Report a vulnerability**. Include the affected endpoint, MCP tool, or CLI version (`cademi version`), the `request_id` of a call when you have one, and the steps to reproduce. Do not include real credentials or personal data.

If a credential may have been exposed, revoke it in your Cademí dashboard right away. Revoking a credential ends every session that uses it. If a webhook signing secret may have been exposed, rotate it.

Every CLI release is signed. `cademi update` verifies the signature before it installs a new version.
