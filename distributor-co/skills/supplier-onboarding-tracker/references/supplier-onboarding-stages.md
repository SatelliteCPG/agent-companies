# Supplier Onboarding Stage Requirements

Detailed requirements for each stage of the 5-stage supplier onboarding pipeline at a national CPG distributor.

## Stage 1: Application

### Required Documentation
- **Company information**: Legal name, DBA, address, DUNS number, tax ID (EIN)
- **Product catalog**: Complete product list with descriptions, pack sizes, UPCs, and wholesale pricing
- **Insurance certificates**: General liability ($2M minimum), product liability ($2M minimum), workers compensation
- **Food safety certification**: SQF Level 2+, BRC Grade B+, FSSC 22000, or equivalent third-party audit
- **Organic certification**: If claiming organic — USDA Organic certificate with certifying agent
- **Non-GMO Project verification**: If claiming Non-GMO — current certificate

### Evaluation Criteria for Advancement
- All required documentation received and complete
- Initial category assessment shows potential fit (not duplicating existing assortment without differentiation)
- Supplier meets minimum requirements: at least 12 months in business, current insurance, valid food safety audit

### Typical Duration
- 1-2 weeks from submission to complete application

## Stage 2: Evaluation

### Assessment Areas

#### Category Fit (40% weight)
- Does the product fill an identified category gap?
- How does it compare to existing products in the assortment?
- Is there documented retailer demand? (buyer requests, market trend data)
- What category growth rate does this product segment show?

#### Margin Analysis (30% weight)
- Does the supplier's cost structure support distributor target margins?
- Cost comparison vs. comparable products in the catalog
- Volume projections based on category benchmarks
- Promotional allowance terms (MCB, TPR, off-invoice)

#### Operational Readiness (20% weight)
- Can the supplier meet minimum order quantities?
- Production capacity sufficient for national distribution?
- Lead time consistent with distributor requirements (typically 7-14 days)?
- Shelf life meets minimum requirements (>75% remaining at delivery)?

#### Brand Strength (10% weight)
- Consumer brand awareness and marketing investment
- Retailer relationships and existing distribution
- Social media presence and consumer engagement
- Awards, certifications, and media coverage

### Decision Outcomes
- **Proceed**: Advances to Compliance stage
- **Hold**: Promising but not ready — revisit in 90 days
- **Decline**: Does not meet criteria — documented rejection with reasons

### Typical Duration
- 2-4 weeks for evaluation and decision

## Stage 3: Compliance

### GS1/GDSN Requirements
- Supplier has a valid GS1 Company Prefix
- All products have properly formatted GTINs (GTIN-12 for retail units, GTIN-14 for case-level)
- Check digits are valid
- Product data is published to the GDSN (or supplier commits to publishing within 30 days)
- GTIN hierarchy is correct: each → inner pack → case → pallet

### EDI Requirements
- Supplier can send/receive EDI transactions:
  - 850 — Purchase Order (receive from distributor)
  - 855 — Purchase Order Acknowledgment (send to distributor)
  - 856 — Advance Ship Notice (send to distributor)
  - 810 — Invoice (send to distributor)
- If supplier cannot do EDI natively, they must use a certified EDI provider or the distributor's supplier portal
- Test transactions must complete successfully before advancing

### Insurance and Legal
- Current certificates of insurance on file
- Distributor named as additional insured
- Hold harmless agreement signed
- Vendor terms and conditions agreement signed

### Food Safety
- Current third-party food safety audit (SQF, BRC, FSSC 22000)
- Audit score meets minimum threshold (SQF Level 2 minimum, BRC Grade B minimum)
- HACCP plan in place for all products
- Allergen control program documented
- Recall procedure documented and tested within the past 12 months

### Labeling Compliance
- FDA/USDA labeling requirements met for the product category
- Nutrition facts panel current (if applicable)
- Allergen declarations present and accurate
- State-specific labeling requirements addressed (CA Prop 65, etc.)

### Typical Duration
- 2-6 weeks depending on supplier readiness
- GS1 registration (if needed) can add 4-6 weeks

## Stage 4: Setup

### Product Data Entry
- All products entered in the distributor's catalog system
- Required fields completed: UPC/GTIN, product description, brand, case pack configuration, inner pack count, unit dimensions (H x W x D), unit weight, case dimensions, case weight, pallet configuration (Ti x Hi), shelf life (days), temperature class (ambient, refrigerated, frozen), certifications (organic, non-GMO, kosher, etc.)
- Product images uploaded (front, back, nutrition panel)

### Pricing Configuration
- Base cost per unit and per case
- Bracket pricing by volume (if applicable)
- Freight terms: FOB origin or delivered
- Promotional allowance schedule: MCB rates, TPR terms, off-invoice discounts
- Payment terms: Net 30, Net 45, etc.

### DC Allocation
- Determine which DCs will stock each product
- Allocation based on: retailer demand in the DC's service area, shipping zone costs, minimum velocity thresholds
- Initial allocation may start with 5-10 DCs and expand based on demand
- Warehouse slotting: assign pick locations at each DC

### Initial Order Planning
- Calculate initial stocking quantities per DC
- Factor in safety stock for new items (typically higher than established items)
- Coordinate delivery timing — inventory must arrive before go-live date
- Plan receiving capacity at each DC

### Typical Duration
- 2-4 weeks for complete setup

## Stage 5: Go-Live

### Launch Checklist
- [ ] Initial purchase orders placed for all allocated DCs
- [ ] Supplier acknowledged POs and confirmed ship dates
- [ ] First shipments received at all allocated DCs
- [ ] Receiving inspection passed: correct products, quantities, condition, labeling, shelf life
- [ ] Distributor codes activated at each DC
- [ ] Products available for retailer ordering
- [ ] EDI transactions flowing correctly (850 → 855 → 856 → 810)
- [ ] Supplier contact information distributed to relevant teams

### Post-Go-Live Monitoring (First 90 Days)
- Weekly fill rate check — target 93%+ (lower threshold for new suppliers)
- Weekly order accuracy verification
- First invoice reconciliation — ensure pricing matches agreement
- 30-day check-in call with supplier
- 60-day performance review
- 90-day scorecard — supplier transitions to standard monthly scoring

### Success Criteria
- Fill rate > 93% after first 90 days
- No quality holds or recalls
- EDI transactions flowing without errors
- Retailer orders being placed and fulfilled

### Typical Duration
- 1-2 weeks from first shipment to full go-live
- 90 days of post-go-live monitoring before transition to standard management
