# Agents

This file defines guidelines and guardrails for AI coding agents working in this repository.

## Security and Safety Guidelines

AI coding agents must follow these rules at all times when working in this repository.

### Protect Sensitive Data

- Do not read, log, print, or commit secret values such as API keys, tokens, passwords, or credentials. Reference variable names (e.g., `ENV['SECRET_KEY_BASE']`) rather than their values.
- Do not hardcode credentials, connection strings, or secrets into source files, configuration files, or tests.
- Do not expose or transmit personally identifiable information (PII) or customer order/payment data outside the application's defined data boundaries.
- Do not add logging statements that output sensitive fields such as passwords, payment card numbers, session tokens, or customer personal details.
- Treat any value sourced from environment variables, Rails credentials (`config/credentials.yml.enc`), or external secret stores as confidential.

### Prevent Unauthorized Deployments

- Do not push commits directly to `main`, `master`, or any production-facing branch without explicit human approval.
- Do not trigger, modify, or bypass CI/CD pipelines (e.g., CircleCI workflows in `.circleci/`) to initiate a production deployment without explicit approval.
- Do not create or push git tags that follow release naming conventions (e.g., `v*`) unless explicitly instructed to do so.
- Do not modify Kubernetes manifests, Helm charts, or infrastructure configuration in a way that would cause an immediate deployment to a live environment.
- Do not approve or merge pull requests autonomously.

### Avoid Destructive Operations

- Do not force-push (`git push --force`) to any branch.
- Do not delete remote branches or tags.
- Do not drop, truncate, or irreversibly alter database tables or records. Do not run `db:drop`, `db:reset`, or any migration that destroys data without explicit approval.
- Do not run irreversible ActiveRecord migrations (e.g., removing columns or tables) without a corresponding rollback migration being reviewed and approved first.
- Do not delete or overwrite log files, uploaded assets, or any data stored outside version control.
- Do not modify or remove infrastructure definitions (e.g., Kubernetes resources referenced in `kube-state-metrics.md`) in a way that could cause service disruption.
- Prefer additive, reversible changes. When in doubt, stop and ask for human confirmation before proceeding.
