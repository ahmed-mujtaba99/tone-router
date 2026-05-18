# tone-router

A Claude skill that routes rewrite requests to channel-specific sub-skills. One trigger word, five tones.

Most "humanize this" prompts treat every piece of writing the same way. They strip em-dashes, vary sentence length, kill a few AI buzzwords, and hand the same prose back to you whether you were writing a LinkedIn post or a Slack DM to your teammate. That is the wrong shape of the problem.

A LinkedIn post wants opinion, punch, and hashtags. An email to your director wants deference and a clean ask. A Slack DM wants two sentences and a question. tone-router triages your draft by channel and hands it to a sub-skill tuned for that context.

## For who

Product Managers, marketing managers, and ops leads who write across five very different audiences in a single day.

## The five channels

| Channel | Tone | Status |
|---|---|---|
| LinkedIn post | Opinionated, hook-first, hashtags at the end | Live |
| Email up | Deferential, structured, ask-first | Live |
| Email lateral | Direct, collaborative, low formality | Live |
| Teams / Slack DM | Short, casual, ends in a question | Live |
| External pitch | Confident, positioning loud, proof points | Live |

## Install

1. Open Claude.ai
2. Go to your skills library
3. Create a new skill named `tone-router`
4. Paste the contents of [`tone-router/SKILL.md`](./tone-router/SKILL.md)
5. Save

Repeat the same for each sub-skill you want to install, using the matching folder in this repo.

## Trigger words

The router activates on any of:

- `/rewrite`
- `/humanize` or `/humanise`
- `/tone`
- Phrases like "fix this tone", "make this sound human", "rewrite this for me"

You can also paste a draft with no trigger word and the skill will pick it up.

## How routing works

The router scans your draft for signals. Hashtags at the bottom plus no greeting plus first-person opinion equals LinkedIn, route silent. "Hi [Senior Name]," at the top plus a buried ask plus "Best regards" equals email up, route silent. Signals are mixed and it asks you once with a quick channel picker.

Once a draft is routed, follow-up edits stay in that channel and are surgical, not regenerative. Ask for "shorter" and you get shorter. No fresh diagnostic. This is the fix for the most common humanizer failure mode.

## Repo structure