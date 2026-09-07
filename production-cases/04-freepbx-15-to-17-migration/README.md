# FreePBX 15 to 17 Migration

## Problem

A client FreePBX 15 system had to be migrated to FreePBX 17 while preserving the
working voice service. The task was not complete when the new interface loaded; SIP
endpoints, trunks and real call paths all had to work after the migration.

## Environment

- FreePBX 15 source system
- FreePBX 17 target system
- SIP/PJSIP extensions and trunks
- Internal and external calling

Customer-specific versions, addresses, numbers and configuration are omitted.

## Preparation

- Inventory extensions, trunks, routes and dependencies outside FreePBX.
- Record current registration and trunk state.
- Test representative internal, inbound and outbound calls before migration.
- Produce and verify backups before changing the source system.
- Define rollback conditions and keep the previous service recoverable.

## Migration and Investigation

1. Restore the supported configuration to the FreePBX 17 environment.
2. Review migrated SIP/PJSIP settings instead of assuming complete equivalence.
3. Confirm that extensions register and can establish calls.
4. Validate trunk reachability, authentication and routing.
5. Compare network routes and operating-system dependencies between old and new hosts.

During restoration, a missing static route on the new server prevented access to a
provider network. The symptoms initially resembled a SIP trunk or PBX configuration
failure, but signaling and network-path checks isolated the issue below the PBX layer.

## Root Cause

The required operating-system route existed on the old server but was absent on the
new one. The PBX configuration alone did not contain everything needed to restore the
service.

## Solution

The missing route was restored and the migrated FreePBX configuration was revalidated.

## Validation

- SIP/PJSIP extensions registered successfully.
- Internal calls completed in both directions.
- Trunk status and provider reachability were verified.
- Inbound and outbound calls completed through the intended routes.
- Two-way audio was checked, not inferred from a successful SIP response.

## Practical Checklist

### Before

- [ ] Inventory PBX and operating-system dependencies
- [ ] Verify backups and restore procedure
- [ ] Capture baseline registrations and test calls
- [ ] Define maintenance and rollback criteria

### After

- [ ] Check extensions and endpoint technology
- [ ] Check trunks, routes and number manipulation
- [ ] Test internal, inbound and outbound calls
- [ ] Verify SDP and two-way RTP
- [ ] Review logs and make the final configuration backup

## Lesson Learned

A PBX migration is an environment migration. Compare routing, firewall, certificates,
DNS and external dependencies—not only the FreePBX database and GUI settings.
