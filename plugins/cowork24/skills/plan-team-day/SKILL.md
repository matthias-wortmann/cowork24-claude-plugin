---
name: plan-team-day
description: Plan a team day, workshop, offsite or client meeting in a space from cowork24.ch and compare options by exact total cost. Use when the user needs a meeting room or workspace for a group, mentions an offsite, workshop, team day, board meeting or client meeting in Switzerland, or wants venue options for a given date and headcount.
---

# Plan a team day on cowork24

The result is a short comparison of real, available rooms with exact totals, and one
recommendation. All data comes from the `cowork24` connector.

## Steps

1. **Collect the brief.** City, date, start and end time, number of people. Budget and
   must-haves (screen, whiteboard, catering, step-free access) are optional. Ask once, for
   everything that is missing, then proceed.

2. **Search.** Call `search_spaces` with the city, `category: "meeting room"`, the date
   window as `checkIn` / `checkOut` and the headcount as `capacity`. If that returns fewer
   than three rooms, search again without the date and without the capacity, and check the
   candidates one by one in the next step.

3. **Check the best three or four.** For each candidate:
   - `get_space_details` for amenities, booking mode and cancellation terms.
   - `check_availability` for the exact window.
   - `get_price_quote` for the exact total.
   Drop any room that is not free. If none is free, show the open slots the tools returned
   for the closest fits.

4. **Compare.** One table: room (linked), area, total for the window in CHF, booking mode,
   the must-haves it meets, cancellation terms. Mark a must-have as "not listed" when the
   host does not mention it. That is different from "no".

5. **Recommend one** and say why in a sentence: fit for the group, total cost, how quickly
   it can be confirmed.

6. **Hand over to booking.** When the user picks a room, follow the `book-space` skill from
   the summary step.

## Rules

- Room size: cowork24 listings do not carry a reliable "fits N people" field. Use what the
  title and description say. If they do not say, tell the user to confirm the room size with
  the host on the listing page rather than guessing.
- Totals come from `get_price_quote` only. Do not multiply an hourly rate yourself.
- Request-to-book rooms need the host to accept. For a date less than two days away, prefer
  instant-book rooms and say why.
- Do not add travel times, catering or anything else the tools did not return, unless the
  user asks and you mark it clearly as not coming from cowork24.
- Answer in the user's language.
