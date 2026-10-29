---
name: kairos-quote-reviver
description: Revive a quote that has gone quiet. Use when the user has sent a quote or estimate and hasn't heard back, wants a follow-up message for a pending quote, or wants a systematic way to chase open quotes instead of letting them die in the inbox.
---

# Stale Quote Reviver

Sent quotes die in inboxes because follow-up is nobody's system.
This skill runs a short, polite 3-touch follow-up sequence for one
quote at a time: a check-in, a value note, and a choice-close. Every
message is a draft — the user reviews and sends each one themselves.

## How to run it

1. Gather the quote details from the user (ask only for what's
   missing — never guess a value):
   - `customerName` — who the quote went to
   - `senderName` and `businessName` — the sign-off
   - `jobDescription` — the work, in a few words
   - `amount` and `currency` (USD, CAD, GBP, EUR, AUD)
   - `sentDaysAgo` — how long ago the quote was sent
   - optional: `tone` (friendly / professional / direct) and
     `validUntil` (a free-text validity line, e.g. "October 15")
2. Call `kairos_quote_reviver_plan` with those details. It returns
   the full drafted cadence plus a `state` value. Show the user the
   touch 1 draft and let them send it when ready.
3. After each touch, ask what happened and call
   `kairos_quote_reviver_next` with the `state` from the previous
   result (pass it back unchanged) and the outcome:
   - `no_reply` — returns the next drafted touch, or closes the
     sequence after touch 3
   - `replied_interested` — the sequence pauses; the user takes the
     conversation from here
   - `won` / `replied_declined` — closes the sequence with a polite
     closing draft

## Presenting results

Relay drafts exactly as the tool returns them — the user edits
before sending. Mention the cadence timing (today, +3 days, +7
days) so the user can plan the sends.

## Hard rules

- **Drafts only.** Never send a message on the user's behalf, and
  never claim a message was sent.
- **Never offer a discount, a price change, or different terms** —
  not in a draft, not in chat. If a customer asks for different
  terms, that's the user's own decision to make in their own words.
- **Estimates are estimates.** If you mention recovery figures,
  use only the estimate the tool returns, with its ESTIMATE label
  attached. Never promise a customer will reply or a quote will be
  won.
- **Never invent quote details.** Amounts, dates and names come
  from the user, not from you.
- If a tool call errors (expired or invalid state), say so plainly
  and offer to start a fresh sequence — don't paper over it.
