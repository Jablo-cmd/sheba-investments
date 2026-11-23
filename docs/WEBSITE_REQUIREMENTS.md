# Sheba Investments — Website Product Requirements

## Intention
The website is Sheba's public corporate presence and primary business-development channel. It must establish credibility, explain the business honestly, distinguish business lines, generate qualified enquiries and provide a foundation for a future secure platform.

The first release is a **corporate website and lead-generation system**, not a trading terminal, broker, investment portal or signal execution platform.

## Audience calls to action
- Independent traders: **Register Your Interest**
- Professional trading candidates: **Trading Careers / Submit Your Profile**
- Brokers: **Explore Partnership Opportunities**
- Strategic partners: **Discuss a Business Opportunity**
- General visitors: **Contact Sheba**

Each CTA must lead to a distinct enquiry path.

## Sitemap

| Route | Purpose |
|---|---|
| / | Positioning, company overview, business lines, principles and audience pathways |
| /about | Vision, approach, values and verified company information |
| /proprietary-trading | Internal trading model and risk-led approach |
| /trader-network | Future independent network and interest registration |
| /research | Research capability; approved content only |
| /partnerships | Broker partnership criteria and enquiries |
| /investments | Long-term investment ambition, labelled future-facing |
| /insights | Approved articles and company updates |
| /contact | Contact details and general enquiry |

Legal routes: /risk-disclosure, /privacy, /terms, /cookies, plus service-specific terms when a service is approved. A careers page may be added only when actively recruiting.

## Homepage sequence
1. Hero with clear positioning, primary CTA and secondary audience route.
2. Honest company introduction.
3. Business-line overview: proprietary trading, trader network, research/signals, broker partnerships and future investments.
4. Operating principles: discipline, risk management, transparency and accountability.
5. Audience pathways.
6. Measured future direction.
7. Approved insights only.
8. Contact CTAs.
9. Footer with verified company details, legal links and risk disclosure.

Label each business line current, in development or future-facing based on owner confirmation. Never use fake tickers, fake counters, fabricated testimonials, invented partner logos or simulated dashboards presented as real.

## Enquiry journeys
**Trader interest:** name, email, country, optional phone, optional experience category/message, privacy acknowledgement and separate optional marketing consent.

**Professional candidate:** name, contact details, country/time zone, experience, markets traded and optional CV/profile link only if secure upload and retention are designed.

**Broker partnership:** contact name, business email, company, jurisdiction, role, provider website, partnership interest and message.

**Strategic partnership:** contact details, organisation if relevant, opportunity type and message.

**General contact:** name, email, category and message.

Do not collect brokerage passwords, API secrets, seed phrases, identity documents, account balances or deposits through public forms. An interest submission is not automatic acceptance or access to a trading service.

## Enquiry handling
Every enquiry must be server-validated, stored with timestamp and source route, associated with consent state and privacy notice version, visible only to authorised admins and protected against duplicate/automated submissions.

Suggested statuses: new, in review, contacted, qualified, closed, spam.

Email acknowledgement is optional. Email failure must not erase a stored enquiry. Never expose enquiry records through public APIs or client-side database queries.

## Content and administration
A repository-managed content approach is acceptable initially. If a database CMS is selected, support draft/review/published states, author/reviewer attribution, timestamps, unique slugs, SEO metadata and approval controls for market-related content.

Admin: secure sign-in, no public registration, enquiry list/filter/detail, status updates, optional internal notes, logged authorised exports and approved article management.

## Accessibility, SEO and analytics
Use mobile-first layouts, keyboard-operable navigation, visible focus, semantic headings, labelled forms, useful validation errors, sufficient contrast and reduced-motion support. Target WCAG 2.2 AA.

SEO: unique titles/descriptions, canonical URLs, Open Graph metadata, sitemap, robots rules, accurate structured data, descriptive URLs, internal links and optimised assets.

Analytics must be privacy-aware. Obtain consent where required before non-essential tracking. Track aggregate CTA clicks and successful enquiries. Never send form contents, email addresses or sensitive financial information to analytics.

## First-release exclusions
No trade execution, copy trading, brokerage account linking, credential collection, client deposits/withdrawals, payment processing, wallet custody, crypto cards, performance dashboards, paid signal subscriptions, personalised recommendations, discretionary management, broker APIs, KYC document collection or public investment marketplace.

Any addition requires separate scope, risk assessment, legal review and product-owner approval.
