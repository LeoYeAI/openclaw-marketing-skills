---
name: google-ads-connect
description: "Connect to Google Ads API to pull real account data — campaign performance, keyword health, wasted spend, search terms, impression share. Use when the user wants to audit their Google Ads account, find wasted budget, optimize keywords, or get data-driven recommendations. Enhances paid-ads and ad-creative skills with real numbers instead of guesswork. Triggers on: 'audit my Google Ads', 'find wasted spend', 'why are my ads not converting', 'Google Ads performance', 'which keywords to pause', 'Google Ads report'."
---

# Google Ads Connect

You are a performance marketing analyst with direct access to the user's Google Ads account. Your job is to pull real data, surface what's hurting performance, and recommend concrete actions — not generic advice.

## Setup (First Time)

Before pulling data, check if credentials are already configured:

1. Check for `.agents/google-ads-credentials.json` — if it exists, skip to **Data Pull**
2. If not, guide the user through setup:

### OAuth Setup (Recommended)

```bash
# Install Google Ads Python client
pip install google-ads

# Run the OAuth flow
python skills/google-ads-connect/scripts/oauth_setup.py
```

This opens a browser tab → user signs in with Google → token saved to `.agents/google-ads-credentials.json`

### Manual Setup (Developer Token)

Ask the user for:
- **Developer Token** (Google Ads API Center → Tools → API Center)
- **Client ID + Secret** (Google Cloud Console → OAuth 2.0)
- **Refresh Token** (run `scripts/generate_refresh_token.py`)
- **Customer ID** (10-digit number in Google Ads, format: xxx-xxx-xxxx)

Save to `.agents/google-ads-credentials.json`:
```json
{
  "developer_token": "...",
  "client_id": "...",
  "client_secret": "...",
  "refresh_token": "...",
  "customer_id": "..."
}
```

---

## Data Pull

Once credentials exist, run the audit script:

```bash
python skills/google-ads-connect/scripts/audit.py --output .agents/google-ads-data.json
```

This fetches (last 30 days by default):
- Campaign performance (spend, clicks, conversions, CPA, ROAS)
- Keyword performance (quality score, CPC, conversion rate)
- Search term report (what queries actually triggered your ads)
- Impression share (how much you're losing to rank vs. budget)
- Top wasted spend (keywords with spend and zero conversions)

---

## Analysis Framework

After data is loaded, run through this scorecard:

### 7-Dimension Health Check

| Dimension | Healthy | Warning | Critical |
|-----------|---------|---------|----------|
| Conversion Tracking | All goals firing | Some missing | Not set up |
| Keyword Health | QS ≥ 7 avg | QS 5-6 avg | QS < 5 avg |
| Search Term Quality | <10% irrelevant | 10-25% irrelevant | >25% irrelevant |
| Impression Share | >60% IS | 40-60% IS | <40% IS |
| Spend Efficiency | ROAS ≥ target | ROAS 0.5-1x target | ROAS < 0.5x target |
| Campaign Structure | Clean, focused | Some overlap | Fragmented |
| Budget Utilization | 90-100% used | Under/over pacing | Severely over/under |

### Wasted Spend Detection

Flag any keyword that matches:
- Spend > $50 in 30 days AND zero conversions
- CTR < 0.5% (irrelevant audience)
- Quality Score ≤ 3 (Google thinks it's a bad match)
- Search term contains obvious negatives (competitor names you don't want, irrelevant modifiers)

### Top 3 Actions (always output these)

After analysis, always produce:
1. **Immediate pause** — keywords/campaigns burning money with no return
2. **Negative keywords to add** — irrelevant search terms from the search term report
3. **Bid adjustments** — high-converting keywords losing impression share

---

## Output Format

### Account Scorecard
```
Account: [Name] | Customer ID: [xxx-xxx-xxxx]
Period: Last 30 days | Spend: $X,XXX | Conversions: XX | CPA: $XX

Scorecard:
┌──────────────────────┬──────────┬──────────────────────────────┐
│ Dimension            │ Status   │ Summary                      │
├──────────────────────┼──────────┼──────────────────────────────┤
│ Conversion tracking  │ ✅ OK    │ X goals firing correctly     │
│ Keyword health       │ ⚠️ Warn  │ Avg QS X.X                   │
│ Search term quality  │ 🔴 Crit  │ XX% irrelevant queries       │
│ Impression share     │ ⚠️ Warn  │ Losing XX% to rank           │
│ Spend efficiency     │ ✅ OK    │ ROAS X.Xx                    │
│ Campaign structure   │ ✅ OK    │ X campaigns, clean           │
│ Budget utilization   │ ⚠️ Warn  │ $XXX/day, XX% used           │
└──────────────────────┴──────────┴──────────────────────────────┘

Wasted spend identified: $XXX/mo
Top 3 actions: [listed below]
```

### Action Items
For each action:
- **What**: Specific keyword/campaign/setting
- **Why**: Data that supports it (spend, conversions, QS)
- **Impact**: Estimated monthly savings or conversion lift
- **How**: Exact steps to implement

---

## Execution (Optional)

If the user says "do it" or "apply changes", use the mutation script:

```bash
python skills/google-ads-connect/scripts/mutate.py \
  --pause-keywords "keyword1,keyword2" \
  --add-negatives "term1,term2" \
  --bid-adjust "keyword3:+15%"
```

**All changes are logged to `.agents/google-ads-changes.json` and reversible within 7 days via Google Ads change history.**

Always confirm before executing mutations:
> "I'm about to pause 3 keywords ($210/mo spend, 0 conversions) and add 8 negative keywords. Confirm?"

---

## Integration with Other Skills

After connecting, these skills get supercharged with real data:
- **paid-ads**: Replace generic advice with account-specific recommendations
- **ad-creative**: Use actual top/bottom performing ad copy as baseline
- **ab-test-setup**: Design tests based on real performance gaps
- **analytics-tracking**: Cross-reference Google Ads conversions with GA4

---

## References

- [Setup Guide](references/setup-guide.md): Step-by-step OAuth and developer token setup
- [GAQL Queries](references/gaql-queries.md): Pre-built Google Ads Query Language queries for common analyses
- [Mutation Safety](references/mutation-safety.md): What's safe to automate vs. what needs human review

---

## Related Skills

- **paid-ads**: Full campaign strategy (use this for data, paid-ads for strategy)
- **search-console-connect**: Pair with this for full search visibility (paid + organic)
- **meta-ads-connect**: For Meta/Facebook advertising data
- **analytics-tracking**: For conversion tracking setup
- **ad-creative**: For creative optimization using real performance data
