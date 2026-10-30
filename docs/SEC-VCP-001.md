# SECURITY & COMPLIANCE SPECIFICATION

Document ID: SEC-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: Cybersecurity Architecture Team

---

## 1. Security Architecture

Sistem VAPECORE POS mengikuti pendekatan defense in depth dan backend-enforced authorization. Semua keputusan keamanan wajib diterapkan pada layer backend, dengan validasi konsisten di frontend hanya sebagai pengalaman pengguna dan penguatan UX, bukan sebagai mekanisme keamanan utama.

Arsitektur keamanan mencakup autentikasi, otorisasi, pengendalian data, proteksi service, komunikasi terenkripsi, audit trail, pemantauan, dan proses insiden. Prinsip utama adalah: tidak ada trust pada klien, tidak ada akses langsung tanpa validasi, dan semua perubahan kritis harus dicatat secara permanen.

## 2. Security Objectives

- Melindungi data transaksi, finansial, karyawan, dan pelanggan.
- Mencegah akses tidak sah terhadap fungsi bisnis dan data sensitif.
- Menjamin transaksi kritis tidak bisa diubah tanpa otorisasi dan bukti audit.
- Menyediakan mekanisme pemulihan serta deteksi insiden secara cepat.
- Mendukung kepatuhan terhadap UU PDP Indonesia dan best practice enterprise security.

## 3. Threat Model

| Threat | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Unauthorized access | High | Medium | RBAC, MFA, session control, IP/device validation |
| SQL injection | High | Low | Parameterized queries, ORM, DB least privilege |
| Privilege escalation | High | Low | Backend policy checks, approval workflow, role validation |
| Payment fraud | High | Medium | Idempotency, gateway verification, settlement reconciliation |
| Data leakage | High | Medium | Encryption, PII minimization, RBAC, log redaction |
| Audit tampering | High | Low | Append-only audit store, write restrictions |
| Denial of service | Medium | Medium | Rate limiting, WAF, scaling, load protection |
| Internal abuse | High | Medium | Segregation of duties, approval chain, monitoring |

## 4. Asset Classification

| Asset Class | Examples | Sensitivity |
|---|---|---|
| Transactional data | Sales, refunds, receipts, stock movement | High |
| Financial data | Journal, cash, AP/AR, period close | High |
| Identity data | User credentials, employee profile, access record | High |
| Operational data | Inventory, branch, warehouse, routes | Medium |
| Reporting data | Dashboard, KPIs, exports | Medium |
| Logs and audit records | Session logs, approval history, config changes | High |

## 5. Authentication and Session Security

### 5.1 Authentication
- JWT atau token equivalent dengan expiration pendek untuk akses.
- Refresh token rotation untuk mencegah token theft reuse.
- Account lockout setelah sejumlah jumlah percobaan gagal.
- MFA diwajibkan untuk admin, finance, audit, executive, dan role privileged lainnya.
- Lost credential recovery harus memerlukan verifikasi identitas, bukan hanya reset otomatis.

### 5.2 Session Management
- Idle timeout default 15 menit untuk browser session.
- Max session lifetime mengikuti kebijakan keamanan organisasi.
- Invalidate session setelah password reset, role perubahan, atau revocation.
- Log session metadata seperti device, IP, browser, location, dan status.

## 6. Authorization Model

- Semua keputusan otorisasi harus dievaluasi di backend dan tidak hanya pada UI.
- Setiap operasi sensitif harus memiliki permission policy unik.
- Akses diberikan berdasarkan kombinasi role, branch scope, warehouse scope, dan event type.
- Validasi ownership resource dilakukan untuk memastikan user hanya mengakses data/operasi yang dibolehkan.
- Authorization harus menolak default dan menegakkan fail-closed behavior.

### Role-Based Access Control

| Role | Example Access |
|---|---|
| cashier | POS transactions, open/close shift |
| store_manager | sales oversight, discount approval, cash reconciliation |
| warehouse_manager | transfer approval, receiving validation |
| finance_manager | journal, reconciliation, closing |
| procurement_manager | requisition, PO, supplier invoice review |
| internal_audit | read-only review of logs and reports |
| admin | user, role, and security configuration |

## 7. API Security Controls

- TLS 1.2+ untuk semua koneksi produksi.
- Rate limiting dan anti-bruteforce pada endpoint login dan operasi sensitif.
- Input validation dan output encoding terhadap XSS, injection, malformed payload.
- Strict CORS policy dan allowlist domain.
- No sensitive stack traces / debug payloads to client.
- API idempotency key untuk transaksi finansial dan pembatalan mutasi.

