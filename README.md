# MuleTrace — Financial Crime Infrastructure & Money-Trail Analysis System

> Rajasthan Police Hackathon | Problem Statement PS05  
> Shortlist Round — Action Plan Prototype

---

## Quick Start

1. **Open the prototype**: Double-click `prototype/index.html` in any modern browser (Chrome, Edge, Firefox). No server needed — works fully offline.
2. **Open the wireframe**: Double-click `wireframe/wireframe.html`. To export as PDF, use `Ctrl+P` (Print) and select "Save as PDF" with Landscape orientation.

---

## Screen List

| # | Screen | Description |
|---|--------|-------------|
| 1 | **Watchlist Dashboard** | KPIs, live alert feed, watchlist table, replay simulator, input adapters |
| 2 | **Ingestion & Normalised Ledger** | Upload dropzone, adapter status, searchable/filterable transaction table |
| 3 | **Mule Risk Analysis** | Ranked accounts, 0-100 score with weighted rule breakdown, evidence rows |
| 4 | **Money-Trail Graph** | UTR-seeded Cytoscape.js graph, hop-by-hop expansion, taint propagation |
| 5 | **Domain & IP Intelligence** | RDAP/WHOIS, DNS, SSL/CT, IP ownership, ASN — all with "Indicative" badges |
| 6 | **Timestamp Correlation** | Transaction vs infrastructure event timeline, IST/UTC toggle, caveats |
| 7 | **Relationship Graph** | Cross-case entity graph (accounts, domains, IPs, phones), shared infra links |
| 8 | **Reports & Lawful Requests** | Report preview, PDF/Excel export, auto-drafted information request templates |

---

## 90-Second Demo Script

> Recommended: practice this flow 2-3 times before presenting.

### 0:00 – 0:10 | Dashboard Overview
- Open the prototype. You land on the **Watchlist Dashboard**.
- Point out the 4 KPI cards: 14 accounts monitored, 7 active alerts, 2 open cases, 3 linked infrastructure items.
- Mention the input adapters: "Statements are just one input — the system accepts CSV drops, API feeds, and lawful bank data."

### 0:10 – 0:25 | Replay Simulator (Star Feature)
- Click **Play** on the Replay Simulator.
- Watch transactions stream in: scores update, alerts fire, the watchlist table updates risk chips in real time.
- Say: "This simulates how the system monitors transactions incrementally. Each new transaction re-runs rules on affected accounts."
- Adjust speed to 5x to show rapid ingestion. Pause.

### 0:25 – 0:35 | Mule Risk Analysis
- Navigate to **Mule Risk Analysis** (Screen 3).
- Click on **Mule A1 (ACC-02)** — score 92/100.
- Show the weighted rule breakdown: "Pass-through ratio scores highest — this account forwarded 100% of received funds within 6 minutes."
- Point to evidence rows: "Every flag links to specific transactions."

### 0:35 – 0:50 | Money-Trail Graph
- Navigate to **Money-Trail Graph** (Screen 4).
- Enter victim UTR `UTR2024041700001` and click Search.
- The graph appears: Victim to Mule A1, expanding hop by hop.
- Click "Expand Next Hop" to reveal the split to A2, A3, A4.
- Expand again to show consolidation at A5 and cash-out.
- Say: "Taint score decays per hop — darker nodes are closer to the fraud origin. The chain ends at ATM withdrawal and a crypto exchange."

### 0:50 – 1:05 | Infrastructure Intelligence
- Navigate to **Domain & IP Intelligence** (Screen 5).
- Show the domain card for `secure-trade-india.example`: WHOIS, DNS, SSL certificates.
- Point to "Indicative" badges: "We clearly label all geolocation as indicative, not proof."
- Show the locked KYC field: "Subscriber data requires a lawful information request."

### 1:05 – 1:20 | Cross-Case Linking
- Navigate to **Relationship Graph** (Screen 7).
- Highlight the shared bank account (ACC-13) and shared name server linking Case A and Case B.
- Say: "The system automatically detects when cases share accounts, infrastructure, or identifiers — enabling pattern recognition across investigations."

