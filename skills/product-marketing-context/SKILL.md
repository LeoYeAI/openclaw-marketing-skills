---
name: product-marketing-context
description: "When the user wants to create or update their product marketing context document. Also use when the user mentions 'product context,' 'marketing context,' 'set up context,' 'positioning,' 'who is my target audience,' 'describe my product,' 'ICP,' 'ideal customer profile,' or wants to avoid repeating foundational information across marketing tasks. Use this at the start of any new project before using other marketing skills — it creates `.agents/product-marketing-context.md` that all other skills reference for product, audience, and positioning context."
---

# Product Marketing Context

You help users create and maintain a product marketing context document. This captures foundational positioning and messaging information that other marketing skills reference, so users don't repeat themselves.

The document is stored at `.agents/product-marketing-context.md`.

## Workflow

### Step 1: Check for Existing Context

First, check if `.agents/product-marketing-context.md` already exists.

**If it exists:**
- Read it and summarize what's captured
- Ask which sections they want to update
- Only gather info for those sections

**If it doesn't exist, offer two options:**

1. **Auto-draft from codebase** (recommended): You'll study the repo—README, landing pages, marketing copy, package.json, etc.—and draft a V1 of the context document. The user then reviews, corrects, and fills gaps. This is faster than starting from scratch.

2. **Start from scratch**: Walk through each section conversationally, gathering info one section at a time.

Most users prefer option 1. After presenting the draft, ask: "What needs correcting? What's missing?"

### Step 2: Gather Information

**If auto-drafting:**
1. Read the codebase: README, landing pages, marketing copy, about pages, meta descriptions, package.json, any existing docs
2. Draft all sections based on what you find
3. Present the draft and ask what needs correcting or is missing
4. Iterate until the user is satisfied

**If starting from scratch:**
Walk through each section below conversationally, one at a time. Don't dump all questions at once.

For each section:
1. Briefly explain what you're capturing
2. Ask relevant questions
3. Confirm accuracy
4. Move to the next

Push for verbatim customer language — exact phrases are more valuable than polished descriptions because they reflect how customers actually think and speak, which makes copy more resonant.

---

## Sections to Capture

### 1. Product Overview
- One-line description
- What it does (2-3 sentences)
- Product category (what "shelf" you sit on—how customers search for you)
- Product type (SaaS, marketplace, e-commerce, service, etc.)

### 2. Target Audience
- Primary ICP (Ideal Customer Profile): role, company type, size, industry
- Secondary audiences if applicable
- What they're trying to accomplish (jobs-to-be-done)
- Their biggest pain points and frustrations

### 3. Positioning & Differentiation
- Key differentiators vs. alternatives
- Unique mechanism or approach
- What you're NOT (important for clarity)
- Positioning statement (optional but helpful)

### 4. Value Proposition
- Primary benefit (the most important outcome customers get)
- Secondary benefits
- Proof points (numbers, results, testimonials)

### 5. Pricing
- Price points and tiers
- Free trial or freemium? Terms?
- How pricing is structured (per seat, usage, flat rate)

### 6. Competitive Landscape
- Direct competitors
- Indirect alternatives
- How you win vs. each

### 7. Voice & Messaging
- Brand voice and tone
- Words/phrases to use
- Words/phrases to avoid
- Example copy you love

### 8. Customer Language
- How customers describe their problem
- How they describe the solution they want
- Exact phrases from reviews, interviews, support tickets

---

## Output Format

Save to `.agents/product-marketing-context.md`:

```markdown
# Product Marketing Context

## Product Overview
[content]

## Target Audience
[content]

## Positioning & Differentiation
[content]

## Value Proposition
[content]

## Pricing
[content]

## Competitive Landscape
[content]

## Voice & Messaging
[content]

## Customer Language
[content]

---
*Last updated: [date]*
```

After saving, confirm the file was created and remind the user that all other marketing skills will automatically reference this context.
