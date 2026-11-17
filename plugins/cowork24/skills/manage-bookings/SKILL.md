---
name: manage-bookings
description: Show and cancel the user's own bookings on cowork24.ch. Use when the user asks about their cowork24 bookings or reservations, wants to know the status of a booking request, asks what they have booked next, or wants to cancel a cowork24 booking.
---

# Manage cowork24 bookings

The user's own bookings live behind the `cowork24-account` connector. It needs a one-time
sign-in with the user's cowork24 account. Searching and pricing do not need it.

## Steps

1. **Check the connection.** If the `cowork24-account` tools are not available, tell the
   user to connect "cowork24-account" in their connector settings and sign in with their
   cowork24 email and password. People who only ever signed in to cowork24.ch with Google or
   Apple have no password there; point them to their bookings at
   https://www.cowork24.ch/inbox/orders instead.

2. **List with `list_my_bookings`.** `filter` is `upcoming` (default), `past` or `all`.
   Show space, dates in local time, status and total. Use the status wording the tool
   returns.

3. **Cancel only on request, in two calls.**
   - Call `cancel_booking` with the `transactionId` and `confirm: false`. It restates the
     booking.
   - Show that to the user and ask whether to cancel this exact booking.
   - Only after an explicit yes, call it again with `confirm: true`.

## Rules

- Customers can cancel a request that the host has not accepted yet. A booking that is
  already confirmed and paid usually cannot be cancelled here. When the tool refuses, say so
  and send the user to the booking's page on cowork24.ch or to support@cowork24.ch. Do not
  retry and do not promise a refund.
- Never cancel more than one booking per confirmation.
- Use `cowork24-account` only for these two tools. For searching, details, availability and
  prices use the `cowork24` connector.
- Answer in the user's language.
