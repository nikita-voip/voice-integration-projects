# SIP 416 Unsupported URI Scheme

## Problem

An SBC received a request whose target used a `tel:` URI and rejected it with:

```text
416 Unsupported URI Scheme
```

## Investigation

The response identified a URI-format compatibility issue rather than a transport,
authentication or media failure. The diagnostic path was:

1. Inspect the Request-URI in the rejected request.
2. Confirm which URI schemes the receiving SBC accepts in that routing context.
3. Determine where normalization should occur.
4. Preserve the called-party value while changing only the required representation.

## Considered Solution

Normalize the destination from a `tel:` URI to the `sip:` form expected by the next
hop, for example:

```text
tel:<number>  →  sip:<number>@<representative-domain>
```

This is a representative pattern, not a customer configuration. The correct domain,
header handling and routing behavior must be derived from the actual interconnect.

## Validation Plan

- Confirm that the rewritten Request-URI uses an accepted scheme.
- Verify that called-party identity remains correct.
- Check route selection and the downstream response.
- Complete an end-to-end test including SDP and bidirectional RTP.
- Confirm that the rule does not rewrite unrelated traffic.

## Lesson Learned

SIP error codes can precisely identify the failing layer. A 416 response should lead
first to URI parsing and normalization—not to random changes in authentication,
codecs or network connectivity.
