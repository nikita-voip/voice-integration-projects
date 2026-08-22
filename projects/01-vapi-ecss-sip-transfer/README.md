# Vapi → ECSS SIP Call Transfer

Production-style AI Voice integration between Vapi and ECSS-10 using native SIP.

---

## Goal

Connect a Vapi AI Voice Agent to an ECSS-10 PBX via SIP REGISTER and successfully transfer live calls to a human operator using native SIP REFER.

---

## Architecture

```
Caller
   │
   ▼
Vapi AI Agent
   │
SIP REGISTER
   │
ECSS-10
   │
SIP REFER
   │
Human Operator
```

---

## Call Flow

1. Caller reaches the Vapi AI Agent.
2. AI answers the call.
3. AI talks to the caller.
4. AI decides to transfer.
5. A SIP REFER is used to request the transfer through the ECSS integration.
6. The transfer target receives the call.
7. AI leaves the call.

---

## Result

✅ SIP REGISTER successful

✅ Incoming AI calls working

✅ Live AI conversation

✅ Native SIP REFER transfer

✅ Human operator receives the call

✅ End-to-end scenario completed successfully

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

## Skills demonstrated

- SIP Troubleshooting
- SIP REGISTER
- SIP REFER
- AI Voice Integration
- ECSS-10
- Vapi
- RTP Analysis
- Wireshark
