# SIP re-INVITE: Hold and Resume Troubleshooting

## Purpose

This case documents a structured way to analyze a call that changes media state
through SIP re-INVITE during hold and resume.

## Typical Flow

```text
Endpoint A          PBX/SBC          Endpoint B
    |--- INVITE ------>|---------------->|
    |<-- 200 OK -------|<----------------|
    |--- ACK ----------|---------------->|
    |                  RTP               |
    |--- re-INVITE (hold) -------------->|
    |<-- 200 OK --------------------------|
    |--- ACK ---------------------------->|
    |--- re-INVITE (resume) ------------>|
    |<-- 200 OK --------------------------|
    |--- ACK ---------------------------->|
```

Actual systems may anchor or regenerate the dialog, so both call legs must be checked.

## SDP Checks

- Which side initiated the re-INVITE?
- Did the SDP use `a=sendonly`, `a=inactive` or another direction attribute?
- Did the connection address or media port change?
- Did the answering side return a compatible direction attribute?
- After resume, were the original bidirectional media parameters restored?

## Troubleshooting Method

1. Establish a baseline from the initial INVITE/200 OK offer-answer exchange.
2. Compare each subsequent SDP body field by field.
3. Track the negotiated direction independently on both call legs.
4. Confirm whether RTP stops, changes direction or moves to a new address and port.
5. Verify that ACK completes every re-INVITE transaction.
6. Correlate signaling timestamps with the user action and the media capture.

## Common Failure Patterns

- Hold succeeds, but resume retains `sendonly` or `inactive`.
- Signaling completes while RTP continues toward an obsolete address or port.
- An intermediary rewrites SDP differently on the two call legs.
- A second re-INVITE overlaps an unfinished transaction.

## Lesson Learned

Hold is not a single SIP message. It is a new offer-answer exchange that changes
the media contract, and resume is another exchange that must restore it correctly.
