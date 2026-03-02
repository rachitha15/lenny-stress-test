---
name: stress-test
description: Test PRD assumptions against insights from Lenny Rachitsky's podcast guests. Use when PM wants to stress test GTM, metrics, pricing, MVP, or problem statement sections.
---

# Lenny Lens: Assumption Stress Test

Use this skill when a PM wants to test the implicit assumptions in a specific
section of their PRD against real experiences from Lenny Rachitsky's podcast guests.

---

## When to apply

Trigger this skill when the user says any of the following:
- "Test assumptions in my [section] section"
- "What would Lenny's guests say about my [section]"
- "Stress test my [GTM / metrics / pricing / MVP / problem statement]"
- "Challenge my thinking on [section]"

Supported section types: GTM, metrics, pricing, MVP scope, problem statement, 
activation, retention, stakeholder alignment.

---

## How to find the PRD content

Check in this order:
1. Current conversation context — has the PM been writing a PRD in this thread?
2. Attached document — is there a PRD file attached?
3. Pasted content — has the PM pasted a section directly?

Always read the full PRD when available — not just the target section. The problem 
statement, solution approach, and target user context are essential background for 
identifying what any specific section is implicitly assuming. If only a single 
section has been shared without broader context, note this and work with what 
is available.

Never ask the PM to paste content you already have access to.
If none of the above exist, ask: "Can you share the PRD or the section 
you'd like me to test?"

---

## Step 1: Identify the section type

Determine which section the PM wants tested. If unclear, ask one question:
"Which section — GTM, metrics, pricing, MVP scope, or something else?"

---

## Step 2: Extract implicit assumptions

Before extracting assumptions, read the full PRD for context — specifically the 
problem statement and solution sections. Understanding what problem is being solved 
and for whom is essential to identifying what the target section is actually taking 
for granted. The assumptions in a GTM section mean very different things depending 
on whether the product is B2B or B2C, new category or existing market, sales-led 
or product-led.

Then read the target section carefully. Extract 3 implicit assumptions — things the 
section takes for granted but does not explicitly justify.

Focus on assumptions that are:
- Behavioural ("users/merchants will do X")
- Market ("the market works like Y")
- Technical ("this approach will achieve Z")
- Competitive ("competitors cannot or will not do W")

Do NOT extract assumptions that are explicitly stated and justified in the PRD.
You are looking for what is taken for granted, not what is argued.

### Section-specific assumption lenses

**GTM section:** Look for assumptions about channel behaviour, sales motion 
feasibility, adoption sequence, and who will champion the product internally 
at the customer.

**Metrics section:** Look for assumptions about what behaviour the metric 
actually captures, whether the metric is gameable, leading vs lagging 
indicator assumptions, and baseline availability.

**Pricing section:** Look for assumptions about willingness to pay, 
price sensitivity of different segments, competitive price anchoring, 
and intermediary margin acceptance.

**MVP scope section:** Look for assumptions about what is sufficient to 
validate the hypothesis, what users will tolerate in an early version, 
and what engineering complexity is being underestimated.

**Problem statement section:** Look for assumptions about problem frequency, 
severity, who actually owns the problem, and whether the stated problem 
is the real problem or a symptom.

**Activation/retention section:** Look for assumptions about what behaviour 
predicts retention, whether the activation event is in the product's control, 
and whether correlation is being treated as causation.

---

## Step 3: Formulate retrieval queries

For each assumption, formulate ONE precise retrieval query to send to 
the Lenny Lens API.

Query formulation rules:
- Write in present tense, not retrospective ("how do companies" not 
  "what did guests regret")
- Make it specific to the underlying mechanism, not the surface topic
  (not "ad network pricing" but "why do supply side partners stay on 
  a platform instead of going direct")
- Strip out company-specific and India-specific context — the corpus 
  is primarily US/global, so abstract to the universal version of the 
  assumption
- Aim for 10-15 words maximum

---

## Step 4: Call the Lenny Lens API

For each assumption, make one API call:

```
POST https://lenny-lens-production.up.railway.app/retrieve-chunks
Headers: 
  Content-Type: application/json
  x-api-key: engage2025
Body: {"query": "[your formulated query]", "limit": 5}
```

Make all 3 calls. Do not wait for user input between calls.

---

## Step 5: Evaluate retrieval confidence

For each call, check the similarity scores returned:
- Above 0.65: High confidence — surface this finding prominently
- 0.50–0.65: Medium confidence — surface but flag as partial signal
- Below 0.50: Low confidence — note that corpus has limited coverage 
  on this assumption, do not fabricate relevance

---

## Step 6: Synthesise and respond

Structure your output as follows. Keep it short — the goal is 3 sharp 
findings, not a comprehensive review.

---

**Assumption stress test: [Section name]**

**Assumption 1:** [State the implicit assumption in one sentence]
*What Lenny's guests experienced:* [Guest name — specific experience or 
insight from the chunk, 2 sentences max. Always cite episode title.]
*Verdict:* Validates / Challenges / Partial signal / No corpus coverage

**Assumption 2:** [State the implicit assumption in one sentence]
*What Lenny's guests experienced:* [Same format]
*Verdict:* Validates / Challenges / Partial signal / No corpus coverage

**Assumption 3:** [State the implicit assumption in one sentence]
*What Lenny's guests experienced:* [Same format]
*Verdict:* Validates / Challenges / Partial signal / No corpus coverage

**The hardest question this surfaces:**
[One specific question the PM should be able to answer before their 
next stakeholder review. Make it concrete and uncomfortable.]

**Context note:**
[One sentence flagging where the corpus context (US/SaaS/B2C) may 
not translate directly to the PM's context. Only include if genuinely 
relevant — skip if context gap is small.]

---

## Critical rules

- Never fabricate guest quotes or episode titles
- Never surface a finding with similarity below 0.50 without explicitly 
  flagging low confidence
- Never reproduce the full chunk text — synthesise in your own words
- Never ask the PM to validate your assumption extraction before calling 
  the API — extract, retrieve, then present
- If the PM's section is very short (under 100 words), ask for the 
  surrounding context before extracting assumptions
- The output should be readable in under 2 minutes. If it exceeds 
  400 words, cut it.
