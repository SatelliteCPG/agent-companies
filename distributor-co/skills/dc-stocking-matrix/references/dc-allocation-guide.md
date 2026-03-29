# DC Allocation Guide

Reference document for managing product-to-DC allocation decisions at a national CPG distributor operating 55+ distribution centers.

## Allocation Philosophy

Not every product belongs in every DC. Allocation decisions balance three factors:

1. **Retailer demand**: Which retailers order this product, and which DCs serve them?
2. **Shipping efficiency**: Is the product close enough to the demand to ship cost-effectively?
3. **Velocity thresholds**: Does the product move fast enough at a DC to justify stocking it there?

## DC Network Regions

### UNFI Reference Network (55 DCs)

| Region | DCs | Key Markets | Temperature Capabilities |
|--------|-----|-------------|-------------------------|
| Northeast | 8 | NYC, Boston, Philadelphia | Ambient, Refrigerated, Frozen |
| Southeast | 7 | Atlanta, Miami, Charlotte | Ambient, Refrigerated, Frozen |
| Midwest | 9 | Chicago, Minneapolis, Detroit | Ambient, Refrigerated, Frozen |
| Southwest | 6 | Dallas, Houston, Phoenix | Ambient, Refrigerated, Frozen |
| Mountain | 5 | Denver, Salt Lake City | Ambient, Refrigerated, Frozen |
| Pacific Northwest | 4 | Seattle, Portland | Ambient, Refrigerated, Frozen |
| California | 6 | LA, SF, Sacramento | Ambient, Refrigerated, Frozen |
| Mid-Atlantic | 5 | DC, Baltimore, Richmond | Ambient, Refrigerated, Frozen |
| Great Lakes | 5 | Cleveland, Columbus, Indianapolis | Ambient, Refrigerated, Frozen |

## Allocation Tiers

### Tier 1: National (All DCs)
- **Criteria**: Established product with proven national demand, ordered by retailers in all regions
- **Typical products**: Top 500 SKUs by volume, category leaders
- **Review cadence**: Annual

### Tier 2: Regional (15-35 DCs)
- **Criteria**: Product with strong regional demand but not national
- **Typical products**: Regional brands, items with geographic demand patterns (e.g., certain ethnic foods)
- **Review cadence**: Semi-annual

### Tier 3: Select (5-15 DCs)
- **Criteria**: New items in ramp phase, niche products with concentrated demand
- **Typical products**: New brand launches, specialty items, seasonal products
- **Review cadence**: Quarterly

### Tier 4: Single DC
- **Criteria**: Very low volume items or test products
- **Typical products**: Ultra-niche, local brands with limited retail footprint
- **Review cadence**: Quarterly (with discontinuation risk)

## Velocity Thresholds

Minimum velocity thresholds determine whether a product should remain stocked at a DC:

| Temperature Class | Minimum Turns/Year | Minimum Cases/Month |
|-------------------|-------------------|---------------------|
| Ambient (shelf-stable) | 4 | 10 |
| Refrigerated | 6 | 15 |
| Frozen | 6 | 15 |

Products below minimum velocity for 3 consecutive months are candidates for:
1. Redistribution to fewer, higher-volume DCs
2. Reclassification as special-order (available but not stocked)
3. Discontinuation at that DC

## New Product Allocation Process

### Step 1: Demand Assessment
- Which retailers have expressed interest or committed to listing?
- Which DCs serve those retailers?
- Are there broker/brand commitments for volume?

### Step 2: Initial Allocation
- Start with DCs that serve committed retailers
- Typically 5-10 DCs for a new brand, expanding based on demand
- Include at least one DC per region where demand exists

### Step 3: Initial Stocking
- Calculate initial stocking quantity: 4-6 weeks of projected demand per DC
- Include additional safety stock for new items (demand uncertainty is higher)
- Coordinate delivery timing — all allocated DCs should be stocked within the same week

### Step 4: 90-Day Review
- Review actual velocity vs. projection at each DC
- Expand allocation to additional DCs if velocity exceeds threshold
- Reduce allocation if velocity is significantly below projection
- Transition to standard velocity-based allocation management

## Seasonal Allocation

Seasonal products require special allocation management:

### Pre-Season (8-12 weeks before)
- Activate seasonal codes at allocated DCs
- Build initial inventory based on prior year demand + growth factor
- Communicate availability to retail accounts

### In-Season
- Monitor velocity weekly — adjust allocation if demand differs from plan
- Replenish aggressively for high-velocity seasonal items
- Track sell-through rate vs. plan

### Post-Season (4-6 weeks after peak)
- Begin markdown process for remaining inventory
- Deactivate codes at DCs where inventory is cleared
- Document lessons learned for next season planning

## DC Allocation and Fill Rate Relationship

Poor allocation directly causes fill rate issues:

| Allocation Problem | Fill Rate Impact | Resolution |
|--------------------|-----------------|------------|
| Product not stocked at serving DC | 0% fill rate for affected retailers | Add allocation or route from alternate DC |
| Insufficient safety stock | Intermittent stock-outs during demand spikes | Increase safety stock or reorder point |
| Too many DCs for demand level | Fragmented inventory, slow turns, stock-outs | Consolidate to fewer DCs, serve distant retailers from hub |
| Supplier lead time longer than reorder cycle | Gaps between replenishment deliveries | Increase order quantities or safety stock |

## Data Sources

- **Satellite CRM**: DC locations (`search_distribution_centers`), distributor codes (`get_distributor_codes`), product catalog (`search_products`). Provides the structural data for allocation planning.
- **WMS**: Actual inventory levels, pick rates, receiving data. Not available through MCP tools yet.
- **ERP**: Purchase orders, sales history, financial data. Not available through MCP tools yet.
- **Retailer POS**: Sell-through data at the store level. Available through SPINS/IRI for some retailers, not through MCP tools.

The gap between CRM structural data and operational WMS/ERP data means allocation reviews require manual data compilation. Future MCP tool development for inventory and velocity data would significantly automate this process.
