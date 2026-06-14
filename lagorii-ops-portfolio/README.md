# 🛍️ Lagorii Kids — Operations & Product Case Study Repository

> A structured documentation of real-world operational problem-solving, integration debugging, process design, and product operations across a D2C kids fashion brand.

---

## 👤 About

This repository documents hands-on work across **product operations**, **ecommerce integrations**, and **process design** at Lagorii Kids — a D2C kids fashion brand operating on Shopify with a multi-platform checkout, returns, logistics, and review ecosystem.

Each case study follows a structured format:
- Problem identification
- Root cause analysis
- Solution design & implementation
- Business impact measurement

---

## 📂 Repository Structure

```
lagorii-ops-portfolio/
├── README.md                          ← You are here
├── ROADMAP.md                         ← Full optimization roadmap
├── docs/
│   ├── incidents/
│   │   ├── 01_checkout_routing_failure.md
│   │   ├── 02_delivery_status_sync_failure.md
│   │   ├── 03_gift_card_order_cancellation.md
│   │   └── 04_spam_review_attack.md
│   └── projects/
│       ├── 05_utr_number_in_refund_emails.md
│       ├── 06_exchange_workflow_design.md
│       └── 07_inventory_reporting_system.md
├── SKILLS_MATRIX.md                   ← Aggregated skills & competencies
└── IMPACT_SUMMARY.md                  ← Consolidated business impact
```

---

## 🗂️ Case Studies

### 🚨 Production Incidents

| # | Incident | Stack | Outcome |
|---|----------|-------|---------|
| 01 | [Checkout Routing Failure](docs/incidents/01_checkout_routing_failure.md) | FlexyPe · PayU · XPay | Orders restored; domestic routing fixed |
| 02 | [Delivery Status Sync Failure](docs/incidents/02_delivery_status_sync_failure.md) | Track123 · Courier APIs | 200+ orders re-synced; returns unblocked |
| 03 | [Gift Card Order Auto-Cancellation](docs/incidents/03_gift_card_order_cancellation.md) | GoKwik · Shopify API | API config fixed; app checkout stabilized |
| 04 | [Spam Review Attack](docs/incidents/04_spam_review_attack.md) | Judge.me | Verified-only reviews enforced |

### 🏗️ Process & Product Projects

| # | Project | Stack | Outcome |
|---|---------|-------|---------|
| 05 | [UTR Number in Refund Emails](docs/projects/05_utr_number_in_refund_emails.md) | Return Prime · Razorpay Webhooks | Webhook-gated emails with verified UTR |
| 06 | [Exchange Workflow Design](docs/projects/06_exchange_workflow_design.md) | Return Prime · Shopify · Warehouse | Full exchange lifecycle from scratch |
| 07 | [Inventory Reporting System](docs/projects/07_inventory_reporting_system.md) | Google Sheets · Excel · QUERY/FILTER | Multi-team decision support dashboard |

---

## 🧠 Key Themes

- **Integration Debugging** — Diagnosing failures across multi-vendor checkout, logistics, and review systems
- **Webhook Engineering** — Using event-driven workflows to fix timing and data integrity issues
- **Process Design from Scratch** — Building exchange workflows where none existed
- **Root Cause Analysis** — Structured 3–5 step investigation methodology across every incident
- **Cross-functional Coordination** — Working with FlexyPe, GoKwik, Track123, Razorpay, Return Prime, Shopify, Appbrew, and Judge.me teams
- **Operational Reporting** — Building Google Sheets systems that replaced manual inventory decision-making

---

## 📊 Impact At A Glance

| Metric | Before | After |
|--------|--------|-------|
| Refund email UTR inclusion | 0% | 100% |
| Delivered order sync (200+ backlog) | Blocked | Restored |
| Exchange option availability | None | Full workflow live |
| App gift card checkout success | 0% | Stable |
| Spam review exposure | Uncontrolled | Verified-only |
| Checkout conversion (routing incident) | Near zero | Restored |

---

## 🛠️ Tech Stack Worked With

`Shopify` `Return Prime` `Razorpay` `GoKwik` `FlexyPe` `Track123` `Judge.me` `Appbrew` `React Native` `Google Sheets` `Excel` `Webhooks` `REST APIs` `PayU` `XPay`

---

## 📄 License

This repository is a personal portfolio of operational case studies. All company-specific data has been generalized for documentation purposes.
