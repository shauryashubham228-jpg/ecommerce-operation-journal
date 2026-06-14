# 🗺️ Operations Optimization Roadmap — Lagorii Kids

> This roadmap consolidates learnings from all documented incidents and projects into a forward-looking optimization plan. Each phase addresses systemic gaps identified through hands-on problem-solving.

---

## Overview

```
Phase 1 → Reactive Stability       (Fixing what's broken)
Phase 2 → Proactive Monitoring     (Catching issues before customers do)
Phase 3 → Workflow Automation      (Removing manual steps)
Phase 4 → Data-Driven Operations   (Decisions backed by dashboards)
Phase 5 → Scalable Architecture    (Built to grow)
```

---

## Phase 1 — Reactive Stability ✅ Completed

Issues resolved reactively through structured root cause analysis and cross-team coordination.

### Resolved Incidents

#### 1.1 Checkout Routing Failure
- **Root Cause:** IP-based geolocation routing misconfigured in FlexyPe; domestic users sent to international checkout (XPay)
- **Fix:** Escalated to FlexyPe team; domestic routing corrected
- **Status:** ✅ Resolved

#### 1.2 Delivery Status Sync Failure
- **Root Cause:** Track123 not updating `Out for Delivery → Delivered` for 200+ orders; blocked return eligibility
- **Fix:** Coordinated with Track123; final-mile status refresh reconfigured
- **Status:** ✅ Resolved

#### 1.3 Gift Card Auto-Cancellation (GoKwik App)
- **Root Cause:** Outdated Shopify API configuration after GoKwik checkout integration; gift card payloads rejected
- **Fix:** Shopify API config refreshed; payload validation aligned
- **Status:** ✅ Resolved

#### 1.4 Spam Review Attack (Judge.me)
- **Root Cause:** Public review permissions allowed unauthenticated submissions; bot/VPN abuse from Germany/Russia
- **Fix:** Switched to verified-customers-only review mode
- **Status:** ✅ Resolved

#### 1.5 UTR Missing in Refund Emails
- **Root Cause:** Return Prime triggered refund emails at initiation, before Razorpay generated the UTR
- **Fix:** Webhook integration configured; emails now triggered only after UTR confirmed
- **Status:** ✅ Resolved

---

## Phase 2 — Proactive Monitoring 🔄 Recommended Next

**Goal:** Catch issues before customers report them.

### 2.1 Checkout Funnel Health Monitor
- Set up real-time alerts when order volume drops >30% from rolling 7-day average
- Track checkout initiation → payment attempt → order creation conversion at each step
- Alert on sudden spikes in abandoned carts without corresponding payment attempts
- **Addresses:** Checkout routing failure (was caught late via ops observation)

### 2.2 Logistics Status Watchdog
- Daily automated check: count orders stuck in `Out for Delivery` for >2 days
- Alert if count exceeds threshold (e.g., >10 orders)
- Cross-reference with courier partner expected delivery windows
- **Addresses:** 200+ order backlog that built up silently

### 2.3 Webhook Delivery Monitoring
- Monitor Razorpay webhook delivery success rate
- Alert on failed/delayed webhook events (UTR not received within expected window)
- Log UTR mapping failures separately for investigation
- **Addresses:** Refund email timing dependency on webhook reliability

### 2.4 Review Anomaly Detection
- Weekly report: reviews by country vs. orders by country
- Flag any country with >5 reviews but 0 matching orders
- **Addresses:** Spam review attack recurrence prevention

### 2.5 API Health Checks
- Post any checkout integration update: run a test order through each payment path
- Checklist: Domestic (PayU), International (XPay), Gift Card (GoKwik app), Gift Card (FlexyPe web)
- **Addresses:** Gift card cancellation that only appeared after integration change

---

## Phase 3 — Workflow Automation 🔄 Recommended Next

**Goal:** Remove manual steps that slow operations or introduce human error.

### 3.1 Exchange Workflow Automation
- **Current State:** Exchange orders tagged `Exchange RP` and held manually for inventory verification
- **Optimization:** Auto-check variant stock on exchange approval; auto-release to fulfillment if stock available
- **Benefit:** Reduce warehouse hold time from hours to minutes
- **Stack:** Return Prime webhooks → Shopify inventory API → auto-tag + status update

### 3.2 Refund Communication Pipeline
- **Current State:** Webhook triggers email after UTR confirmed (already improved)
- **Optimization:** Add fallback: if UTR not received within 24h, send a "refund in progress" email with expected timeline
- **Benefit:** Reduce "where is my refund" queries even in edge-case delays

### 3.3 Return Eligibility Auto-Unlock
- **Current State:** Return button depends on Track123 delivery status updating correctly
- **Optimization:** Add secondary trigger: if order has no delivery update for N days past expected delivery, auto-flag for manual review or unlock return option
- **Benefit:** Prevent 200+ order backlog scenario from blocking returns again

