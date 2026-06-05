<p align="center">
  <img src="https://raw.githubusercontent.com/clonio-dev/.github/main/profile/banner.svg" alt="Clonio — Database Cloning & Anonymization" width="100%"/>
</p>

<h3 align="center">
  Clone production databases. Anonymize PII. Stay GDPR-compliant.<br/>
  <sub>A terminal-first CLI. Runs in your infrastructure. MIT licensed.</sub>
</h3>

<p align="center">
  <a href="https://clonio.dev"><img src="https://img.shields.io/badge/website-clonio.dev-0ea5e9?style=flat-square&labelColor=0f172a" alt="Website"/></a>&nbsp;
  <a href="https://clonio.dev/docs/getting-started/introduction"><img src="https://img.shields.io/badge/docs-read_the_docs-6366f1?style=flat-square&labelColor=0f172a" alt="Documentation"/></a>&nbsp;
  <a href="https://github.com/clonio-dev/clonio-cli/blob/main/LICENSE.md"><img src="https://img.shields.io/badge/license-MIT-22c55e?style=flat-square&labelColor=0f172a" alt="License: MIT"/></a>&nbsp;
  <img src="https://img.shields.io/badge/self--hosted-runs_in_your_infra-22d3ee?style=flat-square&labelColor=0f172a" alt="Self-hosted"/>&nbsp;
  <a href="https://github.com/sponsors/clonio-dev"><img src="https://img.shields.io/badge/sponsor-GitHub_Sponsors-ea4aaa?style=flat-square&labelColor=0f172a&logo=githubsponsors&logoColor=ea4aaa" alt="Sponsor on GitHub"/></a>
</p>

---

## What is Clonio?

**Clonio** is a command-line tool that clones production-like database data into development, test, staging, and CI environments — applying anonymization, schema synchronization, key remapping, and signed audit logs along the way.

Development teams need production-like data to build and test effectively — but production databases contain personally identifiable information (PII) that **cannot** be used outside production. GDPR, DSGVO, and other privacy regulations make this non-negotiable. A single unmasked email address in a test environment can lead to compliance violations and fines.

Clonio solves this: it reads from your source database, applies the transformation rules you define in a `.cloning.yaml` file, synchronizes the target schema where configured, and writes clean, privacy-compliant data to your target environment. Fully automated, fully auditable — straight from the terminal.

There is **no web application to operate**. Clonio is built for terminal-first workflows: local scripts, Docker, Composer, cron jobs, GitHub Actions, GitLab CI, and other pipeline runners.

### Core Capabilities

```
┌─────────────────┐         ┌──────────────────┐         ┌──────────────────┐
│   Source DB     │  ────►  │   clonio CLI     │  ────►  │   Dev / Test /   │
│  (production)   │         │  Anonymization   │         │   Staging / CI   │
└─────────────────┘         └──────────────────┘         └──────────────────┘
                                     ▲
                     Fake · Mask · Hash · Null · Static · Keep
```

- **Multi-database support** — MySQL, MariaDB, PostgreSQL, and more. Cross-database cloning supported.
- **Connection management** — Store source and target connections in a local `clonio.json` file with encrypted passwords.
- **PII-aware config generation** — Inspect a source database and generate a `.cloning.yaml` with suggested transformations from a built-in PII matcher set.
- **Column transformations** — Use `fake`, `hash`, `mask`, `null`, `static`, or `keep` strategies per column, per table.
- **Row selection** — Transfer full tables or only the first/last N rows. Foreign-key aware so referential integrity is preserved.
- **Schema synchronization** — Create missing tables and optionally add or remove columns/tables on the target.
- **Key remapping** — Replace primary keys and rewrite foreign keys consistently across the dataset.
- **Signed audit logs** — Every run produces a cryptographically signed (HMAC-SHA256), tamper-evident audit artefact documenting what was run and which configuration was applied.
- **Audit delivery channels** — Ship audit logs to local files, stdout/stderr, S3, email, Slack, Microsoft Teams, or ntfy.
- **CI-friendly execution** — `--ci` mode, meaningful exit codes, Docker, and Composer integration for pipelines.

