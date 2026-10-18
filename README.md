# FluentXVerse Tutor

The tutor-facing web application for FluentXVerse. It supports the journey from applying and completing screening to managing availability, teaching lessons, and reviewing lesson activity.

Production entry point: https://tutor.fluentxverse.com

## Responsibilities

- Tutor registration, account sessions, profile management, and application progress.
- Written and speaking assessment workflows, profile review, and interview participation.
- Availability, booked lessons, classroom entry, attendance, lesson notes, and student feedback.
- Browser audio/video lessons with Cloudflare RealtimeKit and server-controlled recording notices.
- Teaching metrics, notifications, inbox, and operational account settings.

## Architecture

SolidJS, TypeScript, Vite, Solid Router, and Cloudflare RealtimeKit. Cloudflare Workers serves the frontend; the [application server](https://github.com/fluentxverse/fluentxverse-server) authorizes business operations. Tutor wallets are server-managed through GMR Engine and GMR Vault rather than created from browser-held private keys.

Application source is in `fluentxverse-tutor-solid-prototype/`. Required shared source is included in `shared/`.

## Local Development

Use Node.js 22+, npm, and Bun. From the repository root:

```bash
npm run setup
cp fluentxverse-tutor-solid-prototype/.env.example fluentxverse-tutor-solid-prototype/.env.local
npm run dev
```

Open http://127.0.0.1:5177. Configure your own development API and socket URLs. A running server, configured identity/session services, and a tutor test account are required for live workflows.

```bash
npm test
npm run build
npm run preview
```

The root test command selects standalone helper tests. The app directory also retains cross-app parity, browser, and backend contract tests; run those from the monorepo with their documented fixtures. They are not all standalone tests.

## Deployment and Screening Boundaries

Build output is `fluentxverse-tutor-solid-prototype/dist/`. Review the app's Wrangler configuration before manual deployment; its routes refer to existing production services. Source checks in this repository do not deploy.

Screening source and UI are not equivalent to an independently reviewed certification system. A threshold/signature proof can establish conditions on approved issuer records; it does not establish that an AI assessment was accurate or a lesson genuinely occurred. ERC-8004, zkVerify, and Horizen integrations must be evaluated against their actual deployment and activation gates. Confidential payout settlement is a separate workstream, not an implied capability of this frontend.

## Repository Provenance

This repository is an app-focused export of [the FluentXVerse monorepo](https://github.com/fluentxverse/fluentxverse-monorepo). The monorepo remains the source of truth; submit cross-application changes there. Existing directory names are retained so shared imports remain valid. The historical student/tutor folder suffix does not indicate a Preact app: both active web clients use SolidJS.

Exported source commit: [`c9696e491149`](https://github.com/fluentxverse/fluentxverse-monorepo/tree/c9696e491149275bc01df3b8d05d29a15263257a). See [SOURCE.json](SOURCE.json) for the exact scope. Local uncommitted edits, environment files, runtime data, curriculum backups, and generated proving artifacts are not published. Original Git history is not copied.

Cross-app parity tests and full deployment orchestration remain in the monorepo. The checks in this repository do not establish production acceptance, security audit completion, or proof-system review. No production deployment is triggered by this export.

## Security and Licensing

Never commit API tokens, seed phrases, private keys, student records, recordings, or real assessment evidence. Use synthetic fixtures in tests. Report security issues privately to hello@fluentxverse.com rather than opening an issue containing sensitive data.

No root license file was present in the source revision. Public source availability, if enabled, is not itself a license grant. Contact FluentXVerse for licensing terms; third-party dependencies retain their own licenses.
