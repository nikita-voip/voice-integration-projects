# ECSS-10 3.18 Deployment and PostgreSQL Recovery

## Scope

Participation in a single-server ECSS-10 deployment on Ubuntu 22.04, including
installation troubleshooting, recovery of a failed PostgreSQL component, completion
of the required platform services and a customer demonstration.

## Environment

- Ubuntu 22.04
- ECSS-10 3.18.0.271
- `ecss-postgres-bdr-ssw 18.0.0+ssw`
- Containerized PostgreSQL component
- ECSS web configuration, REST, media and related services

All deployment-specific addresses, identifiers, licenses and access data are omitted.

## Problems Encountered

- Network reachability and DNS resolution
- Package repository and APT issues
- PostgreSQL package left in a failed or partially configured state
- Service dependencies required before the ECSS installation could continue

## PostgreSQL Investigation

The PostgreSQL package had initialized data, but its installation flow attempted
subsequent database work before the service was fully ready. Retrying without
understanding the package behavior risked damaging the initialized state.

The investigation covered:

- package state and maintainer-script behavior;
- container lifecycle and the PostgreSQL readiness window;
- port use and persistent storage;
- database, role and extension state after recovery.

## Recovery

The failed component was recovered without deleting the existing PostgreSQL data.
The exact package was reinstalled, configuration completed successfully and package
management returned to a consistent state.

## Deployment Result

- ECSS-10 installation completed.
- The required PostgreSQL package was restored to an installed state.
- Existing initialized data was preserved.
- PostgreSQL and the principal ECSS services were operational.
- Web configuration, REST, media server and other required components were installed.
- The configured system was demonstrated to the customer.

## Validation

- Package audit returned clean.
- PostgreSQL service/container state was checked.
- Required databases, roles and extensions were verified.
- Core ECSS services and user-facing components were checked after installation.

## Lessons Learned

- Preserve initialized state before repairing a failed package.
- Read package scripts and service readiness behavior before retrying installation.
- Treat DNS, routing and repositories as deployment dependencies, not unrelated Linux
  details.
- Validate the platform as a system after package recovery; an installed package alone
  does not prove service readiness.

Related learning material: [ECSS-10 Training](https://github.com/nikita-voip/ecss10-training).
