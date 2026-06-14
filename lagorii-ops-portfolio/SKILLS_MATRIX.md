# Skills Matrix — Lagorii Kids Operations

> Aggregated skills demonstrated across 7 documented operational case studies.

---

## Technical Skills

### Integration & API
| Skill | Evidence |
|-------|----------|
| Webhook workflow design | UTR refund email fix — Razorpay webhook gating |
| API integration debugging | GoKwik + Shopify API config mismatch identification |
| Webhook authentication | Signature validation in Razorpay webhook setup |
| API lifecycle analysis | Track123 tracking API final-status investigation |
| Checkout flow analysis | FlexyPe routing failure, GoKwik gift card issue |
| Payment gateway understanding | PayU / XPay / Razorpay workflows |

### Ecommerce Platform
| Skill | Evidence |
|-------|----------|
| Shopify ecosystem | Order lifecycle, API config, tagging, gift cards, checkout |
| Return Prime | Analytics, exchange workflow, refund communication |
| FlexyPe checkout | Routing logic, dual-checkout architecture |
| GoKwik checkout | App integration, payload structure, API alignment |
| Judge.me | Review permissions, spam detection, moderation |
| Track123 | Logistics tracking API, status sync |
| Appbrew (React Native) | Navigation lifecycle, filter state persistence |

### Data & Reporting
| Skill | Evidence |
|-------|----------|
| Google Sheets automation | Inventory reporting system |
| Excel reporting | Decision support dashboard |
| QUERY function | Dynamic inventory filtering |
| FILTER function | Actionable SKU segregation |
| VLOOKUP / HLOOKUP | Data mapping and cross-referencing |
| Pivot tables | Inventory and sales aggregation |
| Data segmentation | Multi-team filtered views |
| Conditional formatting | Priority and urgency visualization |

### Mobile & Frontend
| Skill | Evidence |
|-------|----------|
| React Native navigation concepts | Filter persistence diagnosis (Appbrew app) |
| Component lifecycle understanding | State reset vs. navigation stack behavior |
| Frontend state management concepts | AsyncStorage vs. runtime state analysis |
| UX troubleshooting | Back-button vs. swipe gesture behavior analysis |

---

## Operations Skills

### Root Cause Analysis
- Structured 3–5 step investigation methodology applied consistently across all incidents
- Eliminating false hypotheses before narrowing to true root cause
- Distinguishing partial failures from complete failures (e.g., tracking sync)

### Incident Management
- Production incident identification from operational signals (order drops, support ticket spikes)
- Rapid scope isolation (which platform, which user flow, which payment method)
- Escalation with structured evidence (screenshots, samples, specific failure patterns)
- Temporary operational workarounds while permanent fix is in progress

### Process Design
- Exchange workflow designed from scratch based on return analytics
- Hold-state inventory verification process
- Operational tagging conventions for workflow separation

### Cross-Team Coordination
Teams coordinated with across documented case studies:
- FlexyPe technical team
- GoKwik integration
- Shopify support
- Return Prime technical/support
- Razorpay webhook integration
- Track123 technical team
- Judge.me support
- Appbrew technical team
- Internal: Warehouse, Support, Marketing, Listing

---

## Business Skills

| Skill | Evidence |
|-------|----------|
| Revenue impact analysis | Checkout routing failure — silent revenue loss identification |
| Customer experience optimization | UTR refund email, filter persistence, exchange workflow |
| Operational reporting | Inventory decision support dashboard |
| Fraud detection | Spam review attack identification and remediation |
| Inventory planning | Exchange demand → buffer stock insight |
| Marketplace operations | Discount planning, SKU filtering, listing optimization |
| Performance marketing support | Ad campaign product selection via reporting system |
| Support operations | Refund query reduction, exchange support workflow |

---

## Investigation Methodology

Consistent framework applied across all incidents:

```
1. Identify Signal
   └─ Support ticket spike / order drop / anomalous pattern

2. Scope the Problem
   └─ Which platform? Which user type? Which payment method?

3. Eliminate False Hypotheses
   └─ What's working? What changed recently?

4. Isolate Root Cause
   └─ Specific layer, configuration, or timing issue

5. Coordinate Resolution
   └─ Right team + right information + structured escalation

6. Validate Fix
   └─ End-to-end testing + monitoring for recurrence
```

---

## Platform Ecosystem Map

```
                    ┌─────────────────────────────┐
                    │         SHOPIFY              │
                    │    (Order Management Hub)    │
                    └──────────┬──────────────────┘
                               │
         ┌─────────────────────┼─────────────────────┐
         │                     │                     │
    ┌────┴─────┐         ┌─────┴──────┐        ┌────┴────────┐
    │ FlexyPe  │         │  GoKwik    │        │ Return Prime │
    │(Web Checkout)│     │(App Checkout)│      │(Returns/Exchange)│
    └────┬─────┘         └─────┬──────┘        └────┬────────┘
         │                     │                     │
    ┌────┴────┐          ┌─────┴────┐          ┌────┴─────┐
    │  PayU   │          │ Shopify  │          │ Razorpay │
    │  XPay   │          │   API   │          │(Webhooks)│
    └─────────┘          └──────────┘          └──────────┘
         
    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
    │ Track123 │    │Judge.me  │    │ Appbrew  │    │  Google  │
    │(Logistics)│   │(Reviews) │    │(Mobile)  │    │  Sheets  │
    └──────────┘    └──────────┘    └──────────┘    └──────────┘
```
