# SignalDesk — Technology Stack

> This document explains the **why** behind each technology choice. Implementation details are not disclosed.

---

## Stack Summary

| Layer | Technology | Version |
|---|---|---|
| Frontend Framework | React | 19 |
| Language | TypeScript | 5.9 |
| Styling | Tailwind CSS + shadcn/ui | 4 |
| API Contract | tRPC | 11 |
| Backend Runtime | Node.js + Express | 22 / 4 |
| Database | MySQL via TiDB | — |
| ORM | Drizzle | — |
| Auth | Magic Code OTP + Google OAuth | — |
| Payments | Stripe | — |
| Email | Resend | — |
| File Storage | S3-compatible object storage | — |
| Maps | Google Maps JavaScript API | — |
| Charts | Recharts + D3 | — |
| Animations | Framer Motion | — |
| Testing | Vitest | — |
| Deployment | Manus Cloud | — |

---

## Rationale by Layer

### React 19

React 19 was chosen for its mature ecosystem, concurrent rendering capabilities, and the availability of shadcn/ui — a component library that provides production-quality accessible primitives without the overhead of a full design system. The component model maps naturally to SignalDesk's data-heavy dashboard interfaces.

### TypeScript 5.9

Type safety is non-negotiable for a platform where data integrity directly affects investment decisions. TypeScript catches contract mismatches between the frontend and backend at compile time, not at runtime. The strict mode configuration eliminates entire categories of null-reference and type coercion bugs.

### tRPC 11

tRPC was chosen over REST or GraphQL because it eliminates the API contract layer entirely. Procedures defined on the server are immediately available as fully typed hooks on the client — no code generation, no schema files, no manual type synchronization. For a product built by a small team, this is a significant velocity multiplier.

### Drizzle ORM

Drizzle was chosen over Prisma for its zero-overhead query model and TypeScript-first schema definition. It generates SQL that is predictable and inspectable, which matters for a platform that runs complex scoring queries across large property datasets. The schema-first migration workflow (`drizzle-kit generate + migrate`) keeps the database and codebase in sync without magic.

### TiDB (MySQL-compatible)

TiDB provides MySQL wire compatibility with horizontal scalability built in. SignalDesk's data model — properties, signals, scores, users, subscriptions — is inherently relational. A MySQL-compatible database allows standard Drizzle queries while providing the scale characteristics needed as county coverage and user volume grow.

### Magic Code OTP Authentication

Passwordless authentication was chosen deliberately. Passwords create support overhead (resets, breaches, reuse), and real estate investors are not a demographic that tolerates friction. A 6-digit email code sent via Resend is faster to implement, faster for users, and eliminates the password storage liability entirely. Google OAuth is offered as a one-click alternative for users who prefer it.

### Stripe

Stripe is the only viable choice for a SaaS subscription platform that needs to be production-ready quickly. Its webhook system, subscription lifecycle management, and Checkout hosted pages handle the full billing complexity — upgrades, downgrades, cancellations, proration, and failed payment recovery — without custom code.

### Resend

Resend was chosen over SendGrid or Mailgun for its developer-first API, generous free tier, and clean React Email integration. For a platform whose primary email use case is transactional (magic codes, subscription confirmations), Resend's simplicity is an advantage over the configuration overhead of enterprise email platforms.

### Framer Motion

Real estate investors are visually sophisticated — they evaluate dashboards and tools by how polished they feel. Framer Motion provides the animation primitives needed to make the deal feed, score animations, and page transitions feel like a premium product rather than a generic SaaS template.

### Vitest

Vitest runs in the same Vite pipeline as the application code, making test execution fast and configuration minimal. The test suite covers authentication procedures, password hashing, and Stripe webhook verification — the three areas where a bug has direct financial or security consequences.

---

## What Was Deliberately Not Used

| Technology | Why Excluded |
|---|---|
| Next.js | tRPC + Vite provides the same SSR-optional architecture with less framework lock-in |
| Prisma | Drizzle's query model is more predictable for complex analytical queries |
| GraphQL | tRPC provides the same type safety with less infrastructure overhead |
| Firebase Auth | Vendor lock-in risk; magic code OTP is simpler and fully owned |
| Axios | tRPC's `fetch`-based transport is sufficient; Axios adds unnecessary weight |

---

<!-- Built by Ahmad · SignalDesk v1.0 · May 2026 -->