### Self-Hosted

Clonio runs **inside your infrastructure**. Your data never leaves your network. No cloud dependency, no data transfer to third parties. You control where it runs, how it's configured, and who has access.

---

## License

Clonio CLI is **MIT licensed**. Everyone can use it freely — including commercial users — with no usage restrictions, no per-seat pricing, and no feature gates.

> Full license text: [`LICENSE.md`](https://github.com/clonio-dev/clonio-cli/blob/main/LICENSE.md)

### Support Clonio via GitHub Sponsors

There is no pricing plan for the CLI. If Clonio is useful to you or your organization, sponsorships and donations are welcome through **[GitHub Sponsors](https://github.com/sponsors/clonio-dev)**. Sponsorship helps fund ongoing maintenance, new database drivers, better anonymization strategies, and documentation.

<p align="center">
  <a href="https://github.com/sponsors/clonio-dev">
    <img src="https://img.shields.io/badge/%E2%9D%A4%EF%B8%8F_Become_a_Sponsor-GitHub_Sponsors-ea4aaa?style=for-the-badge&labelColor=0f172a&logo=githubsponsors&logoColor=ea4aaa" alt="Become a Sponsor"/>
  </a>
</p>

---

## Getting Started

Download the binary for your platform from the [latest release](https://github.com/clonio-dev/clonio-cli/releases/latest) — the platform binaries are fully self-contained, no PHP required.

```bash
# macOS (Apple Silicon)
mv clonio-macos-aarch64 clonio
chmod +x clonio
mv clonio /usr/local/bin/clonio

# linux (x86_64/aarch64)
mv clonio-linux-* clonio
chmod +x clonio

# Then bootstrap Clonio and run your first clone
clonio init
clonio connection:add production --production
clonio connection:add local-dev
clonio cloning:dump --connection production
clonio cloning:run production.cloning.yaml --target local-dev
```

Prefer Docker, Phar or Composer? Run it as a one-off container or require it as a dev dependency:

```bash
# Docker
docker run --rm -v "$(pwd)":/workspace ghcr.io/clonio-dev/clonio:latest --version

# Composer (dev dependency)
composer require --dev clonio-dev/clonio-cli
```

> See the [Installation Guide](https://clonio.dev/docs/getting-started/installation) for all platforms, Docker tags, and CI setup.

---

## How It Works

1. **Add connections** — Configure your source (production) and target (dev/staging/CI) database credentials in `clonio.json`.
2. **Generate a config** — Run `cloning:dump` to inspect the source and produce a `.cloning.yaml` with PII-aware transformation suggestions.
3. **Review & edit** — Tune anonymization strategies per column, set row limits, and configure key remapping in the YAML file.
4. **Run** — Execute manually or in CI. Clonio synchronizes the schema, transfers data in chunks, and applies all transformation rules.
5. **Audit** — Review the cryptographically signed audit log for compliance documentation, and deliver it to your chosen channels.

---

## Documentation

Full documentation lives at **[clonio.dev](https://clonio.dev)** (served via GitHub Pages):

- [Introduction](https://clonio.dev/docs/getting-started/introduction)
- [Installation](https://clonio.dev/docs/getting-started/installation)
- [First clone](https://clonio.dev/docs/getting-started/first-clone)
- [`.cloning.yaml` reference](https://clonio.dev/docs/cloning-config/cloning-yaml-reference)
- [Command reference](https://clonio.dev/docs/reference/command-reference)

---

<p align="center">
  <sub>Built in Germany. Made for teams who take data privacy seriously.</sub><br/>
  <sub>
    <a href="https://clonio.dev">Website</a> ·
    <a href="https://clonio.dev/docs/getting-started/introduction">Documentation</a> ·
    <a href="https://github.com/sponsors/clonio-dev">Sponsor</a> ·
    <a href="https://github.com/clonio-dev/clonio-cli/issues">Issues</a>
  </sub>
</p>
