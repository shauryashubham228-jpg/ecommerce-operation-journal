# 07 — Inventory Reporting & Decision Support System

**Type:** Operational Systems Project  
**Stack:** Google Sheets · Excel · QUERY · FILTER · VLOOKUP · Pivot Tables  
**Stakeholders:** Listing Team · Performance Marketing · Inventory Operations · Marketplace Management  
**Status:** ✅ Built & In Use

---

## Problem Statement

The operations and marketplace teams were navigating a large, unwieldy master inventory sheet manually. Finding actionable SKUs required scrolling, searching, and cross-referencing — time that added up significantly across multiple teams doing similar work every day.

Key pain points:
- Master sheet too large to navigate efficiently
- No shared filtered views for different team needs
- Performance marketing had no reliable way to identify top-sellers for ad campaigns
- Listing team had no quick way to find slow-moving or discount-eligible SKUs
- Zero-sale inventory was invisible until someone dug for it
- No visual reporting for inventory health

---

## Solution Overview

Built a centralized reporting and decision-support system in Google Sheets and Excel with:
- A maintained master inventory sheet
- A dynamic search and filter decision table
- Pivot tables and charts for visual analysis
- Slicers for interactive filtering
- Cross-team collaboration features

The system acts as a **lightweight operational dashboard** without requiring any custom development or BI tooling.

---

## Core Components

### 1. Master Inventory Sheet

The single source of truth for all inventory data.

**Fields tracked:**
- SKU details and identifiers
- Inventory quantity by variant
- Sales performance metrics
- Marketplace listing status
- Discounting flags
- Inventory movement classification (fast/slow/zero)

**Collaboration features:**
- Filter + sort for any team member
- Comment threads on rows for team communication
- Color-coding conventions for priority/status
- Row freezing for navigation across large datasets

---

### 2. Search & Filter Decision Table

The core productivity improvement. A separate sheet where teams enter criteria and get a focused, filtered view — without touching the master sheet.

```
Master Inventory Sheet
    ↓
QUERY / FILTER Functions
    ↓
Search & Filter Decision Table
    ↓
Actionable SKU View (team-specific)
```

**How each team uses it:**

| Team | Use Case | What They Filter For |
|------|----------|----------------------|
| Listing | Discount planning | Slow-moving SKUs, low conversion, overstocked |
| Performance Marketing | Ad campaign selection | Top-sellers, high stock, strong performers |
| Inventory Ops | Cleanup | Zero-sale SKUs, dead inventory, inactive listings |
| Marketplace Mgmt | Listing actions | Marketplace-specific status, pricing opportunities |

---

### 3. Formula Architecture

**Lookup Functions:**
- `VLOOKUP` — fetch SKU details, map marketplace data, retrieve inventory values
- `HLOOKUP` — horizontal data mapping for structured reporting tables

**Query & Filter:**
- `QUERY` — dynamically generate filtered datasets based on inventory status, sales value, SKU performance
- `FILTER` — actionable SKU segregation, operational filtering, dynamic search outputs
- `SUBTOTAL` — summary calculations that respect active filters

**Mathematical:**
- `SUM`, `AVERAGE`, `MULTIPLICATION`, `DIVISION` for inventory calculations

---

### 4. Visual Reporting

**Pivot Tables:**
- Inventory summaries by category
- SKU-level performance aggregation
- Marketplace-specific breakdowns

**Charts & Graphs:**
- Sales trend visualization
- Inventory distribution by status
- Top-performing categories
- Stock movement over time

**Slicers:**
- Interactive dataset filtering
- Segment inventory by any dimension instantly
- Marketplace-specific data separation

---

## Use Cases in Detail

### Marketplace Discounting

Listing teams identify discount candidates by filtering for:
- Days-in-inventory above threshold
- Units sold below minimum expectation
- Overstock vs. reorder point

Result: Targeted discount campaigns instead of blanket promotions.

### Performance Marketing Campaign Selection

Marketing teams filter for:
- Top-selling products (highest units sold)
- High-stock products (sufficient inventory to scale ads)
- Consistent performers (low return rate)

Result: Ad spend allocated to products that can actually fulfill demand.

### Zero-Sale Inventory Identification

Operations teams filter for:
- Products with zero sales in last 30/60/90 days
- Inactive SKUs not listed on any active marketplace
- Dead inventory consuming warehouse space

Result: Data-driven liquidation and clearance decisions.

### Task Allocation

Instead of sharing the full master sheet, managers generate filtered views for specific action sets:
- "These 20 SKUs need repricing — listing team handles this"
- "These 15 SKUs need new photography — content team handles this"

Result: Cleaner workflow handoffs, no confusion about scope.

---

## Business Impact

| Area | Before | After |
|------|--------|-------|
| Time to find actionable SKUs | Manual search (minutes) | Filter + view (seconds) |
| Marketing product selection | Guesswork | Data-backed |
| Discount planning | Reactive | Proactive, filter-based |
| Zero-sale detection | Manual and delayed | Automated via filter |
| Cross-team visibility | Each team navigating master | Shared, filtered views |
| Reporting frequency | Ad hoc | Regular, consistent |

---

## Optimization Opportunities

The current system is effective for current scale. As operations grow, these extensions would add value:

1. **Sell-through rate trend column** — weekly % change in sell-through per SKU
2. **Restock urgency score** — weighted formula: days of stock remaining × sale velocity
3. **Return reason integration** — pull Return Prime size data to flag "exchange-prone" variants
4. **Automated weekly report email** — Google Apps Script to send filtered summaries to each team
5. **Conditional formatting escalation** — color intensity increases with urgency (e.g., darker red = more urgent discount action)

---

## Key Learnings

- **Structured reporting systems improve operational speed** — teams make better decisions faster when data is pre-filtered for their specific job.
- **QUERY and FILTER are underused** — most teams default to manual filtering; a formula-driven filter table eliminates repetitive work.
- **Operational visibility directly impacts marketplace execution** — teams that can see what's slow-moving act on it faster.
- **Lightweight ≠ less powerful** — a well-structured Google Sheet can serve the needs that many companies build custom dashboards for, at zero incremental cost.
- **Collaboration is a feature** — comments, color-coding, and shared views turn a spreadsheet into a coordination tool.

---

## Skills Demonstrated

`Google Sheets Automation` `Excel Reporting` `Inventory Analytics` `Query-based Reporting` `Data Segmentation` `Pivot Table Analysis` `Dashboard Structuring` `Cross-functional Collaboration` `Operational Reporting` `Data-driven Decision Making`

**Functions used:** `QUERY` `FILTER` `VLOOKUP` `HLOOKUP` `SUBTOTAL` `SUM` `AVERAGE`  
**Features used:** Pivot Tables · Charts · Slicers · Conditional Formatting · Row Freezing · Search Tables
