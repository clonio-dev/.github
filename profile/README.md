<p align="center">
  <img src="https://raw.githubusercontent.com/clonio-dev/.github/main/profile/banner.svg" alt="Clonio — Database Cloning & Anonymization" width="100%"/>
</p>

<h3 align="center">
  Clone production databases. Anonymize PII. Stay GDPR-compliant.<br/>
  <sub>Self-hosted. Source-available. Built for teams who care about data privacy.</sub>
</h3>

<p align="center">
  <a href="https://clonio.dev"><img src="https://img.shields.io/badge/website-clonio.dev-0ea5e9?style=flat-square&labelColor=0f172a" alt="Website"/></a>&nbsp;
  <a href="https://clonio.dev/docs"><img src="https://img.shields.io/badge/docs-read_the_docs-6366f1?style=flat-square&labelColor=0f172a" alt="Documentation"/></a>&nbsp;
  <img src="https://img.shields.io/badge/license-Fair_Use-a78bfa?style=flat-square&labelColor=0f172a" alt="License: Clonio Fair Use"/>&nbsp;
  <img src="https://img.shields.io/badge/self--hosted-runs_in_your_infra-22d3ee?style=flat-square&labelColor=0f172a" alt="Self-hosted"/>&nbsp;
  <a href="https://github.com/sponsors/clonio-dev"><img src="https://img.shields.io/badge/sponsor-GitHub_Sponsors-ea4aaa?style=flat-square&labelColor=0f172a&logo=githubsponsors&logoColor=ea4aaa" alt="Sponsor on GitHub"/></a>
</p>

---

## What is Clonio?

**Clonio** is a self-hosted database cloning tool that creates safe, anonymized copies of production databases for development, testing, and staging environments.

Development teams need production-like data to build and test effectively — but production databases contain personally identifiable information (PII) that **cannot** be used outside production. GDPR, DSGVO, and other privacy regulations make this non-negotiable. A single unmasked email address in a test environment can lead to compliance violations and fines.

Clonio solves this: it reads from your production database, applies the anonymization rules you define, and writes clean, privacy-compliant data to your target environments. Fully automated, fully auditable.

### Core Capabilities

```
┌─────────────────┐         ┌──────────────────┐         ┌──────────────────┐
│   Production    │  ────►  │     Clonio       │  ────►  │   Dev / Test /   │
│    Database     │         │  Anonymization   │         │    Staging DB    │
└─────────────────┘         └──────────────────┘         └──────────────────┘
                                     ▲
                     Fake · Mask · Hash · Null · Static
```

- **Multi-database support** — MySQL, MariaDB, PostgreSQL, SQL Server. Cross-database cloning supported (e.g., MySQL → PostgreSQL).
- **Column-level anonymization** — Replace sensitive columns with fake data, hash values, masked content, null, or static values. Configured per column, per table.
- **Row selection** — Copy full tables, first X rows, or last X rows. Reduce dataset size while keeping relevant data.
- **Foreign key awareness** — Child tables are automatically filtered when parent tables use row selection. Referential integrity is always preserved.
- **Schema replication** — Source schema is inspected and mirrored to the target. New columns and tables are created automatically.
- **Scheduling & triggers** — Run manually, on a cron schedule, or via API trigger URLs for CI/CD integration.
- **Webhook notifications** — HTTP webhooks on success or failure for integration with Slack, Teams, or custom workflows.
- **Signed audit trail** — Every run generates a cryptographically signed (HMAC-SHA256) audit report documenting configuration, execution, and GDPR compliance status. Printable and shareable via public links.
- **Real-time monitoring** — Live execution console with timestamped logs for every step.

### Self-Hosted

Clonio runs **inside your infrastructure**. Your data never leaves your network. No cloud dependency, no data transfer to third parties. You control where it runs, how it's configured, and who has access.

---

## Licensing — Clonio Fair Use License

Clonio is **source-available** under the **Clonio Fair Use License (CFUL)**. Our goal is simple: make GDPR-compliant dev environments accessible to everyone — while businesses that benefit commercially contribute to the project's sustainability.

