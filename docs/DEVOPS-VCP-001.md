# DEVOPS & DEPLOYMENT MANUAL

Document ID: DEVOPS-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: DevOps & Cloud Engineering Team

---

## 1. DevOps Strategy

Strategi DevOps VAPECORE POS menekankan kualitas, keamanan, observability, dan release yang dapat diaudit. Penerapan sistem didesain dalam pendekatan containerized deployment dengan otomatisasi CI/CD, kontrol environment, dan pola rollback yang jelas.

Tujuan utama adalah memastikan setiap perubahan aplikasi atau infrastruktur dapat dibangun, diuji, dideploy, dipantau, dan dikembalikan dengan konsisten. Semua deployment harus mengikuti quality gate dan kebijakan keamanan.

## 2. Environment Architecture

| Environment | Purpose | Notes |
|---|---|---|
| Development | Continuous engineering and unit validation | Remote/shared dev |
| Staging | Integration, regression, UAT, and security validation | Production-like |
| Production | Live business operation | Restricted and monitored |
| Disaster Recovery / Backup | Recovery and continuity testing | Isolated environment |

## 3. Development Stack

- Frontend: Next.js, React, TypeScript, Tailwind CSS
- Backend: NestJS, TypeScript
- Database: PostgreSQL 15+
- Cache / Queue: Redis, async workers
- Containerization: Docker
- Runtime / Deployment: managed cloud or equivalent orchestration platform

## 4. Local and Shared Development Setup

### Local Components
- Docker Compose for local dependencies
- PostgreSQL service
- Redis service
- Application containers for frontend and backend

### Shared Development Baseline
- Shared branch for integration testing
- Automated lint, format, and unit tests
- Standard environment variables and configuration template

## 5. Staging Environment

- Mereplikasi konfigurasi produksi sebanyak mungkin.
- Seed data menggunakan snapshot yang telah disanitasi.
- Automated smoke test dan regression suite setelah deployment.
- Setup access terbatas untuk QA dan release owner.

## 6. Production Environment

- API service dibangun agar dapat di-scale horizontal.
- Database dengan failover, backup, dan monitoring.
- Load balancer / reverse proxy untuk routing trafik.
- Observability meliputi logs, metrics, traces, dan alert.

## 7. Infrastructure Requirements

| Component | Requirement |
|---|---|
| Application | 2+ API instances; horizontal scale support |
| Database | HA Postgres with backup and recovery plan |
| Cache | Redis cluster or managed cache |
| Monitoring | Metrics, logs, traces, alerting |
| Storage | Object storage for export and attachments |
| Network | Private networking and controlled public ingress |

## 8. Cloud Architecture Considerations

- Prefer managed cloud hosting agar operasional lebih cepat, aman, dan terdokumentasi.
- Arsitektur harus tetap portable meskipun provider final belum diputuskan.
- Prefer private networking, WAF, and managed security features if available.
- Deploy design must preserve clear separation of environment and minimal blast radius.

## 9. Docker Configuration

### Example Dockerfile

```dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app .
EXPOSE 3000
CMD ["npm", "run", "start"]
```

### Example Docker Compose

```yaml
version: '3.9'
services:
  app:
    build: .
    ports:
      - '3000:3000'
    environment:
      DATABASE_URL: postgres://postgres:postgres@db:5432/vapecore
      REDIS_URL: redis://redis:6379
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: vapecore
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - '5432:5432'
  redis:
    image: redis:7
    ports:
      - '6379:6379'
```

## 10. CI/CD Pipeline

### Pipeline Stages
1. Dependency install
2. Lint and static analysis
3. Unit tests
4. Integration tests
5. Security scan
6. Build artifact
7. Deploy to staging
8. Smoke test and QA validation
9. Manual approval for production
10. Production deployment and post-deploy validation

### Deployment Rules
- No production deploy without passing quality gate.
- Database migration must be validated in staging.
- Rollback plan must exist before production deployment.

## 11. Build and Release Process

- Build artifact with semantic version tag.
- Run tests and security gates before sign-off.
- Generate deployment manifest or release summary.
- Archive deployed version for rollback and incident review.

## 12. Database Migration and Schema Governance

- Every schema change uses migration scripts with versioned history.
- Before production deployment, migration must be tested in staging.
- Backup must exist before migration and rollback path must be documented.
- Application must support backward or forward compatibility as required by deployment window.

## 13. Environment Variables and Secrets

| Variable | Purpose |
|---|---|
| DATABASE_URL | PostgreSQL connection |
| REDIS_URL | Cache connection |
| JWT_SECRET | Auth signing key |
| API_BASE_URL | Backend endpoint |
| NODE_ENV | Environment mode |
| SECRET_MANAGER | Secret provider identifier |

### Secrets Handling
- Credentials must be injected from secret manager or secure environment store.
- Never commit secrets into source repository or deployment manifest.
- Rotate keys on schedule and after suspected exposure.

## 14. Monitoring, Logging, and Observability

- Metrics: CPU, memory, request latency, database health, queue backlog.
- Logs: application logs, auth logs, payment logs, and error logs.
- Traces: request correlation across API and service boundaries.
- Alert routing: email, chat, and incident channel.
- Alert thresholds must be tuned for business criticality and SLO/SLA.

## 15. Backup and Disaster Recovery

- Automated database backup at defined interval.
- Backup storage encrypted and access-controlled.
- Restore validation at least quarterly.
- Disaster recovery runbook maintained in operations documentation.
- RPO and RTO defined per critical service and financial data.

## 16. Rollback Strategy

- Deployment artifacts versioned and traceable.
- Immediate rollback for failed production deployment or critical issue.
- Database rollback compatibility tested as part of release readiness.
- Rollback must include monitoring and verification after recovery.

## 17. Incident Response and Operational Readiness

| Incident | Owner | Action |
|---|---|---|
| API outage | DevOps | Restore service, assess dependencies, log incident |
| Database issue | DBA / Platform team | Failover and restore |
| Payment failure | Platform owner | Verify gateway health and rollback if needed |
| Security incident | Security lead | Containment, forensic review, remediation |
| Cache degradation | DevOps | Rebalance or failover service |

## 18. Deployment Checklists

- Security scan passed.
- Migration validated.
- Smoke tests passed.
- Backup confirmed.
- Monitoring active.
- Rollback path ready.
- Stakeholder approval recorded.

## 19. Open Items

| Item | Status |
|---|---|
| Final cloud provider | TBD |
| Managed database vs self-hosted | TBD |
| Container orchestration platform | TBD |
| Incident response SLA | TBD |

---

## 20. References

- SAD-VCP-001
- API-VCP-001
- SEC-VCP-001
- QA-VCP-001
- TDCM-VCP-001
