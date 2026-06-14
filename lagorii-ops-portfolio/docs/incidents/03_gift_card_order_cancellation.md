# 03 — Gift Card Order Auto-Cancellation (GoKwik App Checkout)

**Type:** Production Incident  
**Stack:** GoKwik · Shopify API · FlexyPe  
**Severity:** High — Revenue & Customer Trust Impact  
**Status:** ✅ Resolved

---

## Problem Statement

After integrating GoKwik checkout into the mobile application, orders placed using gift cards were being automatically cancelled by Shopify immediately after successful payment. Customers received automatic refunds despite completing the purchase — a deeply confusing and trust-damaging experience.

The website checkout (FlexyPe) was unaffected. The failure was specific to the app checkout + gift card combination.

---

## Architecture Context

| Platform | Checkout | Status |
|----------|----------|--------|
| Website | FlexyPe | ✅ Working |
| Mobile App | GoKwik | ❌ Gift card orders auto-cancelled |

Both systems created/imported orders into Shopify.

---

## Initial Symptoms

- Customers reported: "Payment was successful but order was cancelled"
- Shopify sent automatic refunds immediately after order creation
- Issue only occurred in: App + GoKwik + Gift Card combination
- All other payment methods on app worked correctly
- Website gift card orders through FlexyPe worked correctly

---

## Investigation

### Step 1 — Checkout Flow Segmentation

Isolated the failure to a specific combination:

```
Website (FlexyPe) + Gift Card     ✅ Orders successful
App (GoKwik) + Credit/Debit Card  ✅ Orders successful
App (GoKwik) + Gift Card          ❌ Auto-cancelled
```

Conclusion: Issue was in **GoKwik → Shopify integration specifically for gift card payloads**.

### Step 2 — Shopify Order Lifecycle Analysis

Analyzed order creation logs in Shopify.

```
Customer Places Order via GoKwik App (Gift Card)
    ↓
Order Successfully Created in Shopify ✅
    ↓
Shopify Validation/Processing Stage
    ↓  ← FAILURE POINT
Shopify Automatically Cancels Order ❌
    ↓
Automatic Refund Triggered
```

Order creation succeeded — cancellation happened during Shopify's internal validation.

### Step 3 — API Configuration Analysis

**Root Cause Identified:**

GoKwik's app checkout integration was running on an **older Shopify API configuration** that predated the gift card feature addition.

When gift card support was added to the app checkout, the gift card order payload fields sent by GoKwik were not recognized under the previous API authentication/configuration setup.

Shopify treated the incoming gift card payload as invalid → auto-cancelled → auto-refunded.

---

## Broken Workflow

```
Customer Uses Gift Card in App
    ↓
GoKwik Creates Checkout Order
    ↓
Order Sent to Shopify via Old API Config
    ↓
Gift Card Payload Fields Unrecognized
    ↓
Shopify Validation Fails
    ↓
Order Automatically Cancelled
    ↓
Refund Automatically Triggered
```

---

## Resolution

### Immediate: Customer Support Workaround

While root cause was being investigated, coordinated with support team to:
- Guide affected customers to place gift card orders via website (FlexyPe) instead
- Ensure gift card redemption was still possible during the incident window
- Minimize revenue loss and customer frustration

### Technical Fix: Shopify API Configuration Refresh

Escalated to Shopify support with:
- Exact failure pattern (app + GoKwik + gift card only)
- Website vs app comparison
- Order cancellation lifecycle observations
- Post-integration change timeline

Worked with Shopify support to:
1. Analyze Shopify order logs and API request validation behavior
2. Identify that API config needed refresh after new checkout integration
3. Update and align GoKwik gift card payload validation with current Shopify API config

### Post-Fix

- Gift card orders from app checkout processed successfully
- No further auto-cancellations observed
- App checkout fully stable across all payment methods

---

## Fixed Workflow

```
Customer Uses Gift Card in App
    ↓
GoKwik Checkout Creates Order
    ↓
Updated Shopify API Configuration
    ↓
Gift Card Payload Correctly Recognized
    ↓
Order Successfully Created
    ↓
Fulfillment Proceeds Normally
```

---

## Business Impact

| Area | Before | After |
|------|--------|-------|
| App gift card orders | 0% success | Stable |
| Customer trust | Severely damaged | Restored |
| Support tickets (cancellation confusion) | High | Normalized |
| Revenue from gift card redemption | Blocked | Flowing |

---

## Key Learnings

- **Integration changes require end-to-end retesting of all payment paths**, including edge cases like gift cards.
- **Silent Shopify auto-cancellations** are particularly damaging — customers experience successful payment followed by unexpected cancellation.
- **Narrowing the failure to a specific combination** (app + gift card only) accelerated Shopify support's investigation significantly.
- **A temporary operational workaround** (redirect to website checkout) prevents revenue loss during investigation.

---

## Prevention Recommendations

- [ ] After any checkout integration change, run test orders for: credit card, debit card, UPI, gift card (web), gift card (app), COD
- [ ] Monitor Shopify order cancellation rate — alert on any spike
- [ ] Maintain documented test matrix for GoKwik and FlexyPe checkout paths

---

## Skills Demonstrated

`Root Cause Analysis` `Shopify Ecosystem Understanding` `Checkout Workflow Analysis` `API Integration Debugging` `Payment Operations` `Gift Card Workflow` `Cross-Team Coordination` `Operational Workaround Design`
