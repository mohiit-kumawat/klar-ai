# Contributing to Klar

Thank you for your interest in contributing to Klar. Klar is an AI tutor focused on clear explanations, practical learning, and a simple student experience. This guide explains how to set up the project, make changes, and submit high-quality contributions.

## Before You Start

Please check the existing issues and pull requests before opening a new one. For larger changes, open an issue first so the approach can be discussed before implementation begins.

When reporting a bug, include:

- A clear description of the expected and actual behavior
- Steps to reproduce the issue
- The affected route, page, or component
- Browser, operating system, and relevant environment details
- Logs or screenshots when they help explain the problem

Do not include API keys, database URLs, tokens, passwords, or other secrets in issues, pull requests, screenshots, or logs.

## Development Setup

### Requirements

- Node.js 20 or newer
- pnpm
- PostgreSQL or a compatible Neon PostgreSQL database
- Upstash Redis credentials for rate limiting
- At least one supported AI provider key for chat features

### Installation

```bash
pnpm install
```

Copy the example environment file and fill in the required values:

```bash
cp .env.local.example .env.local
```

On Windows PowerShell, use:

```powershell
Copy-Item .env.local.example .env.local
```

Required environment variables include:

```env
DATABASE_URL=your_postgres_connection_string
JWT_SECRET=your_long_random_secret
GROQ_API_KEY=your_groq_api_key
MISTRAL_API_KEY=your_mistral_api_key
RESEND_API_KEY=your_resend_api_key
UPSTASH_REDIS_REST_URL=your_upstash_rest_url
UPSTASH_REDIS_REST_TOKEN=your_upstash_rest_token
APP_URL=your_localhost_url
```

For local email testing, use the Resend test sender and a verified test recipient as permitted by your Resend account. Do not commit `.env.local`.

### Database

The Drizzle schema is defined in `src/db/schema.ts`. To apply the current schema to the configured database:

To generate migration files:

```bash
pnpm exec drizzle-kit generate

```bash
pnpm exec drizzle-kit push
```

```

Review generated migrations before applying them to a shared or production database.

### Run the Application

```bash
pnpm dev
```

The application is available at `http://localhost:3000`.

## Project Conventions

- Keep changes focused on the issue being addressed.
- Follow the existing TypeScript, React, Next.js, and Tailwind patterns.
- Prefer small, readable functions and existing utilities over duplicate logic.
- Keep secrets and server-only values out of client components.
- Validate untrusted input at API boundaries.
- Preserve authentication, authorization, ownership checks, and rate limits when changing API routes.
- Use accessible labels and keyboard-friendly interactions for UI changes.
- Avoid unrelated formatting changes or broad refactors in feature pull requests.
- Add or update documentation when behavior, setup, or configuration changes.

## Branches and Commits

Create a focused branch from the current default branch:

```bash
git switch main
git pull
git switch -c feature/short-description
```

Use a clear, imperative commit subject. Common prefixes are recommended:

- `feat:` for a new feature
- `fix:` for a bug fix
- `docs:` for documentation
- `refactor:` for behavior-preserving restructuring
- `chore:` for maintenance or tooling
- `security:` for security-related changes

Examples:

```text
feat: add conversation export
fix: prevent duplicate verification tokens
docs: clarify local email setup
```

Keep commits focused. Avoid mixing formatting-only changes, dependency upgrades, or unrelated cleanup with a functional change.

## Validation Checklist

Run the checks relevant to your change before opening a pull request:

```bash
pnpm lint
pnpm build
```

For database changes, also verify the Drizzle schema or migration against a development database. For authentication, email, chat, or rate-limit changes, test both successful and failure paths.

At minimum, confirm that:

- The changed page or API route works locally
- Invalid input is handled safely
- Unauthenticated and unauthorized requests are rejected where appropriate
- Existing user data and conversations remain accessible
- No secrets appear in source files, logs, or the diff

## Pull Requests

A good pull request should:

- Explain what changed and why
- Link the related issue when one exists
- Describe setup or migration steps
- Include validation commands and their results
- Include screenshots or a short recording for meaningful UI changes
- Call out known limitations or follow-up work

Keep pull requests reviewable. Smaller pull requests are easier to test, review, and safely deploy.

## Security Issues

Do not report security vulnerabilities in a public issue. Contact the project maintainer privately with:

- A concise description of the issue
- Reproduction steps or proof of concept
- Potential impact
- Any suggested mitigation

Immediately rotate any credential that has been exposed, even if it was exposed only in a local file, terminal output, screenshot, or commit.

## Code of Conduct

Contributors are expected to communicate respectfully and constructively. Keep discussions focused on the work, welcome different perspectives, and avoid harassment, discrimination, personal attacks, or disruptive behavior.

## License

By contributing to Klar, you agree that your contributions will be provided under the project's MIT License.
