# Intent: Results-ready notification (PRD N-17)

Sources: `inputs/01-approved-prd.md` (approved 2026-09-18), `inputs/02-current-meeting.md` (discovery notes, 2026-09-20). `inputs/03-superseded-request.md` (2026-08-02) is superseded by PRD N-17: it is historical context only and approves nothing in this intent.

## Problem

- **P-1** The fictional clinic receives avoidable calls from patients checking whether their results are ready. (01: "The fictional clinic receives avoidable calls from patients checking whether results are ready.")

## Proposed outcome

- **I-1** Notify the patient when a result is ready for their review in the existing authenticated portal. (01: "Notify the patient when a result is ready for their review in the existing authenticated portal.")
- **I-2** "Ready" means a doctor has reviewed **and** released the result. A finished laboratory upload alone never makes a result ready or a notification eligible. (01: "A doctor must review and release the result before any notification is eligible."; 02, product owner: "'Ready' must not mean that the laboratory upload merely finished.")
- **I-3** The notification only says that an update is available and directs the patient to the existing authenticated portal. (01)

### How success will be observed

- **S-1** Status-only calls ("is my result ready?") fall compared with a measured baseline. They are counted separately from clinical questions. (01: "Measure reduction in results-status calls"; 02, support lead: "count status-only calls separately from clinical questions; compare against a measured baseline.")
- **S-2** Delivery failures are measured and handled without sending duplicate patient messages. (01: "Measure reduction in results-status calls and delivery failures.")
- **S-3** No numerical target is approved. The baseline and any target will be agreed during discovery. (01: "The baseline and numerical target will be agreed during discovery; none is approved yet.") The superseded request's "90% call reduction in one week" is not adopted.

## Affected users and systems

- **U-1** Patients: receive the update-available notification and view the result in the existing authenticated portal. (01)
- **SYS-1** Existing authenticated patient portal and its existing result route. (01: "Use the existing portal result route."; 02, engineering lead: "the existing portal path is adequate.")
- **SYS-2** Notification delivery and its notification/operational logs, with the channel still to be decided (OPEN-1). (01: "handle delivery failures without duplicate patient messages"; 02, privacy owner: "no sensitive content in messages or operational logs.")

In scope: the existing portal result route, duplicate prevention for the same released result version, and delivery-failure handling.

## Out of scope

Excluded from this approved scope:

- **X-1** Portal redesign. (01)
- **X-2** Appointment scheduling. (01)
- **X-3** Clinical interpretation. (01)
- **X-4** Notifying third parties. (01) The referring doctor is not decided here; it is the separate open question OPEN-2.
- **X-5** A new or rebuilt patient dashboard. It is a separate project. (02, engineering lead: "A new patient dashboard is a separate project.")

## Constraints

- **C-1** Review before notification: no notification is eligible until a doctor has reviewed and released the result. (01, 02)
- **C-2** No clinical detail: no diagnosis, test result, clinical measurement or treatment detail in the message or in notification and operational logs. (01; 02, privacy owner: "no sensitive content in messages or operational logs.")
- **C-3** Authenticated access only: results are viewed in the existing authenticated portal. No attached results and no public result link. (01)
- **C-4** No duplicates: avoid duplicate notifications for the same released result version, and handle delivery failures without duplicate patient messages. (01)
- **C-5** Notifying third parties is excluded, and notification to the referring doctor is not approved pending OPEN-2. (01: "notifying third parties [is] outside this approved scope"; 02, clinical owner: "do not infer approval for referring-doctor notifications from the old request.")

## Open questions

- **OPEN-1** Which channel (SMS, email, portal push)? Owners: **product owner and privacy owner**, to decide after the consent/delivery review. (01; 02, privacy owner: "Consent and the actual channel are still under review.") Not decided here.
- **OPEN-2** May the referring doctor be notified? Owners: **clinical owner and privacy owner**, who must decide recipient authorization. (01: "It is not approved by this PRD.") Not approved here.
- **OPEN-3** What are the measured baseline and the numerical target? Owner: **product owner**, the owner of PRD N-17, to agree during discovery. (01: "Owner: product owner."; "The baseline and numerical target will be agreed during discovery; none is approved yet.") No target is set in this intent.

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
