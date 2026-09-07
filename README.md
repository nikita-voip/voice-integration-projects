# Voice Integration Projects

Sanitized case studies from production VoIP, voice infrastructure and Voice AI
work. The emphasis is on the problem, evidence, engineering decision and validation.

## Production Cases

### PBX and Call Processing

- [FreePBX 15 to 17 Migration](production-cases/04-freepbx-15-to-17-migration/README.md) — migration preparation, restoration and end-to-end validation
- [FreeSWITCH Carrier Quality Investigation](production-cases/05-freeswitch-carrier-quality-investigation/README.md) — Telnyx/Twilio route comparison before changing a carrier
- [FusionPBX Queue Agent Troubleshooting](production-cases/06-fusionpbx-queue-agent/README.md) — an extension could call but was not receiving queue calls

### SIP Signaling and Media

- [ECSS-10 Multi-Domain Registration: 401 Unauthorized](production-cases/01-ecss10-multi-domain-registration/README.md)
- [SMG-500 and TAU-32 Conference Investigation](production-cases/02-smg500-tau32-conference/README.md)
- [SIP re-INVITE: Hold and Resume](production-cases/03-sip-reinvite-hold/README.md)
- [416 Unsupported URI Scheme](production-cases/07-sip-416-unsupported-uri-scheme/README.md)

### Platform Deployment and Recovery

- [ECSS-10 3.18 Deployment and PostgreSQL Recovery](production-cases/08-ecss10-deployment-postgresql-recovery/README.md)

## Voice AI Integration

- [Vapi to ECSS SIP Call Transfer](projects/01-vapi-ecss-sip-transfer/README.md) — SIP registration, AI call handling and trace-based transfer validation
- Related engineering notes: [AI Voice Lab](https://github.com/nikita-voip/ai-voice-lab)

## Related Repositories

- [VoIP Notes](https://github.com/nikita-voip/voip-notes) — reusable references and practical guides
- [ECSS-10 Training](https://github.com/nikita-voip/ecss10-training) — labs and platform-specific learning material

## Publication Policy

These cases describe engineering reasoning and outcomes without exposing customer
identities, credentials, telephone numbers, private addresses, internal topology or
proprietary configuration. Simplified diagrams and representative identifiers are
used where useful.
