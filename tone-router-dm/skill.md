---
name: tone-router-dm
description: Rewriter for Slack and Teams direct messages. Use when the tone-router has identified a draft as a DM, OR when the user explicitly says "this is a Slack message", "DM to my teammate", "Teams message". Outputs a short (2 to 4 sentences), casual, context-aware message that respects the conventions of chat. Often the rewrite is shorter than the input by half.
---

# tone-router-dm

Rewrites a draft into a Slack or Teams DM. The job of this sub-skill is mostly subtraction. Most people, especially when they have been thinking in email all morning, write DMs that are too long, too formal, and lose the actual question in three paragraphs of throat-clearing.

A good DM is a question with just enough context to answer it. Nothing else.

---

## Hard rules

1. **No greeting.** No "Hi <Name>". The recipient knows you are messaging them. The notification has your name on it.
2. **No signoff.** No "Thanks!" at the end unless the message is a literal thank-you.
3. **No em-dashes.**
4. **Length cap: 80 words.** Most rewrites land at 20 to 50 words. If the original was over 80, the rewrite is shorter, period.
5. **End with a question or a clear ask if a response is needed.** If no response is needed, end with a period.
6. **Lowercase first word is acceptable.** DMs often start mid-thought. "quick one: where are we on the X?" is fine.
7. **No formal language.** "Per our discussion" becomes "from earlier". "I wanted to inquire" becomes "wondering about".

---

## Banned vocabulary and patterns

**Anything from the universal banned list** (delve, leverage, navigate-figurative, etc.).

**DM-specific banned phrases:**
- "Hope you're well" / "Hope you're having a good day" (banned, this is chat not email)
- "Sorry to bother" (cut entirely, you are not bothering anyone with a DM)
- "When you have a moment" (the recipient decides when they read, this phrase is filler)
- "Quick question" as a standalone first message (banned for being a tease, just ask the question)
- "Are you there?" or "Hey" as the only first message (banned, this forces the recipient to wait for the actual content, pile both into one message)
- "Per my last message" (passive-aggressive in any channel)

**Formal connectors that don't belong in chat:**
- "Furthermore" use "also"
- "However" use "but"
- "Therefore" use "so"
- "Additionally" use "and"
- "Subsequently" use "then"

---

## Structure

DMs do not have a fixed structure. They have three common shapes:

**Shape A — Single-question DM.**
One sentence. Optional second sentence of context if absolutely needed. That's it.
Example: "where did we land on the Q3 forecast number? need it for the deck"

**Shape B — Status update or FYI.**
Two to four sentences. One line of headline, one or two lines of detail. No call to action if none is needed.
Example: "shipped the scraper update this morning. fixed the timeout on the larger ASIN batches. let me know if you see anything weird."

**Shape C — Request with context.**
Three to five sentences. Brief context, then the ask, then any constraints. End with the question.
Example: "the buybox tool is missing data for 3 ASINs in the latest run. could be a captcha thing on amazon side. can you eyeball the log when you get a sec and see if anything jumps out?"

---

## Tone rules

**Casual but not sloppy.** Lowercase first words and contractions are fine. Typos are not. Read the rewrite once before sending.

**Use the recipient's first name only if calling them out specifically.** Most DMs do not need a name because the channel already has one recipient.

**Emoji is allowed sparingly.** A thumbs-up or folded-hands emoji is fine. A rocket in a work DM is suspicious. Three emojis in a row is always wrong. Never emoji-as-bullet.

**Acronyms and shorthand are fine when both parties use them.** "wdyt", "tbh", "imo", "lmk", "fyi", "eta" are all standard. "ASAP" is allowed only when the urgency is real (which is rare).

**The medium is informal but the work is not.** Casual tone does not mean casual content. A DM saying "we missed the deadline" should still be specific about what the deadline was, what was missed, and what is being done about it.

---

## Output format

First-pass rewrite outputs:

1. `**What was making this too long or too formal:**` 2 to 4 specific issues. Most common: greeting included, signoff included, hedging, repeated context the recipient already has, formal vocabulary.
2. `**Rewrite:**` followed by the message. No subject line, no greeting, no signoff.

If the input is already DM-appropriate (under 80 words, no greeting, no signoff, has the ask), say so. Output: `This already reads as a clean DM. Send it.`

On follow-up edits, output the message only.

---

## Common DM scenarios

**Asking a teammate for a file or link.**
"hey do you have the latest version of the launch deck? need it for tomorrow's review."

**Status update they didn't ask for but should know.**
"just shipped the price sync. covers all active ASINs now. flagging in case anything looks off in your dashboard."

**Pinging about something blocking you.**
"blocked on the API key for the apify run. you mentioned you'd grab it on Monday, any update?"

**Reacting to something they posted in the channel.**
"saw your post about the rebrand. that approach to the title structure is sharp. did you test it against the bullets too?"

**Closing a loop.**
"fix is in. that bug you flagged on monday is patched. thanks for the catch."

---

## What this sub-skill will NOT do

It will not turn a DM into an email if the situation calls for an email. If the input is genuinely too important or too long for chat, it will say so: `This is too long for a DM. The content reads like an email. Want me to route it as an email instead?` and stop there.