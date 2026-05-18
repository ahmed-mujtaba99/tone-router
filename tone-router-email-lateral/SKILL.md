---
name: tone-router-email-lateral
description: Email rewriter for messages going to peers, counterparts at other teams, vendor contacts, or anyone roughly at the user's level. Use when the tone-router has identified a draft as a lateral email, OR when the user explicitly says "this is for a peer / brand manager / counterpart". Outputs a direct, collaborative, low-formality email that gets to the point without the deference tax of email-up.
---

# tone-router-email-lateral

Rewrites a draft into an email for a peer. Peer-to-peer email is the most under-served format because most "professional email" advice is calibrated for upward writing. Peers do not need hedging, do not need elaborate greetings, and resent both.

This sub-skill is roughly halfway between email-up (formal, structured, deferential) and the DM sub-skill (short, casual, ends in a question). It keeps email's structure but drops the formality tax.

---

## Hard rules

1. **Subject line is required and can be casual.** Format: `Subject: <4 to 8 words>`. Casual is fine ("Re: pricing on the new SKUs", "Quick one on the launch deck"). Vague is not ("FYI", "Hi", "Question").
2. **No em-dashes.**
3. **Greeting is one word.** `Hi <Name>,` or `Hey <Name>,`. Not `Dear`, not `Hello`.
4. **No deference filler.** "I hope this finds you well", "I hope you're having a good week", "Sorry to bother you" all get cut.
5. **Get to the point in the first sentence.** Same as email-up, but the framing is collaborative not hierarchical.
6. **Length 30 to 150 words.** Peer emails are shorter than upward emails by design.
7. **Signoff is light.** `Thanks,` or `Cheers,` followed by the name. Not `Best regards`. Not `Kind regards`.

---

## Banned vocabulary

**Generic AI tells:** same as the router universal list (delve, tapestry, underscore, etc.).

**Lateral-email-specific banned phrases:**
- "Just following up" (use "Following up" if needed at all)
- "Per my last email" (passive-aggressive, never used between peers in good faith)
- "I wanted to reach out" (just reach out)
- "I hope this email finds you well" (banned)
- "I'm reaching out because" (just say what you're emailing about)
- "Please advise" (corporate code for "tell me what to do", peers don't write this to each other)
- "Kindly" (overly formal, often used as a softener that lands as condescension)
- "Touch base" (use "catch up" or just propose the meeting)
- "Loop in" (acceptable in DMs, slightly off in email — use "include" or "add")

**Hedging that wastes peer time:**
- "I was thinking maybe we could" use "Want to..."
- "If you have a chance, could you possibly" use "Could you..."
- "Sorry to ask, but" cut entirely.

---

## Structure

Peer emails have a looser structure than upward emails, but they still need a shape:

**1. Greeting.** `Hi <Name>,` or `Hey <Name>,`.

**2. The point.** What this email is about, in one or two sentences. Often a request, an FYI, a question, or a forward-with-context.

**3. The detail.** Two to four sentences with the specifics. Numbers, links, file names, dates. Concrete over abstract.

**4. The next step.** What you need back, by when, or what you'll do next. One sentence.

**5. Signoff.** `Thanks,` or `Cheers,` and the name.

Some peer emails are two sentences total ("Hey, can you send me the latest deck? Thanks"). That is fine. Do not pad short emails to look more professional.

---

## Tone rules

**Collaborative, not transactional.** Even when asking a peer for something, frame it as joint work, not a request from a customer. "Can you send me the file" is fine. "Please send me the file at your earliest convenience" sounds like you forgot they're a colleague.

**Disagree directly when needed.** Peers can hear "I think the other approach works better, and here's why" without it damaging the relationship. Hedging disagreement with peers ("I might be wrong but maybe we could possibly consider...") reads as either passive-aggressive or evasive.

**Humor is okay in small doses.** A short joke or self-deprecating line is fine in peer email. Save it for the close, not the open. Never use humor about a third person.

**Names matter.** Peers know each other. Using their first name in the body of the email (not just the greeting) makes the email feel less templated. "Hey Maria, I think you're right about the pricing tier."

---

## Output format

First-pass rewrite outputs:

1. `**What was making this off for a peer:**` 2 to 5 specific issues. Most common issues at this register are: too much formality, missing specifics, buried ask, unnecessary hedging.
2. `**Subject:** <subject>`
3. `**Rewrite:**` followed by the body.

On follow-up edits, output the body only. No diagnostic.

---

## Common peer-email scenarios

**Forwarding a thread with context.** "Hi <Name>, forwarding the below from <Person>. <One sentence on what's going on and what you want from the recipient>. Thanks, <Name>"

**Asking for status on something they owe you.** Skip the "just checking in" opener entirely. "Hey <Name>, where are we on <thing>? I need it for <reason> by <date>."

**Disagreeing on a decision in the thread.** "Hey <Name>, I see the case for X but I'd push back. <Two sentences of reasoning>. Open to talking it through if useful."

**Sharing a win.** "Hey <Name>, wanted you to see this: <concrete result>. Thanks for <specific thing they did>."

---

## When the draft is already good

If the draft is already at the right register for a peer (direct, no padding, clear ask), say so. Do not invent issues. Output: `This reads right for a peer email. Send as-is.` Do not rewrite to look busy.
