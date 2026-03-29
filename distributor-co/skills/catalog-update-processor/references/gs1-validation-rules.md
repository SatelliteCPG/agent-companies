# GS1 Validation Rules for Product Catalog Management

Reference document for validating product data against GS1 standards at a national CPG distributor.

## GTIN Structure

### GTIN-12 (UPC-A) — Retail Units
- 12 digits total
- Digits 1-11: Company prefix + item reference
- Digit 12: Check digit (modulo-10)
- Used for individual retail units (each-level)
- Example: 012345678905

### GTIN-14 — Case Level
- 14 digits total
- Digit 1: Indicator digit (1-8 for standard groupings, 9 for variable measure)
- Digits 2-13: GTIN-12 without check digit
- Digit 14: Check digit (modulo-10)
- Used for cases, inner packs, and pallet levels
- Example: 10012345678902

### Check Digit Calculation (Modulo-10)
1. Starting from the right, alternate multipliers of 3 and 1 (rightmost position gets 3)
2. Sum all products
3. Check digit = (10 - (sum mod 10)) mod 10

Example for GTIN-12 01234567890X:
```
Position:  1  2  3  4  5  6  7  8  9 10 11  [12=check]
Digits:    0  1  2  3  4  5  6  7  8  9  0
Multiply:  1  3  1  3  1  3  1  3  1  3  1
Products:  0  3  2  9  4 15  6 21  8 27  0
Sum = 95
Check = (10 - (95 mod 10)) mod 10 = (10 - 5) mod 10 = 5
```

## GTIN Hierarchy

A product should have GTINs at each packaging level:

```
Pallet (GTIN-14, indicator 1-8)
└── Case (GTIN-14, indicator 1-8)
    └── Inner Pack (GTIN-14, indicator 1-8) — if applicable
        └── Each (GTIN-12 / UPC-A)
```

### Hierarchy Validation Rules
- Each level must have a unique GTIN
- The case GTIN must reference the each-level GTIN in its construction
- Inner pack GTINs must be between each and case levels
- Pallet configuration (Ti x Hi) must produce correct cases-per-pallet count

## Company Prefix Validation

- Every GTIN starts with a GS1 Company Prefix assigned to the brand owner
- Prefix lengths vary: 6-10 digits depending on the company's needs
- A valid GTIN must have a prefix registered with GS1
- Verification: Check against GS1's GEPIR (Global Electronic Party Information Registry)
- Common issue: Suppliers using GTINs with prefixes they don't own, or using placeholder/test GTINs

## Required Product Attributes (GS1 GDSN)

For products published to the Global Data Synchronization Network:

### Mandatory Attributes

| Attribute | GS1 Field | Validation Rule |
|-----------|-----------|-----------------|
| GTIN | gtin | Valid format, correct check digit |
| Product Description | tradeItemDescription | Max 200 characters, no HTML |
| Brand Name | brandName | As registered with GS1 |
| Net Content | netContent | Numeric value + unit of measure |
| Unit of Measure | netContentUnitOfMeasure | Valid UNECE code (OZ, LB, ML, G, etc.) |
| Country of Origin | countryOfOrigin | ISO 3166-1 alpha-2 |
| GPC Category | gpcCategoryCode | Valid GS1 Global Product Classification code |
| Target Market | targetMarketCountryCode | ISO 3166-1 numeric (840 for US) |

### Distributor-Required Attributes (Beyond GS1 Minimum)

| Attribute | Validation Rule |
|-----------|-----------------|
| Case Pack | Integer > 0 |
| Case Dimensions (H x W x D) | Decimal inches, all > 0 |
| Case Gross Weight | Decimal pounds > 0 |
| Unit Dimensions (H x W x D) | Decimal inches, all > 0 |
| Unit Gross Weight | Decimal ounces or pounds > 0 |
| Pallet Ti (cases per layer) | Integer > 0 |
| Pallet Hi (layers per pallet) | Integer > 0 |
| Shelf Life (days) | Integer > 0 |
| Temperature Class | Enum: AMBIENT, REFRIGERATED, FROZEN |
| Storage Temperature Range | Min/Max degrees Fahrenheit |
| Allergen Declarations | List of allergens per FDA Big 9 |

## Validation Rules for Common Issues

### Duplicate Detection
- No two active products should share a GTIN
- Search by GTIN before creating any new product
- If a GTIN match is found, determine: same product (update needed) or data error (wrong GTIN assigned)

### GTIN Reuse Rules
- A GTIN must not be reused for a different product for a minimum of 48 months after discontinuation
- If a product is reformulated significantly, it requires a new GTIN
- Packaging changes that don't affect contents may keep the same GTIN

### When a New GTIN is Required
- Net weight or volume change (any amount — industry standard, though some apply a 20% threshold)
- Product reformulation (ingredient changes affecting allergens, nutrition, or claims)
- New pack size or configuration
- Change of brand owner

### When the Same GTIN is Retained
- Package design change (same contents, same net weight)
- Certification addition or removal (e.g., adding Non-GMO Project seal)
- Ingredient change that doesn't affect allergens, nutrition, or claims
- Pricing change
- Supplier manufacturing location change

## Common Data Quality Issues at Distributor Scale

| Issue | Frequency | Impact | Detection |
|-------|-----------|--------|-----------|
| Invalid check digit | 2-3% of submissions | Product cannot be scanned at retail | Automated check digit validation |
| Missing case dimensions | 5-8% of items | Cannot slot in warehouse | Completeness report |
| Incorrect case pack | 1-2% of submissions | Receiving discrepancies, invoice disputes | Validate against physical receipt |
| Duplicate GTIN | 0.5-1% of new items | Two products sharing a barcode | Pre-creation duplicate search |
| Expired certifications | 3-5% of catalog | Mislabeled products, compliance risk | Annual certification audit |
| Missing allergen info | 2-4% of items | Consumer safety risk, regulatory exposure | Mandatory field enforcement |
| Incorrect hierarchy | 1-3% of items | Case vs. each confusion in ordering | Hierarchy validation rules |

## Data Quality Scoring

For catalog health reporting:

| Quality Level | Completeness | GS1 Compliance | Interpretation |
|---------------|-------------|----------------|----------------|
| Excellent | > 99% | 100% | Retail-ready, minimal manual effort |
| Good | 97-99% | > 99% | Minor gaps, operational but not optimal |
| Needs Work | 95-97% | 97-99% | Regular issues, manual workarounds needed |
| Poor | < 95% | < 97% | Systematic problems, causing downstream errors |
