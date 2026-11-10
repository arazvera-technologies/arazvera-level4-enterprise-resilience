# Level 4 Architecture — Public Overview

## Component responsibilities

The disposable laboratory contains a FastAPI Control Plane, PostgreSQL 16, a restricted database application account, a periodic observer, an independent event Worker, an internal event receiver, a temporary RS256 identity provider and two separate synthetic Stable/Candidate release services.

    Authorized lab operator
        |
        v
    FastAPI Control Plane  <----  Synthetic RS256/JWKS issuer
        |                              (no public listener)
        |
        +--> PostgreSQL 16
        |       +-- evidence and incident ledger
        |       +-- tenant FORCE RLS
        |       +-- transactional Outbox --> independent Worker
        |                                         |
        |                                         v
        |                                  synthetic HTTP receiver
        |
        +--> bounded health probes and operator read APIs
        |
        +--> measured Canary --> candidate synthetic backend
                      |
                 PASS / HOLD
                      |
                 persisted staging route --> stable synthetic backend

## Authorization

Lab operator access can use a local high-entropy credential or a strict signed-only laboratory token with three roles (viewer, operator, admin). The signed-only mode pins a dedicated internal RS256/JWKS origin and rejects legacy operator secrets. The user-facing issuer is ephemeral and does not implement a customer's SSO/MFA.

Synthetic tenant mutations use tenant-bound scopes, PostgreSQL restricted roles, FORCE RLS and durable replay protection. Real IAM integration is a customer-specific workstream, not an included production claim.

## Incident safety

The same transaction that opens or resolves an incident queues one unique internal alert event. An independent Worker sends the event to an allowlisted synthetic receiver and records a delivery receipt. Repeated failed probes do not duplicate the OPEN transition event. No outside recipient or notification platform is configured.

## Release safety

A synthetic Candidate receives 200 actual measured HTTP probes. The result is a lab candidate PASS or a conservative HOLD, with an actual database-backed staging route change. A faulty Candidate restores Stable. This does not deploy a real image or authorize production traffic.

## Infrastructure isolation

The nine long-running lab containers use their own Compose project with restart policies; bootstrap, restore and test containers are one-shot. Only the Control Plane has a Windows loopback port. Other workloads, including AERON/NEXA/trading, are outside the permitted scope.

## Disaster recovery boundary

An independent disposable PostgreSQL restore and bounded API/database stop/start are verified on one host. No cross-host failover, independent failure domain, encrypted offsite recovery point or customer RPO/RTO is claimed.
