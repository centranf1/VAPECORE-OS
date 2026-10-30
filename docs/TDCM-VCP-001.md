# TRACEABILITY & DOCUMENT CONTROL MATRIX

Document ID: TDCM-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: Solution Architecture Team

---

## 1. Purpose

Dokumen ini menghubungkan seluruh deliverable dokumentasi proyek agar keutuhan requirement, arsitektur, model data, API, UX, SOP, security, QA, dan deployment dapat ditelusuri secara konsisten. Matriks ini juga berfungsi sebagai control point ketika terdapat perubahan scope, kebutuhan, atau keputusan arsitektural.

## 2. Document Inventory

| Document ID | Title | Status |
|---|---|---|
| MPS-VCP-001 | Master Project Specification | Baseline |
| SAD-VCP-001 | System Architecture Document | Baseline |
| SRS-VCP-001 | Software Requirements Specification | Baseline |
| DDD-VCP-001 | Database Design Document | Baseline |
| API-VCP-001 | API Technical Specification | Baseline |
| UX-VCP-001 | UI/UX Design System | Baseline |
| SOP-VCP-001 | Business Process & SOP Document | Baseline |
| SEC-VCP-001 | Security & Compliance Specification | Baseline |
| QA-VCP-001 | QA & Test Specification | Baseline |
| DEVOPS-VCP-001 | DevOps & Deployment Manual | Baseline |
| TDCM-VCP-001 | Traceability & Document Control Matrix | Baseline |

## 3. Cross-Document Traceability

| Business Need | Architecture | Data | API | UI | SOP | Security | QA |
|---|---|---|---|---|---|---|---|
| POS transaction | SAD | DDD | API | UX | SOP | SEC | QA |
| Inventory and stock movement | SAD | DDD | API | UX | SOP | SEC | QA |
| Finance posting and ledger | SAD | DDD | API | UX | SOP | SEC | QA |
| Approval workflow | SAD | DDD | API | UX | SOP | SEC | QA |
| Employee and attendance | SAD | DDD | API | UX | SOP | SEC | QA |
| Procurement and GR | SAD | DDD | API | UX | SOP | SEC | QA |
| Security and RBAC | SAD | DDD | API | UX | SOP | SEC | QA |
| Reporting | SAD | DDD | API | UX | SOP | SEC | QA |

## 4. Requirement-to-Implementation Mapping

| Requirement ID | Domain | Document Reference |
|---|---|---|
| FR-POS-002 | POS | SRS-VCP-001, API-VCP-001, DDD-VCP-001 |
| FR-SCT-001 | Inventory | SRS-VCP-001, DDD-VCP-001 |
| FR-FIN-001 | Finance | SRS-VCP-001, DDD-VCP-001 |
| FR-APP-001 | Approval | SRS-VCP-001, API-VCP-001 |
| FR-SEC-001 | Security | SRS-VCP-001, SEC-VCP-001 |
| FR-BI-001 | Reporting | SRS-VCP-001, API-VCP-001 |
| FR-HR-004 | HR / Payroll | SRS-VCP-001, SOP-VCP-001 |
| FR-PROC-005 | Procurement | SRS-VCP-001, API-VCP-001, SOP-VCP-001 |

## 5. Document Dependency Matrix

| Primary Doc | Depends On |
|---|---|
| SAD-VCP-001 | MPS-VCP-001 |
| SRS-VCP-001 | MPS-VCP-001, SAD-VCP-001 |
| DDD-VCP-001 | SAD-VCP-001, SRS-VCP-001 |
| API-VCP-001 | SAD-VCP-001, SRS-VCP-001, DDD-VCP-001 |
| UX-VCP-001 | SAD-VCP-001, SRS-VCP-001 |
| SOP-VCP-001 | SAD-VCP-001, SRS-VCP-001 |
| SEC-VCP-001 | SAD-VCP-001, SRS-VCP-001, API-VCP-001 |
| QA-VCP-001 | SRS-VCP-001, API-VCP-001, SEC-VCP-001 |
| DEVOPS-VCP-001 | SAD-VCP-001, API-VCP-001, SEC-VCP-001 |
| TDCM-VCP-001 | MPS-VCP-001 and all major package documents |

## 6. Decision Log

| Decision ID | Decision | Status |
|---|---|---|
| DEC-001 | Use modular monolith as initial architecture | Accepted |
| DEC-002 | PostgreSQL as primary database | Accepted |
| DEC-003 | Use NestJS + Next.js baseline stack | Accepted |
| DEC-004 | Append-only stock ledger | Accepted |
| DEC-005 | Backend-enforced authorization | Accepted |
| DEC-006 | Cloud deployment approach to be confirmed | TBD |
| DEC-007 | Final payroll scope | TBD |
| DEC-008 | Discount and refund thresholds | TBD |

## 7. Open Issues and Assumptions

| ID | Type | Description | Owner |
|---|---|---|---|
| OI-001 | Assumption | Final branch count not yet fixed | PM |
| OI-002 | Assumption | Payroll scope still TBD | HR / PM |
| OI-003 | Decision Required | Final cloud provider selection | CTO / Project Owner |
| OI-004 | Decision Required | Discount and refund thresholds | Finance / Management |
| OI-005 | Decision Required | Final retention policy for employee personal data | Security / HR |

## 8. Change Control

- Semua perubahan terhadap requirement, Architektur, atau deployment harus dicatat dengan referensi dokumen yang terdampak.
- Setiap change request harus dipertimbangkan dampaknya terhadap architecture, security, data model, integration, dan testing.
- Jika perubahan menyalahi MPS, maka harus dikonfirmasi ulang dan hasilnya disertakan dalam log perubahan.
- Versi dokumen yang mengalami perubahan harus diperbarui sesuai aliran perubahan formal.

## 9. Document Review Status

| Document | Review Status | Approval Status |
|---|---|---|
| SAD-VCP-001 | Ready for review | Pending |
| SRS-VCP-001 | Ready for review | Pending |
| DDD-VCP-001 | Ready for review | Pending |
| API-VCP-001 | Ready for review | Pending |
| UX-VCP-001 | Ready for review | Pending |
| SOP-VCP-001 | Ready for review | Pending |
| SEC-VCP-001 | Ready for review | Pending |
| QA-VCP-001 | Ready for review | Pending |
| DEVOPS-VCP-001 | Ready for review | Pending |
| TDCM-VCP-001 | Ready for review | Pending |

## 10. Completion Summary

Semua dokumen baseline utama dan matriks traceability telah disusun untuk menyediakan paket dokumentasi penerapan VAPECORE POS. Dokumen-dokumen ini masih memerlukan konfirmasi bisnis untuk item TBD dan keputusan arsitektural yang belum final. Paket ini sudah siap digunakan sebagai baseline untuk review lanjutan, implementasi, dan validasi.

---

## 11. References

- MPS-VCP-001
- AGENT.md
- SAD-VCP-001
- SRS-VCP-001
- DDD-VCP-001
- API-VCP-001
- SEC-VCP-001
- QA-VCP-001
- DEVOPS-VCP-001
