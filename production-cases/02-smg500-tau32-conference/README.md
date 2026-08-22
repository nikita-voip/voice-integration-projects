# SMG-500 and TAU-32 Conference Investigation

## Symptom

A conference scenario involving an SMG-500 and a TAU-32 did not behave as expected.
The gateway and conference service initially appeared to be the likely failure point.

## Troubleshooting Approach

The call was separated into signaling, media and analog-side behavior:

1. Verify that each conference leg is established.
2. Confirm SIP dialog state and disconnect reasons on the SMG-500.
3. Check RTP in both directions for every established leg.
4. Compare the event timing with FXO seizure, answer and release behavior.
5. Inspect TAU-side port logic instead of assuming that the conference bridge failed.

## Finding

The conference function on the SMG-500 was not the root cause. The observed behavior
was associated with FXO/TAU logic in the surrounding call scenario.

## Engineering Takeaway

Conference problems are multi-leg problems. A healthy bridge cannot compensate for
incorrect seizure, supervision or release behavior on an analog gateway leg. Verify
each boundary independently before changing the conference configuration.

## Evidence to Preserve During a Similar Investigation

- A timestamped SIP ladder for all legs.
- RTP stream statistics per leg.
- FXO port events and supervision mode.
- TAU-32 port configuration with sensitive values removed.
- A clear expected-versus-observed call-flow diagram.

> Product names are retained for technical context; deployment-specific data is omitted.