### 1:20 – 1:30 | Reports
- Navigate to **Reports** (Screen 8).
- Show the report preview and the auto-drafted lawful information request templates.
- Say: "One click generates evidence-indexed reports and pre-fills requests to banks, registrars, and hosting providers with the correct identifiers, timestamps, and time zones."

---

## Synthetic Data Notes

All data in this prototype is **synthetic and fictional**. No real personal data, bank accounts, domains, or IP addresses are used.

| Data Type | Convention Used |
|-----------|----------------|
| People | "Synthetic Victim 01", "Synthetic Victim 02" — no real names |
| Bank accounts | Fictional IDs (ACC-01 through ACC-14) |
| Domains | RFC 2606 reserved `.example` TLD only (e.g., `secure-trade-india.example`) |
| IP addresses | RFC 5737 documentation ranges only: `203.0.113.x`, `198.51.100.x`, `192.0.2.x` |
| ASNs | IANA documentation range: AS64496–AS64511 |
| Phone numbers | Fictional format: `+91 90000 xxxxx` |
| UTR numbers | Synthetic: `UTR2024041700001` etc. |
| Amounts | INR, realistic ranges, clearly labelled as synthetic |
| Timestamps | IST (UTC+5:30), synthetic dates within a ~60-day window |

### Planted Mule Patterns
1. **Rapid in-out transfers**: Mule A1 forwards received funds within 6 minutes
2. **Fan-in from unrelated senders**: Mule A3 receives 14 small credits from different sources
3. **Round-figure layering**: Mule A2 moves funds in exact Rs 50,000 and Rs 1,00,000 chunks
4. **Dormant account reactivation**: Mule A4 was inactive for ~180 days before sudden activity
5. **Repeated counterparty**: Mule A5 appears as beneficiary from multiple mule accounts

### Noise Data
Legitimate accounts (ACC-07, ACC-08) have normal transaction patterns (salary, bills, groceries) to demonstrate that the system does not flag everything — only genuinely anomalous behaviour scores high.

---

## Compliance Features

- Persistent "Synthetic demo data only" banner on every screen
- Geolocation/hosting fields always labelled "Indicative, not proof of identity or location"
- Subscriber, login, KYC data shown as locked items: "Obtainable only through the applicable lawful process"
- Passive intelligence only: RDAP, DNS, CT logs, public feeds
- "Data Sources and Limits" modal accessible from footer
- No specific legal section numbers cited
- No active scanning or probing of third-party servers

---

## Risk Scoring Model

| Rule | Weight | Trigger |
|------|--------|---------|
| Pass-through ratio | 25% | >80% of incoming funds forwarded within 60 min |
| Fan-in unrelated senders | 20% | Credits from >5 unrelated senders in 7 days |
| Round-figure layering | 15% | >50% of transactions are round amounts |
| Dormant reactivation | 20% | Inactive >90 days, then >3 txns in 7 days |
| Repeated counterparty | 10% | Same beneficiary in >2 linked accounts |
| Anomaly deviation | 10% | Supporting signal from baseline behaviour |

**Taint propagation**: Starts at 1.0 at the seed (victim UTR), decays by 0.15 per hop.

**Risk labels**: Low (0-25), Medium (26-50), High (51-75), Critical (76-100).

---

## File Structure

```
MuleTrace/
├── wireframe/
│   └── wireframe.html          # Grayscale wireframe (print to PDF)
├── prototype/
│   ├── index.html              # Interactive prototype (open in browser)
│   └── vendor/
│       ├── cytoscape.min.js    # Cytoscape.js v3.28.1
│       └── chart.umd.min.js   # Chart.js v4.4.1
└── README.md                   # This file
```

---

## Technical Notes

- Single HTML file, no build step, no server required
- Vendor libraries loaded from local `vendor/` folder (CDN fallback)
- Vanilla JavaScript, all state in memory
- Designed for 1366x768 and up, responsive down to tablet
- Dark investigative-ops theme with accessible red/amber/green risk scale (also distinguished by shape and label)

---

*Built for Rajasthan Police Hackathon — Problem Statement PS05*
