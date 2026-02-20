# AI-Powered Lead Qualifier & CRM Updater
### Built with n8n + OpenAI + Google Sheets

---

## 🎯 Problem It Solves

B2B sales teams waste **2-3 hours daily** manually reading inquiries and deciding who to call first. For a brand like **Luxe Scents** (premium B2B perfume supplier), missing a HOT lead even by a few hours can cost a ₹15-20 lakh deal.

This workflow **fully automates lead triage** — every inquiry is validated, AI-scored, and routed to the right pipeline in under 5 seconds.

---

## ⚡ How It Works

```
Form Submission
      ↓
Validate & Clean Data
      ↓
OpenAI GPT-4o Scores Lead (1-10)
      ↓
Parse & Classify → HOT 🔥 / WARM ⚡ / COLD ❄️
      ↓
Auto-route to Google Sheets CRM
      ↓
Return Response to Form
```

---

## 🏗️ Workflow Nodes

| # | Node | Purpose |
|---|------|---------|
| 1 | Webhook | Receives lead from website form |
| 2 | Code - Validate | Cleans data, blocks invalid emails |
| 3 | OpenAI GPT-4o | Scores and qualifies the lead |
| 4 | Code - Parse | Converts AI response to structured data |
| 5 | IF - Hot Lead? | Routes score 7+ to HOT path |
| 6 | IF - Warm Lead? | Routes score 4-6 to WARM, else COLD |
| 7 | Code - Format Alert | Builds rich alert for sales team |
| 8 | Google Sheets - Hot | Saves HOT leads with CALL TODAY |
| 9 | Google Sheets - Warm | Saves WARM leads with SEND BROCHURE |
| 10 | Google Sheets - Cold | Saves COLD leads with ADD TO NEWSLETTER |
| 11 | Respond - Success | Returns 200 confirmation to form |
| 12 | Error Handler | Catches all errors gracefully |
| 13 | Google Sheets - Errors | Logs errors for audit trail |
| 14 | Respond - Error | Returns 400 with friendly message |

---

## 🤖 AI Scoring Logic

OpenAI GPT-4o analyzes each lead and returns:

```json
{
  "score": 9,
  "intent": "bulk_order",
  "budget_signal": "high",
  "urgency": "immediate",
  "business_category": "hotel",
  "estimated_order_value": "high_value",
  "summary": "Taj Resorts seeking fragrance partner for 18 properties...",
  "recommended_action": "Call today to discuss partnership terms",
  "red_flags": "none"
}
```

### Priority Labels
| Score | Tier | Priority |
|-------|------|----------|
| 9-10 | HOT 🔥 | CALL TODAY |
| 7-8 | HOT 🔥 | CALL THIS WEEK |
| 4-6 | WARM ⚡ | SEND BROCHURE |
| 1-3 | COLD ❄️ | ADD TO NEWSLETTER |

---

## 📊 Google Sheets CRM Structure

4 tabs auto-managed by the workflow:

**Hot Leads / Warm Leads / Cold Leads tabs:**
```
Name | Email | Company | Phone | Score | Priority | Recommended Action | Red Flags | Received At
```

**Errors tab:**
```
Error Message | Timestamp | Raw Input
```

---

## 🧪 Sample Test Payload

```json
{
  "name": "Priya Sharma",
  "email": "priya@tajresorts.com",
  "company": "Taj Resorts & Spas",
  "phone": "+91-9845012345",
  "city": "Mumbai",
  "business_type": "Luxury Hotel Chain",
  "quantity_needed": "500-800 units per month",
  "message": "We are the procurement team at Taj Resorts managing 18 properties. Looking for a premium fragrance partner for lobbies. Budget is ₹15-20 lakhs per quarter. Want to meet this week.",
  "source": "website_form"
}
```

**Expected Result:** Score 10/10 → HOT 🔥 → CALL TODAY → Hot Leads Tab

---

## 🛡️ Error Handling

- Invalid email format → blocked before OpenAI call (saves API cost)
- Message too short → rejected with clear error
- OpenAI parse failure → fallback values, flagged for manual review
- All errors → logged to Errors tab + 400 response returned

---

## 🚀 Setup Instructions

### Prerequisites
- n8n instance (cloud or self-hosted)
- OpenAI API key
- Google account

### Steps
1. Clone this repo
2. Import `AI Lead Qualifier & CRM Updater.json` into n8n
3. Create Google Sheet named `Luxe Scents - Lead CRM` with 4 tabs
4. Add headers to each tab (see above)
5. Connect OpenAI credentials in node 3
6. Connect Google account in nodes 8, 9, 10, 13
7. Replace `Sheet ID` in all Google Sheets nodes
8. Activate workflow
9. Copy production webhook URL
10. Point your form to the webhook URL

---

## 📁 Repository Structure

```
├── README.md
├── AI Lead Qualifier & CRM Updater.json    # Import this into n8n
└── sample_payloads/
    ├── hot_lead.json
    ├── warm_lead.json
    ├── cold_lead.json
    └── error_test.json
```

---

## 💡 Business Impact

| Metric | Before | After |
|--------|--------|-------|
| Time to qualify a lead | 5-10 mins manual | Under 5 seconds |
| Daily triage time | 2-3 hours | 0 hours |
| Lead routing accuracy | Inconsistent | AI-powered, consistent |
| Missed HOT leads | Possible | Impossible |

---

## 🔮 Future Enhancements

- [ ] Auto-send brochure email to WARM leads
- [ ] Slack notification for HOT leads
- [ ] WhatsApp alert via Twilio
- [ ] Daily summary report to sales manager
- [ ] CRM integration (HubSpot / Salesforce)

---

## 🙋 About

Built as part of an **AI Automation Engineer** portfolio.
Demonstrates: Webhook handling · OpenAI integration · Conditional branching · Error handling · Google Sheets CRM

---

⭐ Star this repo if you found it useful!
