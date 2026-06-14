# 06 — Exchange Workflow Design (From Scratch)

**Type:** Process Design Project  
**Stack:** Return Prime · Shopify · Warehouse Operations  
**Status:** ✅ Implemented

---

## Problem Statement

The company had no exchange capability. Customers who wanted a different size had to:
1. Return the product and wait for refund/store credit
2. Then manually place a new order

This was unnecessary friction for what was, fundamentally, a simple size swap. It increased refund processing costs, created drop-off risk after returns, and gave customers a worse experience than they needed.

---

## The Data That Drove the Decision

Using Return Prime's analytics dashboard, I identified a clear pattern:

> **More than 55% of monthly returns were size-related** — size mismatch, fit issues, or variant replacement requests.

This was the key insight. The majority of returning customers weren't dissatisfied with the product — they just needed a different size. A refund-only workflow was solving the wrong problem for most returns.

---

## Feasibility Analysis

Before designing the workflow, analyzed:

### Inventory Dependency
- Exchange only works if replacement stock exists
- Frequently exchanged sizes need deeper inventory buffers
- Stock verification must happen before exchange fulfillment is confirmed

### Shopify Order Handling
- Exchange orders need to be operationally distinct from normal orders
- Warehouse must be able to identify and prioritize exchange fulfillment
- Order state management must support a temporary hold before fulfillment

### Return Prime Capability
- Return Prime supports exchange approval within the returns workflow
- Can trigger Shopify order creation or tagging on exchange approval

---

## Workflow Designed

### Old Workflow (Return Only)

```
Customer Wants Different Size
    ↓
Only Refund/Store Credit Available
    ↓
Customer Receives Refund
    ↓
Customer Must Place New Order Manually
    ↓
(Risk: customer never re-orders)
```

### New Exchange Workflow

```
Customer Requests Exchange (via Return Prime)
    ↓
Exchange Approved
    ↓
Shopify Order Tagged: "Exchange RP"
    ↓
Order Enters Hold State
    ↓
Warehouse Verifies Replacement Inventory
    ↓
Stock Confirmed → Order Released to Fulfillment
    ↓
Replacement Packed & Shipped
    ↓
Customer Receives Replacement
```

---

## Key Design Decisions

### 1. Tagging Convention: `Exchange RP`

All exchange orders receive the Shopify tag `Exchange RP`.

**Why this matters:**
- Operationally separates exchange orders from standard fulfillment queue
- Warehouse staff can identify and handle exchanges differently
- Enables filtering and reporting on exchange volume
- Creates an auditable trail of exchange activity

### 2. Hold State Before Fulfillment

Exchange orders are held before entering the fulfillment queue.

**Why this matters:**
- Prevents fulfillment of an exchange when replacement stock doesn't exist
- Gives warehouse time to verify inventory depth for the requested variant
- Avoids customer disappointment from confirmed exchange that can't be fulfilled

### 3. Inventory Verification Gate

Stock must be confirmed before the order moves to fulfillment.

**Logic:**
```
Exchange Approved
    ↓
Check: Is replacement variant in stock?
    ├── YES → Release to fulfillment
    └── NO  → Flag for manual handling (offer alternative size or store credit)
```

---

## Inventory Planning Insight

The 55% size-return data had a second implication: **frequently exchanged sizes need buffer stock**.

If Size M in a specific style is frequently being exchanged to Size L, the warehouse needs more Size L units than sell-through alone would suggest. Exchange demand must be factored into restock planning.

This was flagged as an operational recommendation: maintain extra units per variant for styles with high exchange rates.

---

## Business Impact

| Area | Before | After |
|------|--------|-------|
| Exchange capability | None | Full workflow live |
| Size-related return resolution | Refund only | Exchange or refund (customer choice) |
| Customer retention post-return | At risk | Improved |
| Operational visibility (exchange orders) | None | Tagged + trackable |
| Fulfillment confusion | N/A | Eliminated via hold-state |
| Unnecessary refund processing | High | Reduced |

---

## Future Optimization Opportunities

- **Automate stock check on exchange approval:** If Return Prime can trigger a Shopify inventory API call, the hold → release step can be automated rather than manual
- **Exchange SLA tracking:** Measure time from exchange approval to shipment; target <48h
- **Size recommendation on exchange:** If requested size is out of stock, suggest nearest available size proactively
- **Exchange rate as a KPI:** Track what % of returns convert to exchanges (target: increase over time)

---

## Key Learnings

- **Data should drive process design.** The 55% size-return insight made the business case undeniable — without that number, the project might not have been prioritized.
- **A hold state is better than a failed fulfillment.** Verifying stock before confirming the exchange is better UX than confirming and then failing.
- **Tagging is underrated as an operational tool.** A simple Shopify tag creates operational separation, filtering capability, and an audit trail with zero custom development.
- **Inventory planning and operations are connected.** Exchange demand must inform restock decisions, not just sell-through.

---

## Skills Demonstrated

`Process Design from Scratch` `Operations Strategy` `Return Prime Analytics` `Shopify Workflow Design` `Inventory Planning` `Warehouse Fulfillment Coordination` `Root Cause Analysis` `Customer Experience Optimization` `Data-Driven Decision Making`
