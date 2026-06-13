# Security Policy

Tessio is a self-hosted ITSM platform. Because you run it on your own
infrastructure, security is a shared responsibility: the project ships secure
defaults and patches vulnerabilities, and you keep your instance updated and
configured according to the hardening guidance in the documentation.

## Reporting a vulnerability

**Please do not report security issues in public GitHub issues, discussions, or
pull requests.** Public disclosure before a fix is available puts every
self-hosted instance at risk.

Report vulnerabilities privately through GitHub's private advisory flow:

1. Open the **Security** tab of this repository.
2. Click **Report a vulnerability**.
3. Include a description, the affected version, impact, and steps to reproduce.

This opens a private channel visible only to the maintainers.

If you are unable to use GitHub's private reporting, open a
[GitHub Discussion](https://github.com/tessio-ai/tessio-community/discussions)
asking a maintainer to arrange a private channel. Do not include exploit
details in the public post.

## What to expect

- We aim to acknowledge your report within **3 business days**.
- We will confirm the issue, determine the affected versions, and keep you
  updated on remediation.
- When a fix ships, we publish a security advisory and credit the reporter
  unless you ask to remain anonymous.

## Supported versions

Security fixes land on the **latest released version** and the `main` branch.
Run the most recent release; older versions are not back-patched. Watch the
repository's releases to be notified of security updates.

## Scope

**In scope:** the Tessio application (API, web console, worker, runner) and the
official deployment artifacts (Docker Compose files and the Helm chart) in this
repository.

**Out of scope:** already-public vulnerabilities in third-party dependencies
(report those upstream), issues requiring a compromised host or physical
access, and findings against a deployment that ignores the documented hardening
guidance.

## Hardening your deployment

Keeping your instance on the latest release is the single most important
control. See the self-hosting documentation for recommended configuration:
secrets management, limiting network exposure, terminating TLS, and the
built-in script sandbox, SSRF protections, and Content-Security-Policy.
