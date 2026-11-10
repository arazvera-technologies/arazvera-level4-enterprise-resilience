# ARAZVERA TECHNOLOGIES — Level 4 Enterprise Resilience Engineering

**Public engineering capability showcase | Version 0.4.0 | November 2026**

An acceptance-tested, single-host laboratory for designing resilient Python/FastAPI backends, secure PostgreSQL tenancy, durable workers, safe release decisions, bounded failure experiments and operational evidence.

**Status:** Laboratory implementation VERIFIED. Customer production deployment and third-party enterprise certification NOT claimed.

## Engineering services available for scoped projects

| Capability | Representative work |
| --- | --- |
| Architecture and reliability assessment | Backend dependencies, service failure analysis, change-risk and acceptance criteria |
| Tenant data protection | Restricted database roles, PostgreSQL FORCE RLS, negative access tests and RS256/JWKS validation |
| Durable recovery and automation | Transactional Outbox, idempotency, independent workers, retries, receipts and controlled database restoration |
| Safe staging releases | Measured Stable/Candidate Canary, conservative HOLD, rollback criteria and evidence history |
| Incident engineering | Health probes, state-transition history, transactional internal notifications and recorded delivery receipts |
| Authentication and authorization design | Three-role laboratory operator controls; integration planning for customer IAM and SSO |

## Proven laboratory acceptance

| Evidence group | Verified outcome |
| --- | --- |
| Full independent disposable Docker Pytest | **129 passed**, zero failed; 2 non-blocking cache warnings |
| Host Python unit tests | **102 passed** |
| Private GitHub Actions v0.4.0 | **4 of 4 jobs passed**, commit 339125a, run 42793494053 |
| Real Chrome/Selenium dashboard checks | **13 of 13 passed** |
| Real lab Canary API acceptance | **3 of 3 passed**, including failing candidate HOLD and Stable route restoration |
| API/PostgreSQL container outage and recovery | **17 of 17 passed** |
| Logical PostgreSQL 16 restore in a separate disposable container | **8 of 8 passed** |
| Independent Worker restart acceptance | **7 of 7 passed** |
| Synthetic identity and operator authorization | Real internal signed JWT/JWKS and viewer/operator/admin negative tests |
| Internal incident notifications | OPEN/RESOLVED Outbox events with independent HTTP delivery and durable receipts |

Test groups overlap. These are genuine **synthetic laboratory tests**, not measurements from an enterprise customer's production installation.

## Deployment and access boundaries

Only the laboratory control API is published to the host's Windows loopback interface. Other test services run within the named Level 4 disposable Docker networks. A separate synthetic identity issuer signs short-lived test tokens; it is not a production SSO provider.

Canary and rollback control actual HTTP routing **between synthetic backends only**, not customer container images or production servers. Notification delivery is currently limited to an internal synthetic downstream. SHA-256 checksums are evidence-integrity checks, not signed third-party attestations.

Read [Architecture](docs/ARCHITECTURE.md), [Verification Evidence](docs/EVIDENCE.md), [Production Adoption Gates](docs/PRODUCTION_READINESS.md) and [Engagement Scope](docs/ENGAGEMENT.md).

## Confidentiality and collaboration

The executable engineering source, security configuration, internal CI test suites and secrets remain in a **separate private repository**. This public repository contains only approved capability documentation and public-facing catalog files, not proprietary code or customer credentials.

**Contact:** [ARAZVERA TECHNOLOGIES](https://github.com/arazvera-technologies) and the [main engineering portfolio](https://github.com/arazvera-technologies/arazvera-engineering-portfolio).

*This project is a reproducible engineering showcase. Every customer production engagement requires an approved scope, customer-owned infrastructure, separate tests and written acceptance.*
