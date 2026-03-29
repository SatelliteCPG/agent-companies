---
name: Distributor Co
description: Agent company for national CPG distributors. Run supply chain operations, supplier management, catalog integrity, and retail fulfillment with AI agents connected to Satellite's MCP tools.
slug: distributor-co
schema: agentcompanies/v1
version: 1.0.0
license: MIT
authors:
  - name: JD Fiscus
tags:
  - cpg
  - distributor
  - agent-native
  - supply-chain
  - operations
  - catalog
metadata:
  sources:
    - kind: github-dir
      repo: SatelliteCPG/agent-companies
      path: distributor-co
      commit: main
      url: https://github.com/SatelliteCPG/agent-companies/tree/main/distributor-co
---

# Distributor Co

Agent company for running the operations of a national CPG distributor like UNFI. A CPG distributor operates 55+ distribution centers, manages relationships with 10,000+ suppliers, maintains a catalog of millions of SKUs, and fulfills orders for thousands of retail customers daily. That means managing DC-level inventory allocation, onboarding new suppliers through a multi-stage compliance pipeline, maintaining product catalog integrity with GS1 validation, processing EDI transactions (850/810/856), tracking fill rates and OTIF metrics, managing cost tiers and promotional pricing, and ensuring reliable order fulfillment to every retail account. This agent company covers supply chain, supplier relations, catalog management, sales, and cross-functional analytics — with 15 agents organized into the same functional teams a real distributor runs.

## Operating Principles

### Supply Chain Excellence

Every product must be in the right DC at the right time. Inventory allocation decisions are driven by retailer demand signals, shipping zone efficiency, and minimum velocity thresholds. Fill rates above 97% are the baseline — below that, retailers complain and suppliers get penalized. Reorder points, safety stock levels, and slow-mover discontinuation are managed proactively, not reactively.

### Supplier Portfolio Management

Suppliers are evaluated, onboarded, and managed through a structured lifecycle. New supplier applications go through a stage-gate process — application, evaluation, compliance, setup, go-live. Active suppliers are scored monthly on fill rate, OTIF, shelf-life compliance, and quality. Underperforming suppliers get improvement plans; top performers get preferred status and expanded DC coverage.

### Catalog Integrity

The product catalog is the single source of truth. Every item has complete GS1-compliant data — UPC/GTIN, case pack, dimensions, weight, certifications, and attributes. Price changes, new item setups, and discontinuations flow through a controlled process with validation at every step. Bad data causes pick errors, invoice disputes, and retailer chargebacks.

### Retail Fulfillment

Retailers depend on consistent, on-time order fulfillment. Purchase orders (EDI 850) are received, picked, packed, and shipped with advance ship notices (EDI 856) and invoices (EDI 810). Substitutions and out-of-stocks are tracked at the order line level. Fill rate and delivery performance are reported weekly by account.

### Data-Driven Operations

Decisions at distributor scale require data, not intuition. Inventory turns, fill rates, supplier scorecards, DC utilization, and order accuracy are tracked continuously. Cross-functional reporting surfaces issues before they become crises. Every KPI has an owner, a target, and a review cadence.
