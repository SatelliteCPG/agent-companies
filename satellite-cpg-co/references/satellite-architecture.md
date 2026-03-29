# Satellite Architecture

Technical architecture reference for the Satellite CPG platform.

## Backend — NestJS 8.x

- **Framework:** NestJS 8.x with TypeScript
- **Modules:** 70+ domain modules (CRM, Products, Orders, Analytics, Communications, etc.)
- **ORM:** Prisma with PostgreSQL
- **Auth:** JWT + OAuth 2.0 global guard
- **Multi-tenancy:** `orgId` enforced at guard level on every request
- **API style:** REST with OpenAPI/Swagger documentation
- **Testing:** Jest unit + integration tests

### Key Backend Patterns

- One module per domain (e.g., `src/crm/`, `src/products/`, `src/communications/`)
- Service-controller-module triad per domain
- Global `AuthGuard` extracts and validates `orgId` from JWT
- Prisma middleware enforces `orgId` filtering on all queries
- DTOs validated with `class-validator` decorators

## Frontend — Vue 3

- **Framework:** Vue 3 with Composition API
- **Build:** Vite
- **State:** Pinia stores
- **UI Library:** Ant Design Vue
- **Routing:** Vue Router with role-based guards

### Key Frontend Patterns

- Feature-based directory structure
- Composables for shared logic (`useAuth`, `useOrg`, `useCRM`)
- Ant Design Vue components with Satellite design tokens
- TypeScript strict mode

## Mobile — Expo

- **Framework:** Expo with React Native 0.81
- **Styling:** NativeWind (Tailwind for React Native)
- **Navigation:** Expo Router
- **State:** Shared API client with web frontend

## Zapier CLI

- **Auth:** OAuth 2.0 + PKCE flow
- **Triggers:** New contact, new order, product update
- **Actions:** Create contact, update product, send communication
- **Searches:** Find contact, find product, find order

## Sally AI

- **Tools:** 35 atomic tools across 5 categories
- **Categories:**
  - CRM (21 tools): contacts, companies, tags, segments, activities
  - Products (7 tools): catalog, variants, pricing, images
  - Communications (3 tools): email, SMS, notifications
  - Analytics (2 tools): dashboards, reports
  - Content (2 tools): blog posts, landing pages
- **Architecture:** Agent-native design with parity, granularity, composability
- **Integration:** NestJS service layer shared with REST API

## Just Scorecard

- **Pipeline:** `.skill.json` self-improving data pipeline
- **Pattern:** AI maps once, deterministic code runs forever
- **Tiers:** Skill files → Client context → Mapping profiles
- **Current skills:**
  - `monthly_financials` — P&L statement processing
  - `spins_retailer_ranking` — SPINS retail data ingestion

## ETL Integrations

| Source | Method | Data |
|---|---|---|
| Shopify | Webhooks + polling | Orders, products, inventory |
| Ixone | API sync | Product data, digital assets |
| Worldsync | GDSN messages | Product attributes, compliance |

## Infrastructure

- **Database:** PostgreSQL (multi-tenant, `orgId` partitioned)
- **Auth:** JWT tokens with OAuth 2.0 provider
- **Deployment:** Containerized (Docker)
- **CI/CD:** GitHub Actions
