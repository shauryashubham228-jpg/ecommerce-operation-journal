# 01 — Production Checkout Routing Failure

**Type:** Production Incident  
**Stack:** FlexyPe · PayU · XPay · IP Geolocation  
**Severity:** Critical — Revenue Impact  
**Status:** ✅ Resolved

---

## Problem Statement

Lagorii Kids operated a dual-checkout architecture through FlexyPe, routing users based on IP geolocation:

| User Type | Checkout | Payment Gateway |
|-----------|----------|-----------------|
| Domestic (India) | Domestic Checkout | PayU |
| International | International Checkout | XPay |

One afternoon, incoming orders suddenly stopped — while website traffic remained stable and users were actively browsing and adding to cart.

---

## Impact

- Domestic users routed to international checkout (XPay)
- XPay validation failed for domestic users → payment not initiated
- Zero orders created during incident window
- Silent failure — no frontend error visible to users

---

## Investigation

### Step 1 — Funnel Analysis

```
Homepage Traffic     ✅ Normal
Product Page Visits  ✅ Normal
Add to Cart          ✅ Normal
Checkout Initiation  ✅ Normal
Payment Gateway      ❌ Not reached
Order Success        ❌ Zero
```

Users were reaching checkout but not triggering payment gateway requests.

### Step 2 — Manual Reproduction

Tested across mobile, desktop, multiple user flows.

**Discovery:** Domestic (Indian) users were landing on the international checkout page instead of the domestic flow.

### Step 3 — Root Cause

FlexyPe's IP-based geolocation routing had misconfigured — domestic IPs were incorrectly classified as international, triggering XPay instead of PayU. XPay validation failed for domestic cards/UPI, silently blocking all payments.

---

## Expected vs Actual Flow

```
EXPECTED:                          ACTUAL (during incident):
Indian User                        Indian User
    ↓                                  ↓
Domestic Checkout (FlexyPe)        International Checkout (FlexyPe)
    ↓                                  ↓
PayU Gateway                       XPay Validation
    ↓                                  ↓
Payment Success                    FAILURE — Payment Not Initiated
    ↓                                  ↓
Order Created                      Order NOT Created
```

---

## Resolution

1. Escalated to FlexyPe checkout team with:
   - Screenshots of incorrect checkout page
   - Mobile + desktop reproductions
   - Exact checkout flow observations
2. FlexyPe identified and corrected the routing configuration
3. Domestic users routed correctly post-fix
4. PayU gateway initialized successfully
5. Order flow restored

---

## Business Impact

| Before | After |
|--------|-------|
| Near-zero orders during incident | Normal conversion restored |
| Silent checkout failure | Routing validated and monitored |
| No payment attempts logged | PayU successfully processing |

---

## Key Learnings

- **Silent failures are dangerous.** No frontend error = delayed detection. Order volume monitoring is essential.
- **Checkout routing must be validated end-to-end after any FlexyPe config change.**
- **IP-based segmentation requires dedicated test coverage** — domestic/international paths must both be verified.
- **Mobile-device testing is critical** — routing issues often manifest differently on mobile.

---

## Prevention Recommendations

- [ ] Set up order volume alert (>30% drop from 7-day rolling average triggers alert)
- [ ] Add post-deployment checkout smoke test for both domestic and international paths
- [ ] Monitor payment gateway initialization rate as a leading indicator

---

## Skills Demonstrated

`Production Incident Investigation` `Ecommerce Funnel Analysis` `Checkout Flow Debugging` `Payment Routing Analysis` `Root Cause Identification` `Cross-functional Escalation` `Revenue Impact Analysis`
