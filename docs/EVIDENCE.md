# Verification Evidence — Level 4 v0.4.0

**Source release:** private commit 339125a1c3f9c8030bbc534a1fd5f8db73aec45d

**Latest hosted CI:** 4/4 successful GitHub Actions jobs, run 42793494053. Full logs are available only to authorized private repository collaborators. Public readers must not interpret inaccessible logs as third-party certification.

## Verified execution groups

| Group | Observation |
| --- | --- |
| Python unit suite | 102 passed |
| Complete disposable Docker suite | 129 passed, 0 failed, 2 non-blocking cache warnings |
| GitHub Actions | 4/4 successful: Python 3.11, Python 3.12, PostgreSQL 16 integration, disposable multi-service integration |
| Selenium/Chrome UI | 13/13 successful interactions |
| Synthetic Canary | 3/3 actual HTTP routing acceptance scenarios, with HOLD and rollback |
| Scoped API/PostgreSQL recovery | 17/17 real container stop/start and readiness/persistence checks |
| Independent Worker crash/restart | 7/7, with delivered pending event and receipt |
| PostgreSQL 16 logical restore | 8/8 in a separate disposable container |
| Tenant RLS | Restricted accounts, FORCE RLS and negative cross-tenant checks |
| Operator signed role model | Real internal issuer/JWKS test and role denial checks |
| Transactional incident alerts | OPEN/RESOLVED events, independent internal HTTP delivery, stored receipts |

These test groups may overlap; their figures are not additive.

## Verification constraints

- Production authorization is always false in the laboratory release and signed identity test responses.
- A SHA-256 manifest is an integrity checksum, not an operator-authenticated digital signature.
- Sparse SLO data is reported as unknown instead of fabricated percentile availability.
- HTTP timeouts during database outage are recorded as unhealthy/unknown, not misreported as HTTP 503.
- A Docker restart policy does not prove unattended host startup.
- No real customer alert delivery, production release, multi-host DR, independent security audit or customer SLA was executed.
