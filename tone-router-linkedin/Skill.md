---
name: tone-router-linkedin
description: LinkedIn post rewriter. Use when the tone-router has identified a draft as a LinkedIn post, OR when the user explicitly asks to rewrite something for LinkedIn (e.g. "make this a LinkedIn post", "post-ready", "LinkedIn version"). Takes a draft and outputs a hook-first, opinionated, hashtag-tagged post in plain prose. Strips em-dashes, kills AI vocabulary, breaks rule-of-three rhythm, and refuses to hedge.
---

# tone-router-linkedin

Rewrites a draft into a LinkedIn post in the voice of a working operator, not a thought-leadership account.

The LinkedIn feed is full of two kinds of posts. The first is generic motivational text that could have been written by anyone about anything. The second is specific, opinionated, slightly uncomfortable writing from someone who actually does the work. This sub-skill produces the second kind.

---

## Hard rules (non-negotiable)

1. **No em-dashes.** Replace with commas, periods, or restructure the sentence.
2. **No bullet points or numbered lists in the post body.** Prose only. Lists are an AI tell on LinkedIn.
3. **No bolded text.** LinkedIn renders bold but using it screams "AI-formatted".
4. **No "→" arrows, no "•" bullets, no emoji-as-bullet patterns.**
5. **Hashtags go at the very end on their own line.** 5 to 10 hashtags. Lowercase preferred.
6. **No banned vocab** (full list below).
7. **First line is the hook.** It must work as a standalone preview in the LinkedIn feed. No "In this post I will discuss..." openers.
8. **Take a side.** If the original hedges, the rewrite picks one. LinkedIn rewards opinions, not balanced essays.
9. **One concrete detail minimum.** A number, a name, a tool, a specific situation. Posts with zero specifics get scrolled past.
10. **Length 100 to 400 words.** Optimal is 150 to 250.

---

## Banned vocabulary (will not appear in output)

**Tier 1 AI tells:** delve, tapestry, underscore, meticulous, showcase, intricate, multifaceted, garner, testament, realm (figurative), navigate (figurative), landscape (figurative), embark, unlock, unleash, unravel, beacon, bastion, paradigm, synergy, holistic.

**LinkedIn-AI tells:** game-changer, game changer, level up, 10x, supercharge, revolutionize, transform (transitive), thrive, elevate, empower, unlock the power of, harness the power of, lean into, double down (when used as inspiration not poker), at the end of the day, the bottom line is.

**Filler openers:** "In today's fast-paced world", "In the ever-evolving landscape of", "It's important to note that", "Without further ado", "Let's dive in", "Buckle up", "Hot take:", "Unpopular opinion:", "Here's the thing".

**Filler closers:** "What are your thoughts?", "Drop a comment below", "Agree or disagree?", "Let me know in the comments", "Thoughts?", "Keep learning", "Stay tuned", "More to come".

---

## Rhythm and structure rules

**Break rule-of-three.** AI loves three-item lists in prose ("user empathy, strategy, and execution"). On a clean rewrite, allow at most one rule-of-three per post. If the original has multiple, collapse them to two-item phrases or expand one to four items.

**Vary sentence length.** Aim for a mix: one-word sentences, six-word sentences, twenty-word sentences. AI prose averages out around 14 words per sentence with very low variance. Break that.

**No negative parallelism in sequence.** "Nothing clever. Nothing pretty. Nothing that survives a code review." is an AI rhythm. Pick one negation, drop the others or rephrase.

**No clipped imperative chains.** "Fix it. Run it. Ship it." is an AI rhythm. Keep imperatives but vary them with full sentences.

**Copula avoidance is a tell.** AI overuses "X serves as Y" / "X stands as Y" / "X represents Y" to avoid plain "X is Y". Use "is".

---

## Structural template (one of three patterns)

The rewrite must follow one of these three structures. Pick the one that fits the draft.

**Pattern A — The Reversal.**
Line 1: A common belief, stated cleanly.
Line 2-3: Why it is wrong, with a specific example.
Body: What is actually true and how the writer knows.
Close: A single concrete next step, or a sentence that lands the point.

**Pattern B — The Story.**
Line 1: A specific moment ("Last Tuesday at 11pm I...").
Body: What happened, what it cost or saved, what was learned.
Close: The wider lesson stated in one or two sentences. Never moralized.

**Pattern C — The Hot Take.**
Line 1: A sharp claim that disagrees with the consensus.
Body: Three to five sentences of evidence or experience backing it.
Close: An invitation to disagree, but stated as confidence not question. ("Fight me on this" is banned. "I will keep saying this until someone proves me wrong" works.)

---

## Output format

When invoked for a first-pass rewrite, output in this order:

1. A diagnostic header titled `**What was making it sound AI:**` with 4 to 8 specific issues found in the draft. Quote the problem phrase in backticks.
2. A diagnostic header titled `**Rewrite:**` followed by the rewritten post in plain prose.
3. Hashtags on their own line at the bottom of the rewrite.

On follow-up edits (user asks "shorter", "cut the second paragraph", "swap word X"), output the edited post only. No diagnostic. No commentary. This is the surgical edit rule from the router.

---

## Hashtag selection

5 to 10 hashtags. Lowercase. Mix of:

- 1 or 2 broad professional tags (`#productmanagement`, `#marketing`, `#leadership`)
- 2 or 3 niche tags relevant to the post's topic (`#claudecode`, `#amazonpm`, `#growthmarketing`)
- 1 or 2 community tags if relevant (`#womenintech`, `#bootstrapped`, `#startups`)

Never tag a person or company without explicit permission from the user.

---

## When the draft is already good

If the input is already a strong LinkedIn post (under 400 words, no AI tells, has a hook, takes a side, has concrete details), say so honestly. Output a one-line note: `The draft already reads as a strong LinkedIn post. No rewrite needed. If you want a specific change, tell me what.` Do not invent issues to justify a rewrite. This is the explicit fix for the "find fault on a clean draft" failure mode.

---

## Example diagnostic

For a draft like "In today's fast-paced AI landscape, product managers must embrace continuous learning to unlock their full potential":

What was making it sound AI:
- `In today's fast-paced AI landscape` — banned filler opener.
- `embrace continuous learning` — Tier-1 LinkedIn-AI cliché.
- `unlock their full potential` — banned vocab (unlock).
- The whole sentence has zero specifics. No name, no number, no situation.
- Copula avoidance: `must embrace` instead of just "have to learn".

That is the level of specificity the diagnostic should hit. Vague feedback like "sounds a bit formal" is not useful.