## 8. Data Protection and Cryptography

- Data sensitif disimpan terenkripsi saat rest dan transit.
- Kunci enkripsi dikelola melalui secret manager / KMS.
- Payment credential, token, dan secret tidak disimpan di repository source code.
- Enkripsi level field dapat diterapkan untuk informasi personal data dan token sensitif.
- Semua password disimpan dengan hashing kuat dan salting yang aman.

## 9. Database Security

- Least privilege account untuk aplikasi, migrasi, dan operasi.
- Database network segmentation dan access restriction antar layer.
- Audit log aktif pada tabel sensitif dan perubahan metadata.
- Query harus melalui parameterized database layer dan tidak menggunakan string concatenation.
- Backup terenkripsi dan hanya dapat diakses oleh role yang dibatasi.

## 10. Audit Trail and Integrity

- Log kritikal harus immutable, append-only, dan tidak dapat dihapus oleh role normal.
- Setiap perubahan status penting mencatat actor, timestamp, prev value, new value, reason, and source.
- Audit log harus dapat ditelusuri untuk transaksi jual, refund, stock adjustment, approval, role change, and configuration update.
- Akses ke audit data dibatasi pada security admin dan internal audit.

## 11. Logging and Monitoring

- Logging terstruktur untuk autentikasi, otorisasi, transaksi, payment, inventory, dan operasi keamanan.
- Centralized log aggregation untuk semua environment.
- Alert rule untuk failed login burst, privilege abuse, abnormal transaction volume, and config mutation.
- Dashboard keamanan untuk visibility terhadap incident patterns.

## 12. Privacy and Data Governance

- Penerapan UU No. 27 Tahun 2022 tentang PDP Indonesia.
- Data hanya dikumpulkan untuk tujuan yang sah dan dibatasi.
- Minimisasi data untuk employee, supplier, dan customer informasi.
- Terdapat mechanism akses, koreksi, dan pembatalan pemrosesan sesuai kebijakan organisasi.
- Pihak yang memproses personal data harus menjaga traceability atas penggunaan data.

## 13. Backup, Recovery, and Business Continuity

- Backup database dan konfigurasi secara otomatis dan terenkripsi.
- Restore validation minimal secara berkala untuk memastikan backup berguna.
- Recovery plan memuat RPO and RTO yang disetujui.
- Backup storage harus diakses hanya oleh user dengan role yang dibatasi.

## 14. Vulnerability and Patch Management

- Dependency scan pada CI/CD pipeline.
- Security review dibutuhkan sebelum produksi.
- Patch severity-based dan prioritas terhadap CVE critical/high.
- Container images harus dibangun dari base image yang divalidasi dan terkini.

## 15. Incident Response

| Phase | Action |
|---|---|
| Detection | Alert review and log correlation |
| Containment | Disable compromised account, isolate endpoint, block traffic |
| Eradication | Remove malicious artifact, revoke tokens, patch issue |
| Recovery | Restore service, validate integrity, re-enable access |
| Lessons Learned | Document root cause and preventive action |

## 16. Compliance Requirements

- Security controls harus didokumentasikan dan diverifikasi.
- Audit evidence harus tersedia untuk review internal maupun eksternal.
- Tidak ada klaim kepatuhan yang dibuat tanpa validasi nyata.
- Setting produksi dan perubahan konfigurasi wajib dipantau dan didukung approval trail.

## 17. Security Controls Matrix

| Control | Domain | Status |
|---|---|---|
| MFA | Authentication | Required |
| RBAC | Authorization | Required |
| Audit log immutability | Governance | Required |
| Encryption in transit/rest | Data protection | Required |
| Idempotency | Transaction integrity | Required |
| Rate limiting | API protection | Required |
| Backup and restore | Recovery | Required |
| Vulnerability scanning | SDLC | Required |

## 18. Open Decisions

| Item | Status |
|---|---|
| Final MFA provider | TBD |
| Key management provider | TBD |
| Cloud security baseline | TBD |
| Employee personal data retention schedule | TBD |
| Final incident response SLA | TBD |

---

## 19. References

- UU PDP Indonesia
- MPS-VCP-001
- SAD-VCP-001
- SRS-VCP-001
- API-VCP-001
- DEVOPS-VCP-001
- TDCM-VCP-001
