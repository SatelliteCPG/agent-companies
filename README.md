# Agent Companies

[Agent Companies v1](https://agentcompanies.io) packages for the CPG industry, built for [Paperclip](https://paperclip.ing).

## Companies

| Company | Description | Import |
|---------|-------------|--------|
| [satellite-cpg-co](./satellite-cpg-co/) | Agent Native B2B SaaS platform for CPG sales teams | `npx paperclipai company import satellite-cpg-co/` |

## Planned

- **brand-co** — Company package for CPG brand teams (marketing, product launches, retail partnerships)
- **retailer-co** — Company package for retailers managing CPG vendor relationships
- **distributor-co** — Company package for distributors managing logistics and fulfillment

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
