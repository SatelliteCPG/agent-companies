# Agent Companies

[Agent Companies v1](https://agentcompanies.io) packages for the CPG industry, built for [Paperclip](https://paperclip.ing).

## Companies

| Company | Description | Import |
|---------|-------------|--------|
| [satellite-cpg-co](./satellite-cpg-co/) | Agent Native B2B SaaS platform for CPG sales teams | `npx paperclipai company import satellite-cpg-co/` |
| [brand-co](./brand-co/) | CPG brand operations — sales, marketing, distribution, finance (14 agents, 5 skills) | `npx paperclipai company import brand-co/` |

## Planned

- **partner-co** — CPG brokers/partners (multi-brand representation, void closure, deduction recovery)
- **retailer-co** — Retailers (category management, vendor evaluation, planogram)
- **distributor-co** — Distributors (warehouse ops, supplier onboarding, DC allocation)

## Quick Start

```bash
# Import a company into your Paperclip instance
npx paperclipai company import ./satellite-cpg-co/

# Or import directly from GitHub
npx paperclipai company import https://github.com/SatelliteCPG/agent-companies/satellite-cpg-co
```

## Protocol

All packages follow the [Agent Companies v1](https://agentcompanies.io) specification and are compatible with the [Paperclip](https://paperclip.ing) runtime.

## License

MIT
