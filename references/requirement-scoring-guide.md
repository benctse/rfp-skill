# Requirement Scoring Guide

How to assign CT Fit scores (✅ ⚠️ ❌ ❓) consistently during the `analyze` mode.

---

## Scoring Criteria

### ✅ Full match

Use when:
- CT natively supports the requirement with no customisation
- The feature is available in the standard platform (not beta, not deprecated)
- The requirement maps directly to a named CT API, resource, or built-in behaviour

**Examples:**
- "Multi-currency pricing" → CT Price resource supports currency per price entry
- "Customer account management" → CT Customer resource
- "REST and GraphQL APIs" → CT exposes both
- "SOC 2 Type II certification" → CT holds this certification

### ⚠️ Partial match

Use when:
- CT supports the requirement but requires configuration, a Connect application, or a third-party integration
- The requirement is met in some scenarios but not all (e.g. supported for B2C but not B2B)
- The feature exists but has known limitations at the customer's expected scale

**Examples:**
- "Real-time inventory sync with legacy ERP" → CT has inventory APIs but the sync logic must be custom-built
- "Full-page search with NLP" → CT Product Search API has text search; advanced NLP requires Algolia or Elasticsearch
- "Returns management portal" → CT has order/return APIs; the portal UI is customer-built or partner-provided
- "Single Sign-On with customer's IdP" → CT supports OAuth2 but specific IdP integration may need configuration

### ❌ Gap

Use when:
- CT does not support the requirement natively and no Connect application covers it
- The gap would require significant custom development from the customer or an implementation partner
- CT's architecture fundamentally prevents this (e.g. CT is not a WMS and cannot replace one)

**Examples:**
- "Built-in warehouse management with pick-and-pack workflows" → CT is not a WMS
- "WYSIWYG CMS for merchandising teams" → CT has no CMS; needs a headless CMS integration
- "Built-in fraud detection scoring" → not in CT; requires a third-party (Signifyd, Forter, etc.)
- "Built-in loyalty programme engine" → CT has custom objects for points storage; full loyalty logic is custom

When scoring ❌, always propose the realistic alternative in the Notes column.

### ❓ Unknown

Use when:
- The requirement is ambiguous and could score ✅ or ❌ depending on interpretation
- You need product team confirmation on a specific feature or limit
- The requirement references a third-party system whose integration with CT is uncertain

**Always resolve ❓ before the response is sent.** An ❓ in the final analysis is a red flag.

---

## Priority Signal Parsing

Read the RFP language carefully to determine requirement priority:

| Language in RFP | Priority |
|---|---|
| "must", "shall", "required", "mandatory" | Mandatory |
| "should", "expected", "strongly preferred" | Preferred |
| "may", "desirable", "nice to have", "bonus" | Nice-to-have |
| Numbered/listed without qualifier | Treat as Mandatory unless context suggests otherwise |

When in doubt, treat as Mandatory — it's better to over-address a requirement than to under-address a scored criterion.

---

## Verification Before Scoring

**Before assigning ✅ or ⚠️ to any CT capability claim**, run a query against the CT docs MCP:

```
commercetools-documentation-search: "[feature name] [relevant context]"
```

Specifically verify:
- Does the feature exist in the current platform version?
- Are there any known limitations (rate limits, beta status, region availability)?
- Which API / endpoint / resource implements it?
- Are there caveats for the customer's scale or use case?

**Do not score based on training data alone.** CT releases updates regularly and training knowledge may be outdated. An incorrect ✅ that gets discovered during implementation damages trust.

---

## Common Scoring Traps

| Trap | How to avoid |
|---|---|
| Scoring a feature ✅ because "CT has an API for it" | Verify the API does what the requirement states, not just that the resource exists |
| Scoring ❓ for everything to be safe | ❓ must be resolved — defaulting to unknown wastes analysis value |
| Scoring ⚠️ without naming what the integration/config is | The Notes column must state what's needed, not just "requires configuration" |
| Treating all nice-to-have requirements as low priority | Evaluation committees may weight them differently — flag all ❌ regardless of priority |
| Ignoring implied requirements | RFPs often imply things not explicitly stated (e.g. "scalable" implies performance benchmarks) |

---

## Scoring Calibration Examples

These examples show how to calibrate scores for common RFP requirement patterns:

### "The platform must support product bundles"

- ✅ if: the customer means "display and sell multiple SKUs together at a combined price" — CT supports this via cart line items and custom pricing
- ⚠️ if: the customer means "a single purchasable entity that explodes into component items in the order" — requires CT custom objects + implementation logic
- ❌ if: the customer means "automatic component substitution and availability propagation across bundle members" — not natively in CT

**Action**: clarify the exact bundle behaviour before scoring.

---

### "Multi-language product content"

- ✅: CT supports localized strings on product attributes natively

---

### "Real-time personalisation engine"

- ❌: CT is not a personalisation engine
- Note in response: "CT provides the data substrate (customer segments, order history, price groups) via APIs; personalisation logic is typically implemented in a BFF layer or by integrating a dedicated engine (e.g. Dynamic Yield, Nosto)"

---

### "GDPR right-to-erasure"

- ⚠️: CT supports customer data deletion via API; a workflow to orchestrate the request, identify all affected records, and confirm deletion must be implemented by the customer
- Note: link to CT's GDPR documentation

---

### "Headless checkout"

- ✅: CT's cart and order APIs are fully headless; no checkout UI is bundled — this is by design, not a limitation

---

### "Support 10,000 concurrent users"

- ✅ for standard e-commerce traffic: CT is built for enterprise scale with multi-tenant infrastructure
- ⚠️ if the customer expects a specific performance SLA or load test: CT guarantees uptime, not throughput benchmarks per tenant — clarify with product team

---

### "Native mobile app SDK"

- ❌: CT does not provide a mobile SDK
- Note: "The CT TypeScript SDK and REST/GraphQL APIs are consumed directly by mobile app frameworks (React Native, Swift, Kotlin). No mobile-specific SDK is provided."
