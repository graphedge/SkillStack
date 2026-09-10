## [PUBLIC] Customer fill-in

**Invoke (example only — not a skill):** `-ex @state-management`

**NON-CANON.** Example of what a customer would put in this slot. Replace with your own rules. MUST NOT treat this sample as Board or writing canon.

Example (a ticket bot):
- Every skill call includes `ticket_id` and `prior` JSON.
- Return the full `next` JSON; do not assume the next step remembers chat.
- MUST NOT read Slack, a database, or env vars that were not named as inputs.

