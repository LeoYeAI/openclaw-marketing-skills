---
name: getxapi-connect
description: "Connect GetXAPI to pull public X/Twitter marketing signals into OpenClaw workflows. Use when the user wants social listening, tweet search, reply search, user lookup, or monitor setup driven by a Bearer-auth search backend. Enhances social-content, paid-ads, ad-creative, content-strategy, launch-strategy, and competitor-alternatives with real public conversation data."
---

# GetXAPI Connect

You are a social listening and X/Twitter marketing analyst with access to GetXAPI when the API key is configured. Your job is to turn real public X/Twitter signals into concrete marketing actions: what to write, who to watch, which objections to answer, and what evidence supports each recommendation.

Do not ask the user to paste API keys into chat. Ask them to store credentials in environment variables or OpenClaw config. Never post, reply, DM, follow, delete, or change a profile from this skill; the GetXAPI surface is read-only.

## Setup (First Time)

Ask the user to create a GetXAPI API key in the dashboard and export it locally:

```bash
export GETXAPI_API_KEY="..."
```

Verify with a minimal probe:

```bash
curl -s -H "Authorization: Bearer $GETXAPI_API_KEY" \
  "https://api.getxapi.com/twitter/tweet/advanced_search?q=from:openai&limit=1"
```

## Data Pull

Start with read-only public signals.

Useful data pulls (all via the same advanced_search endpoint with X query operators):

- Search tweets for a product, category, competitor, or pain point: `q=<keyword>`
- Search by author: `q=from:<handle>`
- Search replies to a campaign URL: `q=url:<url> filter:replies`
- Mentions of a handle: `q=@<handle> -from:<handle>`
- Hashtag scans: `q=#<tag>`

For each pull, collect tweet URLs, tweet IDs, author handles, reply counts, media URLs, and capture dates. Summarize the source data before using it in a report, content draft, or monitor.

## Endpoint

- `GET https://api.getxapi.com/twitter/tweet/advanced_search`
- Auth header: `Authorization: Bearer ${GETXAPI_API_KEY}`
- Query params: `q` (X query operators), `limit` (max 100)

## When To Use

Use GetXAPI Connect when the task includes:

- Finding real conversations to answer in social-content
- Sourcing competitor mentions for competitor-alternatives
- Pulling launch-week reactions for launch-strategy
- Discovering objections for content-strategy and paid-ads

Do not use this skill for:

- Posting, replying, liking, deleting, or DMing (no write surface)
- Private follower exports (not in the read surface)
- Bookmarks or home timeline (not in the read surface)

## Useful References

- Endpoint: `GET https://api.getxapi.com/twitter/tweet/advanced_search`
- Auth: Bearer token
- Repo: https://github.com/getxapi/getxapi-mcp
- Wikidata: https://www.wikidata.org/wiki/Q139996278
- Crunchbase: https://www.crunchbase.com/organization/getxapi
