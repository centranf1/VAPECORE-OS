# QA & TEST SPECIFICATION

Document ID: QA-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: QA Engineering Team

---

## 1. QA Strategy

QA VAPECORE POS berfokus pada integritas transaksi, keamanan, akurasi stok, kualitas API, serta keberlanjutan operasional multi-cabang. Uji harus dilakukan pada level unit, integration, API, UI, end-to-end, security, performance, dan UAT untuk memastikan sistem siap dipakai dalam lingkungan operasional nyata.

Kualitas tidak hanya dinilai dari fungsi yang “berjalan”, tetapi dari kemampuan sistem menjaga konsistensi data, mencegah penyalahgunaan otorisasi, menangani failure, serta memberi bukti bukti operasional yang dapat diverifikasi.

## 2. Testing Scope

- POS transaction and payment flow
- Inventory and stock movement
- Approval workflow and escalation
- Finance journal, AP/AR, and reconciliation
- HR attendance, shift, and payroll validations
- Audit trail and reporting integrity
- Security and access control
- Deployment and rollback readiness

## 3. Test Environment

| Environment | Purpose | Control |
|---|---|---|
| Development | Feature validation and unit testing | Low isolation |
| Staging | Integration, regression, and UAT | Product-like |
| Production-like | Load, security, and acceptance rehearsal | Restricted |
| Production | Live business environment | Controlled and monitored |

## 4. Test Data Management

- Gunakan masked personal data dan data sintetis untuk skenario sensitif.
- Siapkan variasi cabang, warehouse, shift, dan pengguna dengan role berbeda.
- Data uji harus mencakup: zero stock, partial payment, refund, repeated transaction attempts, approval denial, and invalid discount.
- Data yang masuk ke uji security tidak boleh menggunakan data produksi real tanpa sanitization.

## 5. Testing Levels

### 5.1 Unit Testing
Focus:
- Business validation
- Domain logic correctness
- Data transformation
- Error handling and exception path

### 5.2 Integration Testing
Validasi interaksi antar komponen:
- POS -> inventory service
- POS -> finance ledger service
- Approval -> workflow engine
- Warehouse -> stock ledger
- HR -> payroll processing input

### 5.3 API Testing
- Validate HTTP status code, payload schema, business validation, authz, and idempotency behavior.
- Confirm response messages do not leak internal details.
- Ensure security headers and rate limiting work.

### 5.4 UI Testing
- Validate state, form validation, navigation, empty states, and accessibility basics.
- Check dashboard filters and export behavior.
- Verify approval workflow user journeys and error states.

### 5.5 End-to-End Testing
Skenario utama:
1. Login user dengan role tertentu.
2. Create purchase order or receiving record.
3. Complete sales transaction.
4. Trigger stock mutation and approval workflow.
5. Validate finance posting and audit record.
6. Review reporting and export output.

## 6. Critical Test Cases

| Test Case ID | Module | Scenario | Expected Result | Priority | Severity |
|---|---|---|---|---|---|
| TC-POS-001 | POS | Complete sale with valid data | Transaction saved once and receipt generated | Critical | Critical |
| TC-POS-002 | POS | Sale with insufficient stock | Rejected with clear error and no ledger mutation | Critical | Critical |
| TC-POS-003 | POS | Refund without approval | Rejected and logged | Critical | Critical |
| TC-INV-001 | Inventory | Negative stock prevention | Validation denies transaction | Critical | Critical |
| TC-FIN-001 | Finance | Duplicate journal posting | Idempotent or reject | Critical | Critical |
| TC-APP-001 | Approval | Unauthorized approver | Request denied and audit record created | Critical | Critical |
| TC-AUD-001 | Audit | Data tampering attempt | Detect and block unauthorized modification | Critical | Critical |
| TC-SEC-001 | Security | Invalid login brute force | Account lockout and monitoring alert | Critical | Critical |
| TC-BI-001 | Reporting | Export dashboard data | File generated and consistent with source data | High | High |
| TC-HR-001 | HR | Attendance and payroll consistency | Approved data produces expected payroll output | High | High |

## 7. Security Testing

- Access control bypass attempt.
- Unauthorized API exhaustion and privilege abuse tests.
- IDOR and authorization boundary checks.
- Session hijack prevention exercises.
- Audit log immutability and integrity validation.
- Penetration or security-focused regression on authentication and payment path.

## 8. Performance and Reliability Testing

### 8.1 Performance
- Dashboard query performance under normal and peak volume.
- POS throughput under concurrent cashier sessions.
- Reporting export and filtering performance.

### 8.2 Load Testing
- 100 concurrent cashier sessions.
- 5000 transaction/day simulation across several branches.
- 20 concurrent approval tasks and workflow workloads.

### 8.3 Stress Testing
- CPU spike condition.
- Database latency conditions.
- Redis outage or cache degradation fallback.
- Network interruption and retry validation.

## 9. Regression Testing

- Semua fitur kritis harus diuji ulang setelah setiap perubahan.
- Fix patch harus melalui staging terlebih dahulu.
- Release candidate harus lulus smoke test sebelum deployment ke production.

## 10. UAT and Business Acceptance

Stakeholders:
- Store managers
- Finance team
- Procurement and warehouse
- Internal audit
- Executive users
- System admin / security admin

UAT acceptance criteria:
- No critical business defect remains open.
- Real operational workflow is understandable and performable.
- User can finish daily tasks without unsupported workaround.
- Executive reporting is understandable and traceable.

## 11. Defect Classification

| Severity | Description |
|---|---|
| Critical | Data loss, financial issue, security breach, major stock issue |
| High | Significant business disruption / blocked process |
| Medium | Feature works but with limited usability or extra steps |
| Low | Cosmetic or minor documentation issue |

## 12. Defect Lifecycle

- New
- In Analysis
- In Progress
- Fixed
- Retest
- Closed
- Reopened

## 13. Release Gate Criteria

Release dapat diterima bila:
- Tidak ada open critical defect.
- Semua security regression checks selesai.
- API contract tests dan critical E2E scenario selesai.
- UAT sign-off dari pemilik bisnis dan stakeholder relevan.
- Deployment readiness checklist approved by QA and Operations.

## 14. Test Reporting

- Daily execution summary
- Defect trend and aging report
- Risk register summary
- Release readiness report
- Post-release issue summary

## 15. Special Prevention Scenarios

- Penjualan tercatat dua kali -> validated by unique transaction number and idempotency key.
- Pembayaran tercatat dua kali -> payment reference validation and duplicate detection.
- Stok menjadi negatif -> service validation plus stock ledger validation.
- Refund tanpa otorisasi -> approval enforcement and audit capture.
- Manipulasi audit log -> immutable storage, restricted access, and tamper detection.

## 16. References

- SRS-VCP-001
- SAD-VCP-001
- SEC-VCP-001
- API-VCP-001
- DEVOPS-VCP-001
- TDCM-VCP-001

---

## 17. QA Governance Notes

- QA tidak boleh menutup defect hanya berdasarkan code review; hasil harus diverifikasi di kondisi test yang sesuai.
- Pengujian kritis harus pernah diperiksa oleh pihak independen bila ada potensi konflik kepentingan.
- Quality gate adalah bagian dari release criteria dan bukan optional checkpoint.
