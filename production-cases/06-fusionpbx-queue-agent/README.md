# FusionPBX Queue Agent Troubleshooting

## Problem

An extension could make internal calls but did not receive calls delivered through a
FusionPBX Call Center queue.

## Call Architecture

```text
DID → Time Condition → Call Center Queue → Agents
```

The working internal calls proved that the endpoint and basic extension registration
were functional. The failure was specific to the queue-delivery path.

## Investigation

- Confirmed that calls reached the intended time condition and queue.
- Separated endpoint registration from call-center membership.
- Checked whether the extension existed as a Call Center Agent.
- Reviewed the agent-to-queue assignment.

## Root Cause

The extension was a valid PBX endpoint but had not been created as a Call Center Agent.
An extension and a queue agent are separate objects with different roles.

## Solution

A Call Center Agent was created for the extension, assigned to the queue and the
relevant configuration was reloaded.

## Validation

After the agent assignment and reload, inbound calls from the queue reached the
extension successfully. Internal calling remained operational.

## Lesson Learned

Start at the last confirmed working boundary. When direct calls work but queue calls
do not, inspect queue distribution, agent state and membership before changing SIP
registration or endpoint configuration.
