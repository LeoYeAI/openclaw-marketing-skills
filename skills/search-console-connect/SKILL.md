---
name: search-console-connect
description: "Connect to Google Search Console API to pull real organic search data — traffic trends, ranking positions, impressions, CTR, top queries, and page-level performance. Use when the user wants to audit SEO with real data, diagnose traffic drops, find quick-win keywords, or understand what's actually driving (or losing) organic traffic. Enhances seo-audit and ai-seo skills with real GSC data. Triggers on: 'why did my traffic drop', 'what keywords am I ranking for', 'SEO audit with real data', 'Search Console data', 'organic traffic analysis', 'which pages to optimize'."
---

# Search Console Connect

You are an SEO analyst with direct access to the user's Google Search Console data. You pull real traffic and ranking data to replace guesswork with evidence — then tell the user exactly what to fix and in what order.

## Setup (First Time)

Check for `.agents/search-console-credentials.json`. If missing, guide setup:

### Option A: gcloud CLI (Easiest)

```bash
# Install Google Cloud SDK if not present
# Then authenticate:
gcloud auth application-default login \
  --scopes=https://www.googleapis.com/auth/webmasters.readonly

# Enable Search Console API
gcloud services enable searchconsole.googleapis.com
```

Credentials auto-saved to `~/.config/gcloud/application_default_credentials.json`

### Option B: Service Account (For Automation)

1. Google Cloud Console → IAM → Service Accounts → Create
2. Download JSON key
3. In Search Console → Settings → Users and Permissions → Add user (service account email, Owner)
4. Save key path to `.agents/search-console-credentials.json`:

```json
{
  "type": "service_account",
  "key_file": "/path/to/service-account-key.json",
  "site_url": "https://yourdomain.com"
}
```

---

## Data Pull

```bash
python skills/search-console-connect/scripts/pull.py \
  --site https://yourdomain.com \
  --days 90 \
  --output .agents/gsc-data.json
```

Fetches:
- **Top queries**: impressions, clicks, avg position, CTR (last 90 days)
- **Top pages**: same metrics by URL
- **Traffic trend**: daily clicks over time (spot drops)
- **Position distribution**: how many keywords rank 1-3, 4-10, 11-20, 21-50, 51+
- **Coverage report**: indexed vs. not indexed, errors

---

## Analysis Framework

### Traffic Drop Diagnosis

If the user reports a drop, run this sequence:

1. **Date the drop** — find the exact day traffic fell in the trend data
2. **Check algorithm** — cross-reference with [Google algorithm update history](https://moz.com/google-algorithm-change)
3. **Identify affected pages** — compare page performance before/after drop date
4. **Identify affected queries** — same comparison at query level
5. **Pattern match** — is it sitewide (technical) or topic-specific (content)?

### Quick Win Detector

Find keywords where:
- **Position 4-20** AND impressions > 100/month → ranking improvement opportunity
- **High impressions, low CTR** (position 1-5 but CTR < expected) → title/meta fix
- **Position 1-3 on a page with no internal links** → link juice opportunity

Expected CTR benchmarks:
| Position | Expected CTR |
|----------|-------------|
| 1 | 28-35% |
| 2 | 15-20% |
| 3 | 10-13% |
| 4-5 | 6-8% |
| 6-10 | 2-4% |

If actual CTR is significantly below benchmark → title tag or meta description needs work.

### Content Gap Finder

Queries with:
- Impressions > 200/month
- Average position > 20
- Your site appears but never wins

= Topics where you're visible but not competitive. These are content upgrade candidates.

### Keyword Cannibalization Detector

Find queries where 2+ of your pages compete:
- Same query appears with different URLs across time periods
- Both pages rank 10-30 (neither wins)

= Merge or differentiate those pages.

---

## Output Format

### Site Health Summary
```
Site: yourdomain.com | Period: Last 90 days
Total Clicks: XX,XXX | Impressions: XXX,XXX | Avg CTR: X.X% | Avg Position: XX.X

Position Distribution:
  Top 3:    XXX keywords (XX% of impressions)
  4-10:     XXX keywords ← main opportunity zone
  11-20:    XXX keywords
  21-50:    XXX keywords
  51+:      XXX keywords

Traffic trend: [↑ stable / ↓ dropped X% on YYYY-MM-DD / ↗ growing]
```

### Top 3 Quick Wins

Always output these — the highest-ROI actions based on real data:

1. **[Keyword]** — Position X.X, XXX impressions/mo, CTR X.X% (expected X%)
   - Fix: Rewrite title tag to better match search intent
   - Estimated impact: +XX clicks/mo

2. **[Page URL]** — Ranking for XX queries in position 4-15
   - Fix: Add internal links from high-authority pages
   - Estimated impact: 1-3 position improvement

3. **[Topic]** — XX queries, avg position 25, you're visible but losing
   - Fix: Upgrade content depth/structure
   - Estimated impact: Enter top 10 within 60 days

### Traffic Drop Report (if applicable)
```
Drop detected: YYYY-MM-DD | Before: XXX clicks/day | After: XXX clicks/day (-XX%)

Affected pages (top 5 by traffic lost):
1. /page-url — lost XX clicks/day
2. ...

Affected query types: [branded / informational / commercial / navigational]
Likely cause: [algorithm update / technical issue / content devaluation]
Recommended action: [specific fix]
```

---

## Integration with Other Skills

- **seo-audit**: Run this first, then seo-audit uses real GSC data instead of crawl-only analysis
- **ai-seo**: Identify which queries are being won by AI Overviews vs. organic
- **programmatic-seo**: Find keyword clusters to build pages around
- **content-strategy**: Base content calendar on real query gaps
- **meta-tags-optimizer**: Find high-impression/low-CTR pages to fix first

---

## References

- [Setup Guide](references/setup-guide.md): Detailed OAuth and service account setup
- [Query Library](references/query-library.md): Pre-built API queries for common analyses
- [Algorithm Update Timeline](references/algorithm-updates.md): Cross-reference traffic drops with known updates

---

## Related Skills

- **seo-audit**: Full technical + on-page SEO audit (pair with this for complete picture)
- **google-ads-connect**: Pair for full search visibility — paid + organic in one view
- **ai-seo**: For optimizing content to appear in AI Overviews and AI search
- **programmatic-seo**: Scale content creation based on real keyword gaps found here
- **content-strategy**: Turn GSC keyword gaps into a content calendar
