# Sheba Investments — Delivery Roadmap and Acceptance Criteria

## Strategy
Deliver in controlled phases. The first phase establishes public identity and lead generation; it does not launch every planned business line. A phase is complete only when acceptance criteria pass and the product owner approves release.

## Phase 0 — Engineering foundation
Deliver: confirm framework/package versions; create Next.js App Router app with strict TypeScript; configure Tailwind and accessible primitives; lint/format/type checks; environment validation and example env file; local/preview/production conventions; basic CI; documentation links.

Accept when clean install, development and production builds, lint and type checks pass; no secrets are committed or exposed; README explains setup, scripts, environment and deployment.

## Phase 1 — Corporate website
Deliver: responsive public layout, navigation/footer, homepage and approved pages, audience-specific CTAs, approved copy, reviewed legal content, SEO metadata, sitemap and accessible forms.

Accept when routes and metadata work; mobile/tablet/desktop are reviewed; keyboard navigation works; contrast/focus checked; claims have owner approval/evidence; no page implies a planned service is live.

## Phase 2 — Enquiry system and admin
Deliver: Supabase project and versioned migrations, enquiry table/RLS, server endpoints and Zod schemas, anti-spam/rate limiting, email integration if approved, admin authentication and protected enquiry views.

Accept when enquiries persist; invalid/oversized/abusive submissions are rejected; public users cannot read enquiries; admin access is server-checked; email failure does not lose stored enquiry; consent/version recorded; personal form data is not sent to analytics.

## Phase 3 — Content and business development
Potential deliverables: approved insights CMS, draft/review/published workflow, SEO/analytics improvements, lead-source attribution, secure exports and newsletter only if consent/unsubscribe/retention workflows exist.

Accept when drafts are private, publishing is role-based, market content has a review gate, unsubscribe works if applicable and analytics respects consent.

## Phase 4 — Internal Trading Operations (separate project)
Requires its own specification and legal/provider approval. Potential scope: provider register, agreements/rules, trader engagements, account allocation/permissions, risk policy, trade journal, performance, reward/payout reconciliation, incidents and audit reports.

Accept only with provider permission for team model, role separation, tested risk limits/escalation, reconciliation controls, audit history and no unsupported credential sharing.

## Phase 5 — Trader Network (separate project)
Requires legal classification and approval. Potential scope: member authentication/profiles, consent/eligibility, approved research access, notifications, support/complaints and referral attribution under approved agreements.

Accept only with member data isolation, clear terms/risk disclosures, approved content distribution, partner disclosures and secure account lifecycle.

## Phase 6 — Research, signals and investment systems
Separate specifications required for research review/publication, signal versioning/outcomes, performance methodology, investment mandates/holdings/approvals and financial/broker integrations.

Do not activate a phase by merely adding a navigation link. Legal, operational, security and reporting controls must exist.

## Definition of done
Requirements and users documented; owner approves behaviour/copy; permissions and failure cases implemented; validation and error states exist; automated tests cover critical paths; responsive/accessibility checks pass; security/privacy reviewed; logs avoid sensitive data; docs updated; preview reviewed before production; rollback known.

## Developer handover
Provide setup/run instructions, architecture/routes, environment variable list without secrets, schema/migration history, RLS policy summary and test evidence, admin provisioning, deployment/rollback, test results/limitations, third-party services and outstanding decisions/risks.
