---
name: find-workspace
description: Find and compare workspaces on cowork24.ch, with live prices. Use when the user wants a coworking space, day pass, desk, private office, meeting room or airport lounge, asks where to work in a Swiss city such as Zürich, Bern, Basel or Geneva, asks what a space on cowork24 costs or includes, or pastes a cowork24.ch link.
---

# Find a workspace on cowork24

cowork24.ch is a Swiss marketplace for coworking desks, private offices and meeting rooms in
Swiss cities, plus airport lounges in Switzerland and at international airports. Everything
about inventory, prices and availability comes from the `cowork24` connector. Never answer
from memory.

## Steps

1. **Work out what is being asked.** You need a place. Type of space, date, group size and
   budget help but are optional. If only the place is known, search first and refine from the
   results. Ask a question only when there is no place at all.

2. **Search with `search_spaces`.**
   - `location`: the city, town or airport as the user said it.
   - `category`: "coworking desk", "private office", "meeting room" or "airport lounge" when
     the user named a type. Leave it out for a general "coworking" request; it would narrow
     the results too far.
   - `maxPrice`: CHF per unit, only when the user gave a budget.
   - `checkIn` / `checkOut`: only when the user gave a date. `capacity` filters only together
     with a date range.
   - Pass times the way the user said them, without a timezone. They are read as local time
     at the space.

3. **Present a shortlist of three to five.** For each: name as a link to its cowork24.ch
   page, area, price with its unit exactly as returned, and whether it is instant book or
   request to book. Say how many were found in total. If the result renders as a map with
   cards, do not repeat every card in text; add only what helps the user choose.

4. **Go deeper on request.** `get_space_details` accepts a listing id, a cowork24.ch URL or
   the exact title. Report the amenities the host lists, the price, the booking mode and the
   cancellation terms.

5. **Offer the next step.** Checking a date, an exact price for a time window, or preparing
   the booking. The `book-space` skill covers those.

## Rules

- When a search returns nothing, say that cowork24 has no spaces there. Do not present
  spaces from another city as if they answered the question. Offering a nearby city is fine
  when it is named as such.
- Prices are in CHF and belong to a unit (hour, day, month). Never convert one unit into
  another and never estimate a total. An exact total comes from `get_price_quote`.
- Report only amenities, opening times and terms that the tools return.
- Monthly desks and airport lounges have no calendar. A date filter can hide them, so search
  without dates when the user wants one of those.
- Answer in the user's language. cowork24 serves German, French and English speakers.
