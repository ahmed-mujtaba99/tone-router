---
name: tone-router
description: Channel-aware rewriting router for Product Managers, marketing, and ops. Use whenever the user types "/rewrite", "/humanize", "/humanise", "/tone", "fix this tone", "make this sound human", "rewrite this", or pastes any draft (LinkedIn post, email, Teams/Slack message, recruiter pitch, executive update) and asks for a tone pass. This skill is the ROUTER. It does not rewrite anything itself. It identifies which channel the text is for, then hands off to the matching sub-skill. Sub-skills live alongside this skill, one per channel. Trigger this skill before any sub-skill — never invoke a sub-skill directly unless the user explicitly named the channel in their message (e.g. "rewrite this as a LinkedIn post"). If the channel cannot be inferred from the text, ask the user once before routing.
---

# Tone Router

The single entry point for every rewrite request. Owns the triage decision. Does not rewrite text itself.

The problem this skill solves: one humanizer cannot do five jobs. A LinkedIn post wants opinion and punch. An email to a VP wants deference and a clean ask. A Slack DM wants two sentences. The wrong tone in the wrong channel does more damage than AI-flavored prose ever could. This router picks the right downstream skill so the rewrite matches the channel.

This skill is designed for Product Managers, marketing managers, and ops leads, anyone who writes across five very different audiences in a single day.

---

## How invocation works

The user triggers this skill by:

- Typing `/rewrite`, `/humanize`, `/humanise`, `/tone` (any spelling)
- Pasting a draft and saying "fix this", "make this sound human", "tone pass", "rewrite this for me"
- Saying "make this sound less AI" or "make this sound like me"

When triggered, this skill does ONE of three things, in this order:

1. **Channel is obvious from the text or the request.** Route silently. Do not ask. Examples: text ends in hashtags, route to LinkedIn. Text starts with "Hi [Name]," and ends with "Best regards," route to one of the email sub-skills based on who the recipient is. Text is two lines with no greeting and references a teammate by first name, route to DM.

2. **Channel is ambiguous.** Ask the user once with `ask_user_input_v0`, single-select, the five channel options below. Then route.

3. **No text provided yet, just the trigger word.** Ask the user to paste the draft, then ask the channel if it is not obvious from the paste.

---

## The five channels and their sub-skills

| Channel | When to route here | Sub-skill name |
|---|---|---|
| LinkedIn post | Hashtags at the end, opinionated, hook-first, written for an audience the user does not personally know | `tone-router-linkedin` |
| Email up | Recipient is VP, director, executive, senior client, or external senior stakeholder. Tone needs structure, a clean ask, and no strong opinion presented as fact | `tone-router-email-up` |
| Email lateral | Recipient is a peer manager, counterpart at another team, vendor, or anyone at roughly the same level. Tone is direct, collaborative, no deference layer | `tone-router-email-lateral` |
| Teams / Slack DM | Short message, single thread, internal teammate. Tone is casual, two to four sentences, often ends in a question | `tone-router-dm` |
| External pitch | Recruiter outreach, podcast or event pitch, job application copy, cold message to someone outside the company. Tone is confident, positioning loud, concrete proof points | `tone-router-pitch` |

---

## Channel detection signals (use these in order)

Before asking the user, scan the draft for these. If two or more signals match a single channel, route silently.

### LinkedIn post signals

- Hashtags at the end of the draft
- Opens with a hook line that is not addressed to a named person
- Uses "I" or first-person reflection
- 100 to 400 words, no signoff, no "Hi [Name]"
- Themes are career, industry takes, personal wins, lessons learned, hot takes on tools or methodology

### Email up signals

- Opens with "Hi [Name]," or "Dear [Name]," where the named person holds a senior title
- Mentions deliverables, sign-off, approval, review, alignment, escalation
- Has a clear ask buried somewhere in the body
- Ends with "Best regards," "Thanks," "Kind regards," and the user's name
- Vocabulary leans formal: "circling back", "wanted to flag", "for your awareness", "as discussed"

### Email lateral signals

- Opens with "Hi [first name]" where the name is a peer or vendor contact
- Practical, transactional content (file sharing, status updates, joint problem-solving)
- Signoff is light: "Thanks", "Cheers", no "Best regards"
- Often references a shared artifact (doc, spreadsheet, ticket, channel)

