# hmz-paperclip-kpi-monitor

> **Autonomous KPI health monitor | runs 6:00 PM daily | flags underperformance before HMZ sees it**

[![schedule](https://img.shields.io/badge/schedule-6%3A00PM_daily-blue?style=flat)](.) [![kpis](https://img.shields.io/badge/KPIs-28_tracked-green?style=flat)](.) [![status](https://img.shields.io/badge/status-always_on-brightgreen?style=flat)](.) [![company](https://img.shields.io/badge/company-DigiMinds-orange?style=flat)](.)

[Overview](#overview) · [KPIs Tracked](#kpis-tracked) · [Thresholds](#thresholds) · [Escalation](#escalation) · [Tips](#tips)

---

## 🧠 OVERVIEW

Paperclip KPI Monitor runs every evening at 6 PM and checks all 28 active DigiMinds KPI tasks against targets. It calculates variance, trend direction, and health status — then generates a daily scorecard. Critical KPIs below threshold trigger immediate CEO loop escalation.

| Component | Value |
|---|---|
| Trigger | Daily 6:00 PM (LaunchAgent) |
| KPIs tracked | 28 active KPI tasks |
| Escalation threshold | >20% below target = CRITICAL |
| Output | Daily scorecard → Paperclip API |
| Model | Groq Llama 3 (zero Claude tokens) |

---

## 📊 KPI CATEGORIES (28 TOTAL)

| Category | KPIs | Key Metric |
|---|---|---|
| Revenue | 5 | MRR, ARR, deal velocity, pipeline value |
| Lead Generation | 6 | Leads/day, ICP score avg, conversion rate |
| Content | 4 | Post reach, engagement rate, profile visits |
| Client Delivery | 7 | ROAS delivered, client retention, NPS |
| Operations | 6 | Agent uptime, task completion rate, cost/lead |

---

## 🎯 THRESHOLD SYSTEM

| Status | Condition | Action |
|---|---|---|
| 🟢 GREEN | Within 5% of target | No action |
| 🟡 YELLOW | 5-20% below target | Note in scorecard |
| 🔴 RED | >20% below target | CEO loop escalation |
| ⚪ GREY | No data (missed tracking) | Flag data gap |

---

## 💡 TIPS

■ **Monitoring (4)**
| Tip | Source |
|---|---|
| Daily scorecard accessible at `/api/kpi/scorecard?date=today` | API ref |
| RED KPIs auto-appear in next CEO loop cycle (within 6h) | CEO loop integration |
| Historical trend at `/api/kpi/trend?kpi=mrr&days=30` | API ref |
| GREY KPIs mean data pipeline broken — fix before day-end | Operations rule |

■ **Thresholds (3)**
| Tip | Source |
|---|---|
| Thresholds are recalibrated monthly as baselines change | KPI SOP |
| Client delivery KPIs are weighted 3x over operational KPIs | Priority rules |
| MRR is the master KPI — all others subordinate to revenue health | DigiMinds strategy |

---

## ☠️ TOOLS REPLACED

| KPI Monitor | Replaced |
|---|---|
| Daily performance review | Manual spreadsheet check |
| Underperformance detection | Discovering problems from clients |
| Trend analysis | Monthly reviews (too late) |
| Escalation routing | Hoping someone noticed |

---

## ⚠️ GOTCHAS

| Issue | Fix |
|---|---|
| KPI shows GREY | Data source disconnected — check API connections |
| All KPIs show RED same day | Likely data pipeline issue, not real decline |
| Monitor ran but no scorecard | Check Paperclip API logs at port 3100 |
| Thresholds seem wrong | Recalibrate via `/api/kpi/calibrate` |

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil) — Paperclip autonomous KPI monitoring*
