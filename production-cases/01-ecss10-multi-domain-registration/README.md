# ECSS-10 Multi-Domain Registration Issue

## Symptom

SIP registration and call attempts failed with responses such as `401 Unauthorized`
and the ECSS diagnostic reason `configurationOrCustomizationError`.

## Environment

- ECSS-10
- Multiple SIP domains
- SIP endpoints using REGISTER and INVITE
- Domain-specific routing and Request-URI validation

## Investigation

The signaling response looked like an authentication problem, so credentials alone
were not enough to explain the failure. The investigation correlated:

1. The source network and its assigned IP set.
2. SIP domain configuration.
3. `allowed-ruri-list` matching.
4. The REGISTER and INVITE Request-URI domains.
5. Network properties used during domain selection.

## Root Cause

The same IP set was assigned to more than one SIP domain. This made domain selection
ambiguous and caused requests to be evaluated in the wrong configuration context.

## Resolution

The IP-set-to-domain mapping was corrected, then the Request-URI and allowed URI
rules were validated against the intended domain. REGISTER and INVITE processing
were retested after the configuration change.

## Verification Checklist

- Confirm that each source network maps to the intended SIP domain.
- Compare the Request-URI domain with the selected ECSS domain.
- Validate `allowed-ruri-list` against the actual signaling.
- Check REGISTER and INVITE separately.
- Treat `401 Unauthorized` as a routing or domain-selection symptom until the full
  selection path has been verified.

## Lesson Learned

A SIP authentication response does not always mean that the password is wrong.
In a multi-domain platform, network classification and domain selection happen
before authentication can be interpreted correctly.

> All customer-specific addresses, identifiers and configuration values are omitted.