### 3.4 Review Moderation Automation
- **Current State:** Manual monitoring for spam reviews
- **Optimization:** Configure Judge.me auto-hold for reviews from unmatched geographies pending manual approval
- **Benefit:** Reduce moderation workload while maintaining brand reputation protection

---

## Phase 4 — Data-Driven Operations 📊 In Progress

**Goal:** Replace manual searching with always-on decision support.

### 4.1 Inventory Decision Dashboard (Extended)
- **Current State:** Google Sheets with QUERY/FILTER for SKU-level analysis
- **Optimization:**
  - Add sell-through rate trend (weekly % change)
  - Add restock urgency score per SKU
  - Integrate return reason data from Return Prime to flag "exchange-prone" sizes
  - Link to marketplace listing status
- **Benefit:** Proactive restocking for frequently exchanged sizes (currently identified as 55%+ of returns)

### 4.2 Returns & Exchange Analytics Report
- Weekly automated report:
  - Return rate by category/size/SKU
  - Exchange conversion rate (returns converted to exchanges vs. refunds)
  - UTR delivery time distribution (refund speed)
  - Refund-related support ticket volume
- **Benefit:** Track impact of exchange workflow and refund communication improvements

### 4.3 Checkout Conversion Tracking (Post-Incident)
- Baseline checkout conversion rate by device (mobile vs. desktop)
- Track weekly to catch routing or payment issues early
- Segment by checkout path: FlexyPe web, GoKwik app
- **Benefit:** Routing incidents like FlexyPe geolocation failure would show immediately as mobile conversion drop

### 4.4 App UX Performance Metrics
- Track filter usage rate in mobile app
- Measure session depth improvement post filter-persistence fix
- **Benefit:** Validate that the Appbrew filter persistence fix actually improved browsing behavior

---

## Phase 5 — Scalable Architecture 🔮 Future State

**Goal:** Build systems that work at 10x current order volume without linear increase in ops effort.

### 5.1 Unified Webhook Event Bus
- Centralize all webhook events (Razorpay, Return Prime, GoKwik, Track123) into a single event log
- Enable replay, auditing, and debugging of any integration failure
- **Benefit:** Faster root cause analysis; no more reconstructing event timelines manually

### 5.2 Order Lifecycle State Machine
- Define all possible order states across Shopify + FlexyPe + GoKwik + Track123 + Return Prime
- Map valid transitions and detect invalid states automatically
- Alert on stuck orders (orders in impossible or unexpected states)
- **Benefit:** Catch checkout routing failures, gift card cancellations, and sync failures within minutes

### 5.3 Exchange Inventory Buffer System
- Based on return analytics (55%+ size-related returns), model minimum buffer stock per size per style
- Auto-generate restock recommendations for top-exchanged variants
- **Benefit:** Ensure exchange fulfillment is never blocked by stock; improve exchange SLA

### 5.4 Multi-Checkout QA Test Suite
- Automated test scenarios run after any checkout-related deployment:
  - Domestic user → PayU checkout ✓
  - International user → XPay checkout ✓
  - Gift card user (web) → FlexyPe ✓
  - Gift card user (app) → GoKwik ✓
  - COD order ✓
- **Benefit:** Catch integration regressions before they hit production customers

### 5.5 Review Trust Score System
- Assign a trust score to incoming reviews based on: order match, geography match, review velocity, IP pattern
- Auto-publish high-trust reviews; hold low-trust for moderation
- **Benefit:** Scale review management without proportional manual effort

---

## Priority Matrix

| Initiative | Impact | Effort | Priority |
|------------|--------|--------|----------|
| Checkout funnel health monitor | 🔴 High | 🟡 Medium | P1 |
| Logistics status watchdog | 🔴 High | 🟢 Low | P1 |
| Exchange workflow automation | 🔴 High | 🟡 Medium | P1 |
| Returns & exchange analytics report | 🟡 Medium | 🟢 Low | P2 |
| Webhook delivery monitoring | 🟡 Medium | 🟡 Medium | P2 |
| Unified webhook event bus | 🔴 High | 🔴 High | P3 |
| Multi-checkout QA test suite | 🔴 High | 🔴 High | P3 |
| Exchange inventory buffer system | 🟡 Medium | 🔴 High | P3 |

---

## Skills Development Roadmap

Based on operational gaps identified across all incidents:

| Skill Area | Current Level | Target | Path |
|------------|--------------|--------|------|
| Webhook integration design | Working knowledge | Advanced | Build custom webhook handler; study event-driven architecture |
| API debugging | Intermediate | Advanced | Learn Postman/curl-based API testing; read Shopify Admin API docs |
| Data pipeline basics | Intermediate | Advanced | Learn basic SQL; explore Shopify Analytics API |
| Mobile app behavior | Conceptual | Working | Study React Native navigation lifecycle; build small test app |
| Ecommerce funnel analytics | Working knowledge | Advanced | Set up GA4 ecommerce events; build funnel dashboards |

---

*Last updated: June 2026*
*Based on: 7 documented operational case studies*
