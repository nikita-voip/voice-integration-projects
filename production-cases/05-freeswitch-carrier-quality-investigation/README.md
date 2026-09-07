# FreeSWITCH Carrier Quality Investigation

## Problem

Poor call quality was attributed to Telnyx, and replacing the carrier was being
considered. The first requirement was to verify whether the problem could be reproduced
and whether it followed the carrier route.

## Environment

- FreeSWITCH 1.10.13-dev
- FusionPBX on Debian 12
- Vultr-hosted system
- Telnyx and Twilio gateways
- Dedicated test extension

## Investigation

1. Reviewed the existing call architecture and located both carrier gateways.
2. Enabled the Telnyx gateway and confirmed registration state as `REGED`.
3. Used a test extension to place controlled calls through Telnyx.
4. Repeated comparable calls through Twilio.
5. Compared the observed call behavior instead of relying on the original assumption.

## Finding

The reported Telnyx quality problem was not reproduced during the controlled tests.
The available evidence did not justify replacing the carrier at that point.

## Engineering Decision

No carrier replacement was recommended based solely on the initial attribution. A
repeatable symptom and route-specific evidence would be required before making that
change.

## Validation Notes

- Gateway registration confirmed signaling readiness.
- Real calls were tested through both configured carrier paths.
- The comparison used the same system and a known test extension.
- Registration alone was not treated as proof of media quality.

## Lesson Learned

**Do not replace a carrier based on assumptions. Reproduce the problem and compare
routes first.**

For an intermittent recurrence, the next evidence set should include timestamps,
call identifiers, RTP statistics, codec/transcoding state and captures from the same
test window.
