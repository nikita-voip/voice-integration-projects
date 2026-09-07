# Vapi to ECSS SIP Call Transfer

Production-style AI Voice integration between Vapi and ECSS-10 using native SIP.

---

## Goal

Connect a Vapi AI Voice Agent to an ECSS-10 PBX through SIP registration and
validate transfer behavior using SIP traces—not only application-level status.

---

## Architecture

```
Caller → Voice AI / Vapi → SIP integration → ECSS-10 → Transfer target
```

---

## Call Flow

1. Caller reaches the Vapi AI Agent.
2. AI answers the call.
3. AI talks to the caller.
4. AI decides to transfer.
5. Blind transfer is requested with SIP REFER.
6. The SIP trace confirms REFER behavior and the transfer target receives the call.
7. The AI leg leaves the completed blind-transfer scenario.

## Transfer Investigation

Two transfer modes were evaluated:

### Blind REFER

Blind transfer worked and was confirmed in the SIP trace. The signaling evidence
matched the successful call result.

### Warm Transfer Experimental

The experimental warm-transfer flow did not produce the expected second SIP INVITE
on ECSS. This is not documented as a completed warm transfer: the trace showed that
the required second call leg was not created.

The useful result was the boundary itself—application intent does not prove that a
new telephony leg exists. The SIP trace remains the source of truth.

---

## Result

✅ SIP REGISTER successful

✅ Incoming AI calls working

✅ Live AI conversation

✅ Native SIP REFER transfer

✅ Human operator receives the call

✅ End-to-end scenario completed successfully

⚠️ Experimental warm transfer did not create the expected second ECSS SIP INVITE

---

## Files

| File | Description |
|------|-------------|
| [Refer.png](screenshots/Refer.png) | Sanitized SIP REFER configuration |
| [Subscriber.png](screenshots/Subscriber.png) | Sanitized ECSS subscriber configuration |
| [history call.png](screenshots/history%20call.png) | Successful transferred call |
| [vapi-transfer1.pcap](captures/vapi-transfer1.pcap) | Wireshark capture of the transfer |

---

## Technologies

- ECSS-10
- Vapi
- SIP
- SIP REGISTER
- SIP REFER
- RTP
- VoIP

---

## Notes

Sensitive information (IP addresses, credentials, phone numbers) has been removed before publishing.

## Lesson Learned

Blind and warm transfer are different call architectures. Validate each expected
dialog and INVITE in the signaling trace instead of treating a transfer API response
as proof of the complete telephony flow.

## Skills demonstrated

- SIP Troubleshooting
- SIP REGISTER
- SIP REFER
- AI Voice Integration
- ECSS-10
- Vapi
- RTP Analysis
- Wireshark