| |                  **Personal & Open Source**                  |           **Small Business**            |              **Business**              |
|---|:------------------------------------------------------------:|:---------------------------------------:|:--------------------------------------:|
| **Price** |                           **Free**                           |        **€39 (~~@59~~) / month**        |      **€99 (~~€199~~) / month**       |
|  |                                                              |            2026 Launch Price            |      2026 Launch Price       |
|  |                                                              |            €468 / year · billed annually in advance            |      €1188 / year · billed annually in advance       |
| **Who** | Individuals, students, hobbyists, open source projects, NGOs | Companies with up to €1M annual revenue | Companies with over €1M annual revenue |
| **All features** |                              ✓                               |                    ✓                    |                   ✓                    |
| **Commercial use** |                     Non-commercial only                      |                    ✓                    |                   ✓                    |
| **Self-hosted** |                              ✓                               |                    ✓                    |                   ✓                    |
| **Source access** |                              ✓                               |                    ✓                    |                   ✓                    |

### Why this model?

**Every open source project should be able to run dev and test stages with GDPR and PII-compliant data.** Privacy compliance shouldn't be a privilege reserved for companies with big budgets. Clonio is free for the open source community — no asterisks, no feature gates.

**Businesses that earn revenue from data on their dev stages should contribute.** If your organization processes production data in non-production environments to build, test, or demo commercial products, Clonio saves you the cost and risk of manual data sanitization. The license fee funds continued development and ensures the tool stays maintained and evolving.

**Fair use means fair for everyone.** You run Clonio on your own servers. You control your own data. The license simply asks commercial users to pay a fair price for the value they receive — no per-seat pricing, no usage metering, no surprise invoices.

> Full license text: [`LICENSE.md`](https://github.com/clonio-dev/clonio/blob/main/LICENSE.md)

### Support Clonio via GitHub Sponsors

Commercial licenses and community sponsorships are handled through **[GitHub Sponsors](https://github.com/sponsors/clonio-dev)**. This is the easiest way to get your license and support the project at the same time:

- **Small Business (€59/mo)** and **Business (€199/mo)** tiers are available as sponsorship tiers — your sponsorship _is_ your license.
- **Community sponsors** at any amount help fund development, documentation, and database driver support.
- All sponsors get listed as supporters of GDPR-compliant open source tooling.

<p align="center">
  <a href="https://github.com/sponsors/clonio-dev">
    <img src="https://img.shields.io/badge/%E2%9D%A4%EF%B8%8F_Become_a_Sponsor-GitHub_Sponsors-ea4aaa?style=for-the-badge&labelColor=0f172a&logo=githubsponsors&logoColor=ea4aaa" alt="Become a Sponsor"/>
  </a>
</p>

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/clonio-dev/clonio.git

# Install dependencies
composer install && npm install

# Configure your environment
cp .env.example .env
php artisan key:generate

# Run migrations
php artisan migrate

# Build frontend assets
npm run build

# Start the application
php artisan serve
```

> See the [Installation Guide](https://clonio.dev/docs/getting-started/installation) for Docker setup, queue worker configuration, and production deployment.

---

## How It Works

1. **Add connections** — Configure your source (production) and target (dev/staging) database credentials.
2. **Create a cloning** — Select tables, define anonymization rules per column, set row limits, configure scheduling.
3. **Execute** — Run manually, on schedule, or trigger via API. Clonio replicates the schema, transfers data in chunks, and applies all transformation rules.
4. **Audit** — Review the cryptographically signed audit trail for compliance documentation.

---

## Tech Stack

Clonio is built with:

- **[Laravel](https://laravel.com)** — PHP application framework
- **[Inertia.js](https://inertiajs.com) + [Vue 3](https://vuejs.org)** — Full-stack SPA without API complexity
- **[Tailwind CSS](https://tailwindcss.com)** — Utility-first styling
- **[Pest](https://pestphp.com)** — Elegant PHP testing

---

<p align="center">
  <sub>Built in Germany. Made for teams who take data privacy seriously.</sub><br/>
  <sub>
    <a href="https://clonio.dev">Website</a> ·
    <a href="https://clonio.dev/docs">Documentation</a> ·
    <a href="https://github.com/sponsors/clonio-dev">Sponsor</a> ·
    <a href="https://github.com/clonio-dev/clonio/issues">Issues</a>
  </sub>
</p>
