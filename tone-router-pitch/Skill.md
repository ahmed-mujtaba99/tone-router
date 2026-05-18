---
name: tone-router-pitch
description: Rewriter for external pitch messages — recruiter outreach replies, cold DMs, podcast or event pitches, job application copy, sales-style cold emails for personal opportunities. Use when the tone-router has identified a draft as an external pitch, OR when the user explicitly says "this is a cold message", "pitch to a recruiter", "podcast pitch", "applying for X". Outputs a confident, proof-loaded, specific message that opens a door rather than closes it with vague enthusiasm.
---

# tone-router-pitch

Rewrites a draft into an external pitch. The recipient is someone outside the user's company, often someone the user has never met, and the message needs to do three things in under 200 words: establish credibility, make a specific ask, and stand out from the dozens of similar messages in the recipient's inbox that day.

This is the only one of the five sub-skills where being slightly louder about yourself is correct. Modesty in a cold pitch is wasted; the recipient does not know who you are, so it's on you to tell them.

---

## Hard rules

1. **First sentence is not "Hi, my name is".** The recipient can see your name. Use line one for something else.
2. **One concrete credential or proof point in the first three sentences.** A number, a result, a recognizable company, a specific tool, a specific outcome.
3. **Subject line (if email) must be specific to the recipient.** Not "Quick question" or "Hello". Format: `Subject: <6 to 10 words referencing what the recipient cares about>`.
4. **No em-dashes.**
5. **The ask is explicit and small.** "A 15-minute call this week" or "Five minutes to read the attached" or "A reply with your thoughts". Not "to discuss synergies" or "to explore opportunities".
6. **Length 80 to 180 words for an email, 50 to 120 for a DM-style pitch.**
7. **No false familiarity.** "I've been a huge fan of your work for years!" is banned unless the user actually has been, and even then, name the specific thing.

---

## Banned vocabulary

**Generic AI tells:** delve, tapestry, underscore, meticulous, showcase, intricate, leverage, navigate (figurative), landscape (figurative).

**Pitch-specific tells (these scream "template"):**
- "I hope this email finds you well"
- "I came across your profile and was impressed"
- "I've been following your work"
- "Your background really resonates with me"
- "I would love the opportunity to..."
- "I believe I would be a great fit because"
- "I'm a results-driven professional"
- "passionate about" (passion is shown, not claimed)
- "transformational", "disruptive", "innovative" applied to yourself
- "rockstar", "ninja", "guru" applied to yourself or anyone else
- "I noticed that <company> recently..." as an opener if it's based on a quick LinkedIn skim
- "synergies", "alignment", "opportunities"

**Hedges that kill confidence:**
- "I might be a fit" use "I think I'm a fit, here's why"
- "I was wondering if perhaps" use "I'd like to"
- "Sorry to take up your time" cut entirely
- "I know you're busy" cut entirely

---

## Structure

A pitch has four parts, in this order:

**1. The hook (line 1 to 2).** A specific reason for writing that is not "I want a job" or "I want to be on your podcast". Could be: a specific result they had that you noticed, a specific overlap in work, a referral, a question their public work raised for you.

**2. The credibility (lines 2 to 4).** Who you are and what you've done, expressed in concrete terms. The format that works:
"I'm a <role> at <company / context>. <One sentence with a specific number, scope, or result>. <One sentence with a specific tool, project, or domain>."

**3. The ask (lines 5 to 7).** The specific thing you want, in plain terms, with a small commitment. "A 20-minute call" not "a chance to chat". "A reply with your thoughts on X" not "your guidance".

**4. The exit (one line).** Make it easy for them to say no. "Totally understand if the timing isn't right." or "Happy to send the work first if that's easier." This is counter-intuitive but it raises response rates.

---

## Tone rules

**Confidence without bragging.** "I led a 12-person rebuild of our pricing engine" is confidence. "I am a transformational pricing leader" is bragging. The first is a fact. The second is a label.

**Specificity wins over polish.** A pitch that says "I run the catalog for a 300-SKU Amazon brand and built an in-house tool that scrapes BuyBox data" is much stronger than "I'm an experienced e-commerce product manager with deep Amazon expertise." Both could describe the same person. Only one gets a response.

**Show research, but don't perform it.** If you're pitching to a podcast host, referencing a specific episode is good. Listing five of their episodes is creepy. Pick one and use it as a hook.

**Don't open with flattery.** Flattery is filler. The recipient sees through it. Open with substance and let your respect for their work be implied by the fact that you're reaching out at all.

---

## Output format

First-pass rewrite outputs:

1. `**What was making this a weak pitch:**` 3 to 6 specific issues. Most common issues at this register: zero specifics, hedging, flattery opener, no clear ask, ask is too big.
2. `**Subject:** <subject line>` (if it's an email)
3. `**Rewrite:**` followed by the message body.

On follow-up edits, output the body only.

---

## Common pitch scenarios

**Replying to a recruiter who reached out.**
Don't say yes too fast. The reply asks one or two specific questions that shows you've looked into the role, signals interest without commitment, and proposes a time window if you want to take the call.

**Cold-pitching a podcast.**
Lead with the angle, not your bio. "I think you should do an episode on <specific topic> and here's why" works. "I'd love to be a guest on your show" does not.

**Cold DM to someone whose work you admire.**
Pick one specific question their work raised that you can't answer yourself. A real question, not "would love to pick your brain". Brain-picking is banned vocabulary.

**Job application cover letter / opening message.**
Three things in order: the role you're applying for and one sentence on why this specific company, two sentences on the most relevant specific result you've delivered, one sentence on the next step you'd like.

**Reaching out to a former colleague for an intro.**
Don't bury the ask in catch-up small talk. One line of genuine catch-up, then "the reason I'm writing is I'd love an intro to <person> for <reason>. Here's a forwardable paragraph."

---

## When the draft is already good

If the pitch is already specific, has a clean ask, no flattery, and no banned vocab, say so. Output: `This pitch reads strong. The hook works, the ask is clear, and the credibility is concrete. Send it.` Do not invent issues.
