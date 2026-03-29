# Agent Companies

[Agent Companies v1](https://agentcompanies.io) packages for the CPG industry, built for [Paperclip](https://paperclip.ing).

## Companies

| Company | Description | Import |
|---------|-------------|--------|
| [satellite-cpg-co](./satellite-cpg-co/) | Agent Native B2B SaaS platform for CPG sales teams | `npx paperclipai company import satellite-cpg-co/` |
| [brand-co](./brand-co/) | CPG brand operations — sales, marketing, distribution, finance (14 agents, 5 skills) | `npx paperclipai company import brand-co/` |
| [partner-co](./partner-co/) | CPG broker/partner — multi-brand representation, void closure, deduction recovery (12 agents, 5 skills) | `npx paperclipai company import partner-co/` |
| [retailer-co](./retailer-co/) | CPG retailer — category management, vendor evaluation, promotions (12 agents, 4 skills) | `npx paperclipai company import retailer-co/` |
| [distributor-co](./distributor-co/) | CPG distributor — supply chain, supplier onboarding, DC allocation (15 agents, 4 skills) | `npx paperclipai company import distributor-co/` |

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
