# RFP Configuration

## RFP Details

```yaml
rfp_title: ""                    # e.g. "Digital Commerce Platform RFP 2026"
customer_name: ""                # e.g. "Acme Retail Group"
customer_industry: ""            # e.g. "Fashion & Apparel"
rfp_reference: ""                # Reference number from the RFP document, if any
submission_deadline: ""          # e.g. "2026-07-15"
evaluation_date: ""              # e.g. "2026-08-01"
source: ""                       # Path to the RFP document, e.g. "RFP/source/acme-rfp.pdf"
```

---

## Responder Profile

```yaml
company_name: "commercetools"
company_tagline: "The leading composable commerce platform"
company_founded: "2006"
company_hq: "Munich, Germany"
company_employees: "600+"
company_customers: "350+"
company_website: "https://commercetools.com"

contact_name: ""                 # Primary contact for this RFP
contact_title: ""                # e.g. "Senior Solutions Engineer"
contact_email: ""
contact_phone: ""
```

---

## Solution Being Proposed

```yaml
product: "commercetools Composable Commerce"

# Brief description of what you're proposing for this customer
# Keep this customer-specific — not a generic product pitch
value_proposition: |
  [Describe what commercetools offers that directly matches this customer's situation.
  Reference their industry, scale, or stated challenges here.]
```

---

## Core Capabilities

List the capabilities you will highlight in the response. These are checked against RFP requirements in `analyze` mode.

```yaml
capabilities:
  - name: "API-first architecture"
    description: "Every commerce function exposed via REST and GraphQL APIs"
    category: technical

  - name: "Product catalog management"
    description: "Multi-catalog, multi-language, complex variants, product types"
    category: functional

  - name: "Cart and order management"
    description: "Flexible cart calculation, discount engine, order lifecycle"
    category: functional

  - name: "Customer management"
    description: "Customer accounts, groups, addresses, authentication"
    category: functional

  - name: "Promotions and discounts"
    description: "Cart-level and product-level discounts, discount codes, tiered pricing"
    category: functional

  - name: "Multi-store and multi-region"
    description: "Store channels, locale/currency per store, geo-distributed infrastructure"
    category: functional

  - name: "B2B features"
    description: "Business units, company accounts, approval workflows, purchase lists, quotes"
    category: functional

  - name: "Inventory management"
    description: "Multi-supply channel inventory, reservations, backorder support"
    category: functional

  - name: "Search and filtering"
    description: "Product Search API with facets, full-text, geo-search"
    category: functional

  - name: "Pricing engine"
    description: "Tiered, embedded, external price modes; customer-group pricing; channel-specific prices"
    category: functional

  - name: "Extensibility"
    description: "API extensions, subscriptions, custom objects, custom types, Connect applications"
    category: technical

  - name: "Cloud infrastructure"
    description: "Hosted on GCP, multi-region, 99.99% uptime SLA"
    category: operational

  - name: "Security and compliance"
    description: "SOC 2 Type II, ISO 27001, GDPR, PCI DSS (SAQ-A)"
    category: compliance

  - name: "Developer experience"
    description: "TypeScript SDK, Postman collection, comprehensive docs, sandbox environments"
    category: technical

  # Add more capabilities specific to this proposal:
  # - name: ""
  #   description: ""
  #   category: functional | technical | operational | compliance | commercial
```

---

## Case Studies

Provide 2–4 real customer references relevant to this RFP. Only include customers you have permission to reference.

```yaml
case_studies:
  - customer: ""                   # e.g. "Global Fashion Retailer"
    industry: ""                   # e.g. "Fashion & Apparel"
    region: ""                     # e.g. "EMEA"
    challenge: |
      [What problem they had before commercetools]
    solution: |
      [How commercetools was implemented and what capabilities were used]
    outcome: |
      [Measurable results: time to market, conversion, revenue, cost savings]
    can_be_named: false            # true if the customer allows public naming

  - customer: ""
    industry: ""
    region: ""
    challenge: |
    solution: |
    outcome: |
    can_be_named: false
```

---

## Team

List team members who will be named in the proposal.

```yaml
team:
  - name: ""
    title: ""                      # e.g. "Account Executive"
    role_in_engagement: ""         # e.g. "Commercial lead"
    relevant_experience: ""        # 1-2 sentences about their experience for this deal

  - name: ""
    title: ""                      # e.g. "Solutions Engineer"
    role_in_engagement: ""         # e.g. "Technical architect and demo lead"
    relevant_experience: ""

  - name: ""
    title: ""                      # e.g. "Customer Success Manager"
    role_in_engagement: ""         # e.g. "Post-sales implementation and onboarding"
    relevant_experience: ""
```

---

## Pricing Approach

```yaml
pricing_model: "subscription"     # subscription | usage-based | hybrid

# Fill in only what is approved to share in this proposal
# Mark as "TBD" if not yet defined
pricing_tiers:
  - tier: "Starter"
    description: ""
    indicative_price: ""           # e.g. "from €X,000/month"
    included: []

  - tier: "Growth"
    description: ""
    indicative_price: ""
    included: []

  - tier: "Enterprise"
    description: "Custom"
    indicative_price: "Contact us"
    included: []

pricing_notes: |
  All pricing is indicative and subject to final scoping and contract negotiation.
  Prices exclude applicable taxes and implementation partner fees.
```

---

## Response Format Instructions

```yaml
# If the customer specified a required format, describe it here
required_format: ""               # e.g. "Follow the template in Appendix A of the RFP"
page_limit: ""                    # e.g. "50 pages maximum"
file_format: ""                   # e.g. "PDF, font size 11, 2.5cm margins"
submission_method: ""             # e.g. "Upload to procurement portal at ..."
language: "English"               # Response language
```
