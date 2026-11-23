# Sheba Investments — Technical Architecture

## Objective
Build a secure corporate website first, with foundations for separate internal and external platform areas later. Do not build a trading platform before permissions and operating processes are ready. Avoid coupling the public website to future trading functionality.

## Recommended stack

| Layer | Technology | Responsibility |
|---|---|---|
| Framework | Next.js App Router, current stable release | Routing, rendering, server endpoints |
| Language | TypeScript, strict mode | Type safety |
| UI | React | Components |
| Styling | Tailwind CSS | Responsive design system |
| Components | shadcn/ui and Radix UI | Accessible reusable components |
| Motion | Framer Motion / current Motion for React package | Restrained transitions |
| Database | Supabase PostgreSQL | Website data and future bounded domains |
| Authentication | Supabase Auth | Protected admin authentication |
| Validation | Zod | Runtime form/API validation |
| Forms | React Hook Form where useful | Complex form state |
| Hosting | Vercel | Hosting and deployments |
| Email | Transactional provider selected during implementation | Acknowledgements and notifications |
| Analytics | GA4 or approved privacy-aware alternative | Aggregate usage/conversion |
| Testing | Vitest, React Testing Library, Playwright | Unit, component and end-to-end tests |
| Quality | ESLint and Prettier | Static checks and formatting |

Pin compatible dependency versions and consult current official documentation.

## Initial system context
Public: visitor browser -> Next.js website -> server-side enquiry endpoint -> validation/anti-spam -> Supabase.

Optional email: stored enquiry -> server-side email provider -> acknowledgement/internal notification.

Admin: administrator -> Supabase Auth -> protected Next.js admin routes -> server-side data access -> Supabase PostgreSQL.

Analytics: consent-aware browser events -> analytics provider.

The browser must never receive service-role keys, email provider secrets or privileged database credentials.

## Suggested application structure

~~~text
src/
  app/
    (public)/
      page.tsx
      about/
      proprietary-trading/
      trader-network/
      research/
      partnerships/
      investments/
      insights/
      contact/
      privacy/
      terms/
      risk-disclosure/
    (admin)/
      admin/
        login/
        enquiries/
        content/
    api/
      enquiries/route.ts
      health/route.ts
  components/
    layout/
    navigation/
    sections/
    forms/
    ui/
  features/
    enquiries/schemas/
    enquiries/services/
    enquiries/types/
    content/
    auth/
  lib/
    supabase/
    email/
    analytics/
    security/
    env/
  styles/
  types/
docs/
supabase/migrations/
supabase/seed/
tests/
~~~

Adapt to framework conventions. Keep server-only modules separate from browser-safe modules. Never import privileged server modules into client components.

## Rendering and data access
- Prefer server components for static content.
- Use client components only when interaction requires them.
- Pre-render or revalidate marketing content where practical.
- Submit forms to server route handlers/actions with server-side validation.
- Do not let the browser write directly to privileged tables.
- Use server-only Supabase clients for privileged operations.
- Use public clients only for genuinely public, RLS-protected reads.
- Keep secrets in environment variables and validate configuration.

## Backend workflows
Enquiry: submit over HTTPS; validate with Zod; check request size, origin, rate limits and anti-spam; normalise fields; store enquiry and consent; return generic success; attempt email notification; log failures without full personal content or secrets. Email failure must not erase a stored enquiry.

Admin: no public registration; owner provisions accounts; server checks identity and role for every privileged action; MFA where supported; secure session/cookie settings.

## Supabase rules
Use separate development, staging and production environments/projects where practical. Store schema changes as versioned SQL migrations. Enable Row Level Security on exposed tables. Use least privilege. Keep service-role credentials server-only and never in public environment variables. Avoid broad public read policies. Test anonymous, authenticated non-admin and admin access. Keep production data out of fixtures.

## Future bounded contexts
These are future areas, not first-release requirements.

- **Trading Operations:** provider/programme register, agreements/rules, trader engagements, account assignments/permissions, risk limits, trade journal, performance, payout reconciliation, incidents and audit reporting.
- **Trader Network:** independent profiles, consent/eligibility, approved research access, entitlements, notifications, broker referral attribution, support and complaints.
- **Research & Signals:** research authoring, signal versions, review/approval, distribution eligibility, outcomes, methodology and publication audit.
- **Partnerships:** provider due diligence, agreements, disclosures, referral attribution, commission reconciliation and conflicts.
- **Capital & Investments:** mandates, holdings, transactions, valuation, exposure reporting and governance approvals.

Each domain needs separate requirements and security review.

## Integration policy
No broker, prop-firm, exchange, wallet, card, payment, identity-verification or trading API integration is authorised by this document.

Before integration, verify provider suitability, corporate onboarding, current technical documentation, contracts, permissions and legal requirements. Document data exchanged, retention, failure modes and reconciliation. Obtain owner approval and test sandbox/failure scenarios.

Never store brokerage passwords, seed phrases or private keys. Do not request credentials as a workaround for a missing API.

## Environments and observability
Use local, preview/staging and production. Production requires protected deployment access, separate secrets/database, HTTPS, backups and tested recovery, redacted error monitoring, dependency updates, rollback procedure and documented domain/DNS/email configuration.

Use Vercel previews for review. Production releases must be traceable to reviewed commits.

Capture application errors, request IDs, enquiry success/failure, email outcomes, admin security events and deployment versions. Never log passwords, tokens, private keys, full enquiry messages or sensitive account data.

For significant decisions, add an ADR under docs/adr with context, decision, alternatives, consequences, date and owner.
