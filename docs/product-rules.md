# Parcelo — product rules

Training artifact for the course «AI-інструменти для QA», module M4. Fictional product,
fictional rules. Numbering matches the status specification used in the course materials
(case C34), so that a rule can be referred to by its number on camera.

## Status specification

1. Statuses: created → picked_up → in_transit → at_local_hub → out_for_delivery →
   delivered / delivery_failed / returned_to_sender
2. Standard delivery SLA is 3 working days from `picked_up`; once it is exceeded, the
   shipment is automatically marked "delayed"
3. At most 3 delivery attempts; after the 3rd failed attempt the parcel is returned to sender
4. For international shipments, the status "customs_hold" may appear between `in_transit` and
   `at_local_hub`; it stops the SLA timer indefinitely until customs clearance is completed
5. The recipient can reschedule delivery only while the status is `out_for_delivery`, at most
   twice
6. A weight or dimension mismatch at the hub triggers "on_hold_verification": the sender must
   confirm within 48 hours, otherwise the parcel is returned
7. The delivery address can be changed only before `out_for_delivery`; later a new shipment is
   required

## How status is shown on the page

8. The current status is rendered in the element with `data-testid="status-label"`
9. The delay badge is rendered in the element with `data-testid="delay-badge"` and is shown
   only when the status is marked "delayed" under rule 2

## What this means for parcel UA123456789

The parcel is international, was picked up 12 working days ago and has been in `customs_hold`
since day 4. Under rule 4 the SLA timer has been stopped since it entered customs, so under
rule 2 it must not be marked "delayed", and under rule 9 the delay badge must not be shown.

The page currently shows the badge anyway. This contradicts the rules above and is an
intentional defect of this training environment. Do not fix it.
