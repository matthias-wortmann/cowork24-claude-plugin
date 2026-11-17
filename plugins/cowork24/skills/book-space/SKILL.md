---
name: book-space
description: Check availability, get an exact price and prepare a booking for a space on cowork24.ch. Use when the user wants to book or reserve a desk, office, meeting room or lounge on cowork24, asks whether a space is free at a given time, asks what a booking will cost in total, or wants a checkout link.
---

# Book a space on cowork24

A booking is completed and paid for on cowork24.ch. This skill gets the user to the checkout
page with the right space, time and price. It never takes payment and never creates a
reservation on its own.

## Steps

1. **Identify the space.** A listing id, a cowork24.ch URL or the exact title all work as
   `listingId`. If the user has not chosen a space yet, use the `find-workspace` skill first.

2. **Fix the time window.** You need a start and an end.
   - Pass times without a timezone ("2026-06-15T09:00"). They mean local time at the space.
   - The end is exclusive. One whole day is start `2026-06-15`, end `2026-06-16`.
   - Resolve relative dates ("next Wednesday") to a calendar date and state that date back to
     the user.

3. **Check availability with `check_availability`.** Pass `seats` when more than one person
   is booking.
   - If the window is free, continue.
   - If it is not, list the open slots the tool returned and let the user pick. Never invent
     a slot, and do not present closed days as bookable.
   - Some spaces (monthly desks, lounges) are sold from stock and have no time slots. The
     tool says so. That is not "unavailable".

4. **Get the price with `get_price_quote`.** Show the line items and the total exactly as
   returned. If the space has price variants, name them and pass the chosen one as
   `priceVariantName`.

5. **Show the summary with `prepare_booking` and `confirm: false`.** It restates the space,
   dates, seats, total, booking mode and cancellation terms.

6. **Wait for an explicit yes.** Only when the user has confirmed this exact space, time and
   price, call `prepare_booking` again with `confirm: true` and hand over the checkout link.

7. **Explain what happens next.** The user opens the link, signs in on cowork24.ch and
   completes the booking there.
   - Instant book: the payment confirms the booking.
   - Request to book: the host accepts or declines first.

## Rules

- Never ask for card details and never claim that a booking or payment has been made. Until
  the user finishes checkout on cowork24.ch, nothing is reserved.
- Never set `confirm: true` on an assumption. A changed date, seat count or space needs a
  new summary and a new yes.
- If the tool rejects a window because the start is too soon, the host needs lead time.
  Offer the earliest start the tool allows.
- Cancellation terms come from the tools. Do not paraphrase them into something more
  generous.
- Answer in the user's language.
