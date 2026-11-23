# Sheba Investments — Data Model and Security Requirements

## Purpose
Define data boundaries and minimum security expectations. This is a conceptual model; create migrations only for approved functionality being implemented.

## Initial website data

**Enquiries:** UUID; enquiry type (general, trader interest, trading candidate, broker partnership, strategic partnership); name; email; optional phone/country/organisation/role/website/experience; optional length-limited message; source path; status (new, in review, contacted, qualified, closed, spam); privacy notice version and acknowledgement timestamp; separate marketing consent; created/updated timestamps.

Collect only fields needed for the selected enquiry type.

**Consent records:** if detailed evidence is needed, use append-only records with subject reference, purpose, notice version, consent status, capture timestamp, withdrawal timestamp and capture source. Privacy notice acknowledgement is not blanket marketing consent.

**Newsletter subscriptions:** create only if a newsletter launches. Store email, status, consent version, subscribed/unsubscribed timestamps and a hash of any confirmation token. Never store a raw token.

**Admin profiles:** if needed, store authentication user UUID, controlled role and timestamps. A profile row alone does not prove authorisation; validate roles server-side and through database policies.

**Articles:** if a database CMS is selected, store title, slug, excerpt, body, status, author/reviewer IDs, timestamps, SEO metadata and review metadata.

## Future data domains
Do not create speculative tables in the first release. When approved, design separate schemas for:
- Proprietary trading: providers, programmes, agreements, internal traders, engagements, accounts, assignments, permissions, risk policies/events, trade journal, reward statements and payout reconciliation.
- Trader network: members, profiles, service entitlements, broker referrals, preferences, support cases and complaints.
- Research/signals: research items, publications, versions, reviews, events, outcomes, distribution and performance methodologies.
- Partnerships: providers, due diligence, agreements, disclosures, referrals, commission statements/reconciliation and conflicts.
- Investments: mandates, positions, transactions, valuations and approvals.

## Data ownership and isolation
Internal trading records are private company data. A network member may access only their own profile, preferences, entitlements and permitted service records. One member must never see another member's data. Staff access is role-based. Partners do not receive direct database access. Third parties receive only data required by an approved integration.

If Sheba later serves multiple organisations, design tenant isolation explicitly before enabling it.

## Suggested future roles

| Role | Scope |
|---|---|
| owner | Company administration and role provisioning |
| admin | Approved operational administration |
| enquiry manager | Enquiry access and status |
| content editor | Draft and edit content |
| content reviewer | Review and approve assigned content |
| trading manager | Internal proprietary trading |
| risk manager | Risk oversight and incidents |
| trader | Assigned internal trading records only |
| network member | Own permitted external records |
| compliance reviewer | Assigned compliance/audit records |

Implement only roles needed by the approved phase.

## Authentication and authorisation
No public admin registration. Enforce MFA for privileged users where supported. Verify identity and role server-side for every protected action. Protect API routes as well as pages. Apply secure sessions, cookies and CSRF/origin protections. Use RLS as a second layer, not a replacement for server-side checks. Test anonymous, ordinary user, editor, enquiry manager and owner access. Revoke access when staff/contractors leave.

## Application security
Require HTTPS, server validation, output encoding, parameterised database operations, rate limiting, request size limits, secure secrets, dependency scanning, security headers, safe upload controls if enabled, tested backups and incident response. Do not put sensitive data in URLs, analytics or client logs.

## Environment variables
Example names only:

~~~env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
EMAIL_PROVIDER_API_KEY=
EMAIL_FROM_ADDRESS=
EMAIL_NOTIFICATION_TO=
NEXT_PUBLIC_SITE_URL=
ANALYTICS_MEASUREMENT_ID=
~~~

Only intentionally public values may use the public prefix. Service-role and email credentials remain server-only. Provide an example file with empty placeholders. Never commit real credentials.

## Privacy and auditability
Publish an accurate privacy notice reviewed for applicable jurisdictions. Collect minimum data. Define retention for enquiries, unsuccessful applications, newsletters, logs and backups. Provide controlled access/correction/deletion/objection workflows where applicable. Restrict and log exports. Avoid collecting identity documents, financial account information or special-category personal data in initial forms.

For privileged actions, retain actor ID, action, record reference, timestamp, result, request ID and safe before/after metadata. Never log passwords, tokens, private keys or sensitive full content. Normal application roles must not alter audit history.

## Security acceptance tests
Verify anonymous visitors cannot read enquiries; ordinary users cannot access admin; enquiry managers cannot change owner permissions; editors cannot bypass reviewer approval; changing record IDs cannot expose another user's data; secrets are absent from client bundles; rate limiting works; invalid/oversized payloads fail; logs/analytics contain no full form content; backup restoration is tested.