### Teams / Slack DM signals

- Under 80 words
- Names a teammate by first name only
- References internal artifacts (a board, a ticket, a file, a tool)
- Often ends with a question or "wdyt", "thoughts?", "lmk"
- No greeting, no signoff

### External pitch signals

- Addressed to a recruiter, hiring manager, podcast host, event organizer, or cold prospect
- Positions the user with a clear professional identity and concrete proof points
- Asks for a meeting, intro, application review, speaking slot, or reply
- Often contains a link, a portfolio reference, or a one-line credential

---

## Routing workflow

1. Read the draft (or note that none was provided).
2. Run channel detection above.
3. If two-plus signals match one channel, route silently. Tell the user one line: "Routing through the [channel name] sub-skill."
4. If signals are mixed or absent, ask via ask_user_input_v0 with question "Which channel is this for?" and options [LinkedIn post, Email (up), Email (lateral), Teams/Slack DM, External pitch].
5. Once channel is known, load the matching sub-skill and apply its rules.
6. Deliver in the format that sub-skill specifies.

---

## What this skill does NOT do

- Does not rewrite text. Rewriting belongs to the sub-skills.
- Does not run a diagnostic. The sub-skills decide whether a diagnostic is warranted.
- Does not enforce a single tone across channels. The whole point is that tone differs by channel.
- Does not re-route mid-conversation unless the user asks. Once a draft is routed to LinkedIn, follow-up edits stay in LinkedIn mode unless the user says "actually make this a DM instead."

---

## Behavior on follow-up turns (important)

When the user replies after a rewrite with a small edit ("shorter", "cut the second paragraph", "swap word X for something else"), apply the edit directly. Do NOT re-run the sub-skill's full diagnostic. The diagnostic is for first-pass rewrites only.

This is the fix for the common loop where every edit re-triggers a fresh round of "what was making it sound AI." A draft that already passed through a sub-skill is treated as clean. Edits are surgical, not regenerative.

---

## Sub-skill contract

Every sub-skill in this family MUST:

- Live at `/skills/user/tone-router-<channel>/SKILL.md` (or the equivalent path in the user's skill library)
- Have its own description block that triggers only when the channel is named explicitly OR when this router hands off
- Specify its own output format (diagnostic plus rewrite, or rewrite-only, depending on channel)
- Encode that channel's formatting rules
- Default to NOT showing a diagnostic on follow-up edits

---

## Universal rules (every sub-skill inherits these)

These are non-negotiable and apply to every channel:

1. No em-dashes. Replace with comma, period, or colon depending on function.
2. Straight quotes only, not curly.
3. No decorative emojis unless the channel sub-skill explicitly allows them.
4. No Tier-1 AI vocabulary: delve, tapestry, underscore, meticulous, showcase, intricate, multifaceted, garner, testament, realm (figurative), navigate (figurative), landscape (figurative), embark, unlock, unleash, unravel, beacon, bastion.
5. No banned filler phrases: "in today's fast-paced world", "in the ever-evolving landscape", "it's important to note", "at the heart of", "without further ado", "in conclusion", "game-changer", "let's dive in".
6. Take a side when the original hedges, EXCEPT in email-up where deference outranks opinion.
7. Use the user's name and role only when they have provided them. Do not invent biographical details.

---

## What the user provides (optional context)

The router and its sub-skills work better when the user has shared, in a prior conversation or in their profile:

- Their role and function (e.g. Product Manager, marketing lead)
- The team or product they work on
- Names of frequent collaborators (so the router can map them to "peer", "manager", "report")
- A voice sample of their own past writing

If none of this is available, the sub-skills default to a neutral professional voice and ask the user for any one concrete detail before publishing.

---

## When to ship updates to this skill

This router is stable. If a sub-skill needs a rule change (e.g. LinkedIn formatting preference flips, or a new banned phrase enters the corporate lexicon), update the sub-skill, not the router. The router should change only when:

- A new channel is added or removed
- The detection signals stop catching real-world cases
- The follow-up-turn behavior needs tightening

Keep this file under 250 lines. It is a router, not a style guide.
