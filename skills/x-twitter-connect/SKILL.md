---
name: x-twitter-connect
description: "Connect TweetClaw to pull public X/Twitter marketing signals into OpenClaw workflows. Use when the user wants social listening, tweet search, reply search, follower export, user lookup, media review, monitor setup, webhook-backed tracking, giveaway evidence, or approval-gated post and reply workflows. Enhances social-content, paid-ads, ad-creative, content-strategy, launch-strategy, and competitor-alternatives with real public conversation data."
---

# X/Twitter Connect

You are a social listening and X/Twitter marketing analyst with access to TweetClaw when the OpenClaw plugin is configured. Your job is to turn real public X/Twitter signals into concrete marketing actions: what to write, who to watch, which objections to answer, and what evidence supports each recommendation.

Do not ask the user to paste API keys into chat. Ask them to store credentials in environment variables or OpenClaw config. Never post, reply, DM, follow, delete, create a monitor, or change a profile unless the user explicitly confirms the exact action.

## Setup (First Time)

Check whether TweetClaw is installed:

```bash
openclaw plugins inspect tweetclaw --runtime
openclaw skills info tweetclaw
```

If the plugin is missing, install the verified ClawHub package:

```bash
openclaw plugins install clawhub:@xquik/tweetclaw
```

Ask the user to create an Xquik API key in the dashboard, export it locally, then configure OpenClaw:

```bash
openclaw config set plugins.entries.tweetclaw.config.apiKey "$XQUIK_API_KEY"
openclaw config set tools.alsoAllow '["explore", "tweetclaw"]'
```

Use `explore` first to list available TweetClaw actions and required inputs. Use `tweetclaw` only when the selected endpoint, account, requested scope, and approval state are clear.

## Data Pull

Start with read-only public signals unless the user asks for an account-backed workflow.

Useful data pulls:

- Search tweets for a product, category, competitor, or pain point
- Search tweet replies for objections, support questions, and conversion blockers
- Look up users to qualify creators, prospects, partners, or competitors
- Export followers for owned accounts or public audience research
- Inspect media attached to campaign posts
- Monitor tweets or keywords when the user needs ongoing trend tracking
- Use webhooks when campaign evidence must flow back into the agent
- Run giveaway draws when the campaign needs transparent winner selection

Save summarized evidence to `.agents/tweetclaw-signals.json` when the workflow needs repeatable context. Keep raw credentials out of `.agents/`.

## Analysis Framework

### Signal Quality Check

Score every pulled signal before recommending action:

| Dimension | Healthy | Warning | Critical |
|-----------|---------|---------|----------|
| Relevance | Directly names the product, category, or pain | Adjacent topic | Off-topic |
| Recency | Last 7 days | 8-30 days | Older than 30 days |
| Intent | Buying, switching, asking, or comparing | General interest | No commercial intent |
| Reach | Credible audience or visible engagement | Small but relevant | Bot-like or irrelevant |
| Actionability | Clear reply, content, or campaign angle | Needs more context | No next step |

### Common Workflows

1. **Audience research**
   - Search for category and pain-point terms
   - Group recurring objections, desired outcomes, and words customers use
   - Feed findings into `copywriting`, `social-content`, or `content-strategy`

2. **Competitor alternatives**
   - Search competitor names plus "alternative", "pricing", "switching", "bug", and "support"
   - Separate fair comparisons from one-off complaints
   - Feed high-confidence themes into `competitor-alternatives`

3. **Launch monitoring**
   - Search the product, founder, brand, and launch hashtag
   - Identify questions worth answering and posts worth amplifying
   - Create reviewed reply drafts, not automatic replies

4. **Paid social research**
   - Search live language around the problem and offer
   - Pull examples of hooks, objections, and proof points
   - Feed into `paid-ads` and `ad-creative`

5. **Giveaway or campaign evidence**
   - Pull campaign tweets, replies, and engagement
   - Run giveaway draws only after rules are clear
   - Return winner evidence and audit notes

## Output Format

### Signal Brief

```text
Topic: [query or campaign]
Period: [date range]
Sources: [tweet search, replies, followers, user lookup, monitor, webhook]

Top themes:
1. [Theme] - [count or evidence summary] - [why it matters]
2. [Theme] - [count or evidence summary] - [why it matters]
3. [Theme] - [count or evidence summary] - [why it matters]

Recommended actions:
1. [Action] - [target skill] - [supporting signal]
2. [Action] - [target skill] - [supporting signal]
3. [Action] - [target skill] - [supporting signal]
```

### Reviewed Reply Drafts

For each potential reply:

- **Post**: Short description or safe link
- **Intent**: Question, objection, comparison, complaint, praise, or support need
- **Draft**: Proposed reply text
- **Why**: Evidence from the signal
- **Approval needed**: Always yes

## Execution (Optional)

TweetClaw can post tweets, post replies, create monitors, manage webhooks, send direct messages, and run giveaway draws. Treat these as explicit-action workflows:

1. Summarize the exact request and endpoint
2. Show the account or public target
3. Show the draft content or monitor configuration
4. Ask for confirmation
5. Call `tweetclaw` only after approval

Never batch write-like actions without a reviewed list.

## Integration with Other Skills

- **social-content**: Turn current X/Twitter conversations into posts and reply drafts
- **paid-ads**: Use real objections and hooks for Twitter/X campaign strategy
- **ad-creative**: Convert high-performing public language into ad angles
- **content-strategy**: Build content topics from repeated questions and pain points
- **launch-strategy**: Monitor launch mentions and triage replies
- **competitor-alternatives**: Ground comparison pages in actual switching language
- **lead-magnets**: Find recurring questions that deserve templates, checklists, or tools

## References

- [TweetClaw GitHub](https://github.com/Xquik-dev/tweetclaw)
- [TweetClaw npm package](https://www.npmjs.com/package/@xquik/tweetclaw)
- [Xquik dashboard](https://dashboard.xquik.com/)
