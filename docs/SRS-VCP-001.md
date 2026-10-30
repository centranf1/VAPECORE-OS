# SOFTWARE REQUIREMENTS SPECIFICATION

Document ID: SRS-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: Business Analyst & Requirements Engineering Team
Reference: MPS-VCP-001

---

## 1. Document Control

| Field | Value |
|---|---|
| Document ID | SRS-VCP-001 |
| Name | Software Requirements Specification |
| Project | VAPECORE POS |
| Status | Baseline |
| Language | Bahasa Indonesia |
| Owner | Senior Business Analyst |
| Reviewers | Solution Architect, Security Architect, QA Engineer |

### Revision History

| Version | Date | Description |
|---|---|---|
| 1.0.0 | 2026-10-30 | Initial requirements baseline |
| 1.1.0 | 2026-10-30 | Detailed expansion of requirement catalog, business rules, traceability, and acceptance criteria |

---

## 2. Introduction

SRS ini mendefinisikan kebutuhan fungsional dan non-fungsional VAPECORE POS sebagai platform operasional enterprise untuk retail multi-cabang. Dokumen ini memuat requirement bisnis, rule of operation, hak akses, dan kualitas layanan yang harus dipenuhi oleh tim produk, engineering, security, QA, dan operasi.

Tujuan utama dokumen ini adalah menyediakan spesifikasi yang dapat diimplementasikan, diuji, diaudit, dan dipelihara dengan prinsip single source of truth. Semua perubahan pada scope atau pekerjaan berikutnya harus merujuk ke dokumen ini sebelum implementasi dilanjutkan.

## 3. Purpose and Scope

### 3.1 Purpose
Dokumen ini berfungsi untuk:
- Menggambarkan kebutuhan bisnis seluruh domain operasional perusahaan.
- Menentukan kebutuhan fungsi, data, integrasi, otorisasi, kebijakan, dan kualitas layanan.
- Menjadi dasar perancangan arsitektur, model data, API, UX, SOP, Security, QA, dan operational deployment.
- Menjamin transaksi kritis, stok, jurnal, dan audit trail seluruhnya terdokumentasi dan valid.

### 3.2 Scope
Cakupan sistem mencakup:
- Executive Command Center
- Point of Sale
- Product Management
- Inventory Management
- Stock Control, Tracking & Cycle Count (SCT)
- Warehouse Management
- Distribution & Transfer Management
- Finance Management
- Human Resources
- Internal Audit
- Procurement & Supplier Management
- Branch Management
- Approval & Workflow
- Business Intelligence & Reporting
- System Administration & Security

### 3.3 Out of Scope
- Payroll engine yang sepenuhnya kompleks di luar cakupan baseline saat ini, kecuali apabila disetujui pada fase berikutnya.
- Settlement bank atau payment gateway tertentu masih bersifat pilihan implementasi.
- Integrasi ERP/CRM pihak ketiga di luar batas yang disepakati sebagai prioritas awal.

## 4. System Overview

VAPECORE POS adalah sistem enterprise yang terintegrasi untuk operasi retail dari level toko, gudang, dan cabang hingga kantor pusat. Sistem ini harus mampu menangani transaksi penjualan, perubahan stok, distribusi barang, pembukuan jurnal, manajemen SDM, approval, hingga kepatuhan audit.

Setiap transaksi yang berdampak pada stok, kas, pembiayaan, personal data, atau aktivitas sensitif harus terikat pada validasi, audit log, dan otorisasi yang jelas. Sistem juga harus menyediakan visibilitas manajerial dan eksekutif melalui dashboard dan report.

## 5. User Classes and Characteristics

| User Class | Description | Primary Needs |
|---|---|---|
| Store Employee | Cashier dan staf operasional toko | POS transaction, cash handling, receipt issuance |
| Store Manager | Pengelola operasional toko | Sales overview, stock status, discount approval, cash reconciliation |
| Supervisor | Supervisor area/cabang | Branch metrics, stock movement, performance reporting |
| Finance | Tim keuangan | Journal, AP/AR, reconciliation, closing |
| Procurement | Tim pembelian dan supplier | PO, receipt, supplier invoice matching |
| Warehouse Staff | Tim gudang dan distribusi | Receiving, transfer, cycle count, allocation |
| HR | Karyawan dan operasional SDM | Attendance, shift, approval, payroll |
| Internal Audit | Tim audit internal | Audit trail, control evidence, compliance review |
| Executive | Direksi / top management | KPI, dashboard, branch comparison |
| System Admin | Administrator platform | User, role, permission, logging, policy |

## 6. Business Objectives and Success Measures

### 6.1 Business Objectives
- Meningkatkan akurasi transaksi dan stok di seluruh cabang.
- Menyediakan operasional retail yang terintegrasi dan terdokumentasi.
- Mencegah kesalahan transaksi finansial dan penyalahgunaan otorisasi.
- Mempercepat insight keputusan melalui dashboard dan KPI.
- Menyiapkan landasan audit dan kepatuhan yang siap ditinjau.

### 6.2 Success Criteria
- 99.9% availability untuk layanan utama saat jam operasi.
- 100% transaksi kritis mencatat ledger dan audit log.
- Transaksi stok, finansial, dan refund tidak dapat diselesaikan tanpa validasi yang sah.
- Waktu respons operasi standar di bawah 2 detik untuk UI dan API utama.
- Zero critical defect untuk fitur operasional utama pada release validasi.

## 7. Functional Requirements

### 7.1 Executive Command Center

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-EXC-001 | Executive Dashboard | High |
| FR-EXC-002 | KPI Monitoring | High |
| FR-EXC-003 | Branch Performance Comparison | High |
| FR-EXC-004 | Approval Status Monitor | High |
| FR-EXC-005 | Stock Discrepancy Alert | High |

#### FR-EXC-001: Executive Dashboard
- Description: Menyediakan dashboard ringkas performa perusahaan pada periode tertentu.
- Actor: Executive Management
- Preconditions: User memiliki hak akses dashboard eksekutif.
- Trigger: Login dan pemilihan rentang tanggal.
- Main Flow: Pilih periode > pilih cabang/area > lihat KPI > drilldown detail.
- Alternative Flow: Bandingkan dengan periode sebelumnya.
- Exception Flow: Data kosong, periode tidak valid, atau cabang tidak tersedia.
- Business Rules: Data harus berasal dari transaksi valid dan bukan entri manual yang tidak terverifikasi.
- Input Requirements: tanggal mulai, tanggal akhir, cabang, area, divisi.
- Output Requirements: KPI summary, trend chart, drilldown data, export.
- Validation: Rentang tanggal tidak boleh kosong atau tidak valid.
- Permission Requirements: EXECUTIVE_VIEW
- Acceptance Criteria: Dashboard menampilkan KPI yang akurat, dapat digunakan untuk drilldown, dan dapat diekspor ke format standar.

### 7.2 Point of Sale

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-POS-001 | Product Search and Cart | High |
| FR-POS-002 | Sales Transaction | Critical |
| FR-POS-003 | Payment Processing | Critical |
| FR-POS-004 | Refund and Reversal | Critical |
| FR-POS-005 | Cashier Shift Management | High |
| FR-POS-006 | Receipt and Transaction History | High |

#### FR-POS-002: Sales Transaction
- Description: Sistem harus menyimpan setiap transaksi penjualan dengan nomor transaksi unik dan label audit yang jelas.
- Actor: Cashier, Store Manager
- Preconditions: Shift aktif, stok valid, user berhak melakukan transaksi.
- Trigger: Customer checkout.
- Main Flow: Cari produk > tambahkan ke cart > validasi harga dan kuantitas > pilih metode pembayaran > simpan transaksi.
- Alternative Flow: Split payment, diskon khusus, atau voucher.
- Exception Flow: Stok tidak cukup, pembayaran gagal, total melebihi limit, atau data produk tidak valid.
- Business Rules:
  - Transaksi yang sudah disimpan tidak bisa dihapus permanen.
  - Refund dan void harus memiliki otorisasi yang mengacu pada kebijakan approval.
  - Setiap perubahan kuantitas atau harga harus tercatat dalam audit trail.
- Input Requirements: produk, qty, harga, diskon, pajak, metode pembayaran, cabang, shift.
- Output Requirements: transaction ID, receipt, perubahan stok, dan entri jurnal terkait.
- Validation: Harga, diskon, pembayaran, dan status shift harus valid secara business rule.
- Permission Requirements: POS_CREATE_SALE, POS_APPROVE_DISCOUNT, POS_REFUND
- Acceptance Criteria: Transaksi tersimpan dengan ID unik, stok menyesuaikan, jurnal dibuat, dan receipt dapat dicetak.

### 7.3 Product Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-PROD-001 | Product Master | High |
| FR-PROD-002 | SKU & Barcode | High |
| FR-PROD-003 | Price List Management | High |
| FR-PROD-004 | Promotion and Discount Policy | Medium |

#### FR-PROD-001: Product Master
- Setiap produk harus memiliki master data minimal: SKU, barcode, nama, kategori, unit, supplier default, harga, status aktif, dan audit metadata.
- Produk tidak boleh aktif bila atribut dasar hilang, kecuali dalam status draft.

### 7.4 Inventory Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-INV-001 | Stock Availability | Critical |
| FR-INV-002 | Inventory Adjustment | High |
| FR-INV-003 | Stock Aging | Medium |
| FR-INV-004 | Inventory Valuation | High |

#### FR-INV-001: Stock Availability
- Sistem harus menolak transaksi penjualan atau pengeluaran stok yang melebihi kuantitas yang tersedia, kecuali mekanisme adjustment atau approval yang sah.
- Status stok harus dapat dilihat per cabang, gudang, dan SKU.

### 7.5 Stock Control, Tracking & Cycle Count

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-SCT-001 | Stock Ledger | Critical |
| FR-SCT-002 | Stock Transfer | High |
| FR-SCT-003 | Cycle Count | High |
| FR-SCT-004 | Discrepancy Resolution | High |

#### FR-SCT-001: Stock Ledger
- Setiap mutasi stok harus masuk ke ledger append-only.
- Ledger harus mencatat tanggal, SKU, lokasi, tipe pergerakan, referensi dokumen, kuantitas, dan actor.
- Tidak boleh ada penghapusan transaksi yang mengubah saldo historis.

### 7.6 Warehouse Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-WH-001 | Warehouse Master | High |
| FR-WH-002 | Goods Receipt | High |
| FR-WH-003 | Stock Allocation | Medium |
| FR-WH-004 | Transfer Confirmation | High |

#### FR-WH-002: Goods Receipt
- Goods receipt harus memvalidasi data PO, supplier, kuantitas, kualitas, dan lokasi penyimpanan.
- Setelah diterima, stok baru harus tersedia dengan penambahan ledger yang benar.

### 7.7 Distribution & Stock Transfer

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-DIST-001 | Stock Transfer Request | High |
| FR-DIST-002 | Transfer Approval | High |
| FR-DIST-003 | Transfer Execution | High |
| FR-DIST-004 | Transfer Reconciliation | Medium |

#### FR-DIST-002: Transfer Approval
- Transfer antar lokasi harus melalui alur persetujuan berdasarkan kebijakan cabang dan aturan kuantitas.
- Transfer yang disetujui harus dijaga agar tidak kehilangan status pelacakan dalam proses.

### 7.8 Finance Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-FIN-001 | General Journal Posting | Critical |
| FR-FIN-002 | Cash Reconciliation | High |
| FR-FIN-003 | Accounts Receivable / Payable | High |
| FR-FIN-004 | Financial Closing | High |

#### FR-FIN-001: General Journal Posting
- Setiap transaksi bisnis utama harus menghasilkan entri jurnal yang konsisten dengan persamaan dasar akuntansi.
- Posting tidak boleh duplikat untuk referensi yang sama tanpa idempotency key atau mekanisme pengenalan unik.

### 7.9 Human Resources

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-HR-001 | Employee Management | High |
| FR-HR-002 | Attendance | High |
| FR-HR-003 | Shift Management | High |
| FR-HR-004 | Payroll Processing | Medium |

#### FR-HR-004: Payroll Processing
- Payroll harus diproses dari data absensi, shift, dan kebijakan kompensasi yang terstandarisasi.
- Perubahan data master karyawan dan komponen gaji harus diberi catatan audit.

### 7.10 Internal Audit

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-AUD-001 | Audit Log Access | High |
| FR-AUD-002 | Audit Finding Record | High |
| FR-AUD-003 | Compliance Review | High |
| FR-AUD-004 | Independent Review Rights | High |

#### FR-AUD-001: Audit Log Access
- Auditor harus memiliki akses baca terhadap log transaksi, perubahan data, dan keputusan otorisasi.
- Akses tidak boleh mengubah atau memperbarui data historis.

### 7.11 Procurement & Supplier Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-PROC-001 | Supplier Master | High |
| FR-PROC-002 | Purchase Requisition | High |
| FR-PROC-003 | Purchase Order | High |
| FR-PROC-004 | Goods Receipt | High |
| FR-PROC-005 | Supplier Invoice Matching | Medium |

#### FR-PROC-005: Supplier Invoice Matching
- Proses matching antara invoice, PO, dan goods receipt harus mampu mengidentifikasi selisih kuantitas atau nilai sebelum pembayaran.

### 7.12 Branch Management

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-BR-001 | Branch Master | High |
| FR-BR-002 | Branch User Assignment | High |
| FR-BR-003 | Branch Performance KPI | High |

### 7.13 Approval & Workflow

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-APP-001 | Approval Request | High |
| FR-APP-002 | Approval Routing | High |
| FR-APP-003 | Escalation | High |
| FR-APP-004 | Approval History | High |

#### FR-APP-001: Approval Request
- Sistem harus dapat membuat approval request berdasarkan event bisnis tertentu seperti discount, refund, stock adjustment, or transfer.
- Setiap request harus memiliki scope, requester, approver, status, alasan, dan TTL approval.

### 7.14 Business Intelligence & Reporting

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-BI-001 | Dashboard Reporting | High |
| FR-BI-002 | Export and PDF | High |
| FR-BI-003 | Drilldown | Medium |
| FR-BI-004 | Data Warehouse / Snapshot | Medium |

#### FR-BI-001: Dashboard Reporting
- Dashboard harus menampilkan KPI utama untuk penjualan, stok, kas, AP/AR, dan sangka volume performances.
- Data harus bersumber dari transaksi yang tervalidasi dan tidak memerlukan proses manual.

### 7.15 System Administration & Security

| Requirement ID | Requirement Name | Priority |
|---|---|---|
| FR-SEC-001 | User and Role Management | Critical |
| FR-SEC-002 | Permission Management | Critical |
| FR-SEC-003 | Authentication Policy | Critical |
| FR-SEC-004 | Audit Trail | Critical |

#### FR-SEC-001: User and Role Management
- Admin dapat membuat, memblokir, menonaktifkan, atau memodifikasi akun pengguna.
- Setiap akun harus terikat pada role dan scope cabang/warehouse tertentu.

## 8. Non-Functional Requirements

| ID | Requirement | Description |
|---|---|---|
| NFR-001 | Performance | POS and dashboard operations should respond under 2s for standard transactional workloads |
| NFR-002 | Availability | Services essential for sales and inventory availability target 99.9% |
| NFR-003 | Security | Sensitive operations require authorization, MFA for privileged roles, and secure transport |
| NFR-004 | Auditability | Every critical event writes immutable audit log with actor and timestamp |
| NFR-005 | Scalability | System supports growth across branches, warehouses, and transaction volume |
| NFR-006 | Reliability | Transactions are atomic and support rollback or compensating action on failure |
| NFR-007 | Maintainability | Architecture and code follow modular boundaries and documentation standards |
| NFR-008 | Data Integrity | Stock, finance, and approval data use validated business rules and reconciliation checks |
| NFR-009 | Observability | Logs, metrics, and traces are available for incident and performance monitoring |
| NFR-010 | Recoverability | Backup and restore plan supports restoration of critical services within defined RTO |

## 9. Business Rules and Policy Constraints

1. A transaction is considered valid only when all mandatory fields and business validations pass.
2. Stock cannot become negative without an approved adjustment or documented exception.
3. Cash and financial postings must reconcile before period close.
4. Approval routing must be based on role, branch, and threshold policy.
5. Refund, discount override, and stock correction require distinct authority levels.
6. Internal audit access is read-only and cannot change transactional history.
7. User identity and session will be invalidated after password reset, role change, or privilege revocation.
8. Data anonymization and minimization must be applied to personal data handling.
9. Every critical event must include source actor, timestamp, transaction reference, and result status.
10. Business users cannot bypass backend validation through UI or direct API calls.

## 10. Data Requirements

- Master data: product, customer, supplier, employee, branch, warehouse, user, role.
- Transactional data: sales, refund, receiving, transfer, adjustment, journal, payroll.
- Audit data: log entries, approval history, change events, access records.
- Reporting data: summary snapshot, aggregation, dashboard metrics, export dataset.
- Data retention requirements must respect legal and operational obligations for employee and customer information.

## 11. Acceptance Criteria

### 11.1 Critical Release Acceptance Criteria
- No open critical defects related to cash, stock, authentication, or approval.
- All critical business flows pass end-to-end and API contract tests.
- Transactions affecting ledger, stock, or financial state produce traceable evidence.
- Unauthorized access attempts are denied and logged.
- UAT sign-off is completed by product owner and relevant business stakeholders.

### 11.2 Feature Acceptance Examples
- POS sale flow can complete with valid stock and payment data and generate receipt.
- Refund flow requires approver with valid authorization and creates audit evidence.
- Goods receipt updates stock ledger and triggers finance/warehouse workflow.
- Dashboard shows KPI from valid source data and supports export.

## 12. Traceability Matrix Summary

| Business Need | SRS | Architecture | Data | API | UI | Security | QA |
|---|---|---|---|---|---|---|---|
| POS sales integrity | FR-POS-002 | SAD | DDD | API | UX | SEC | QA |
| Stock accuracy | FR-SCT-001, FR-INV-001 | SAD | DDD | API | UX | SEC | QA |
| Finance correctness | FR-FIN-001 | SAD | DDD | API | UX | SEC | QA |
| Approval governance | FR-APP-001 | SAD | DDD | API | UX | SEC | QA |
| Auditability | FR-AUD-001, FR-SEC-004 | SAD | DDD | API | UX | SEC | QA |
| Executive insights | FR-EXC-001, FR-BI-001 | SAD | DDD | API | UX | SEC | QA |

## 13. Assumptions and Open Decisions

| Item | Status |
|---|---|
| Final cloud provider | TBD |
| Payroll scope finalization | TBD |
| Discount/refund threshold policy | TBD |
| Employee data retention schedule | TBD |
| Multi-warehouse operational policy | Assumed per branch model |

## 14. References

- MPS-VCP-001
- SAD-VCP-001
- DDD-VCP-001
- API-VCP-001
- SEC-VCP-001
- QA-VCP-001
- TDCM-VCP-001

---

This document is intended to be used as the governing requirement baseline for VAPECORE POS implementation and quality validation.
- Menjamin data stok dan keuangan konsisten antar modul.
- Memastikan approval untuk transaksi kritis.
- Mendorong kontrol internal dan pemisahan tugas.

## 9. Business Rules

1. Setiap transaksi penjualan menghasilkan entri stock ledger dan financial posting jika relevan.
2. Transaksi selesai tidak dapat dihapus permanen.
3. Barang yang tidak tersedia tidak dapat dijual.
4. Approval diperlukan untuk diskon melebihi threshold.
5. User hanya dapat mengakses data berdasarkan cabang/warehouse/role.
6. Audit log bersifat immutable.

## 10. User Stories

- Sebagai cashier, saya ingin proses checkout cepat agar transaksi selesai tepat waktu.
- Sebagai store manager, saya ingin melihat perbedaan stok agar dapat menangani issue inventory.
- Sebagai finance, saya ingin semua jurnal dapat ditelusuri agar rekonsiliasi akurat.
- Sebagai internal audit, saya ingin melihat riwayat semua perubahan agar proses audit lebih efektif.

## 11. Use Cases

### UC-01 Sales Transaction
- Actors: Cashier, Customer
- Goal: Menyelesaikan checkout.

### UC-02 Stock Adjustment
- Actors: Store Manager, Stock Control
- Goal: Koreksi stok sesuai hasil audit atau selisih.

### UC-03 Purchase Order Approval
- Actors: Head of Procurement, Manager
- Goal: Menyetujui order pembelian.

## 12. User Journey

1. User login.
2. Akses modul sesuai role.
3. Operasi bisnis dijalankan.
4. Sistem memvalidasi input.
5. Transaksi disimpan dan audit log dibuat.
6. User menerima status dan hasil.

## 13. Approval Requirements

- Discount > threshold -> approval by Department Head.
- Refund > threshold -> approval by Manager.
- Stock transfer antar warehouse -> approval by Warehouse Manager.
- Purchase order > budget -> approval by finance + procurement head.

## 14. Role and Permission Requirements

| Role | Example Permissions |
|---|---|
| cashier | POS_CREATE_SALE, POS_REFUND_LIMITED |
| store_manager | INVENTORY_VIEW, STOCK_ADJUST_APPROVE |
| finance_manager | FINANCE_POST_JOURNAL, RECONCILE_CASH |
| procurement_head | PO_APPROVE, SUPPLIER_MANAGE |
| internal_audit | AUDIT_READ, AUDIT_EXPORT |
| executive | EXECUTIVE_DASHBOARD, REPORT_EXPORT |

## 15. Notification Requirements

- Low stock warning.
- Payment failure alert.
- Approval pending alert.
- Cash variance alert.
- Security event alert.

## 16. Reporting Requirements

- Daily sales summary.
- Product movement report.
- Stock discrepancy report.
- Financial ledger report.
- Audit log review report.

## 17. Validation Rules

- Quantity cannot be negative.
- Discount must be within allowed range.
- Payment must match total amount.
- Stock transfer cannot exceed available stock.
- Date/time must use Asia/Jakarta timezone.

## 18. Exception Handling

- Payment gateway timeout -> mark pending and retry.
- Data conflict during sync -> queue reconciliation.
- Approval timeout -> escalate by policy.
- Invalid inventory adjustment -> reject and log reason.

## 19. Acceptance Criteria

- Semua transaksi utama dapat dibuat dan ditelusuri.
- Setiap perubahan stok menghasilkan ledger.
- Setiap dokumen keuangan berdampak pada ledger.
- User tanpa izin gagal di backend.
- Audit log tersedia untuk semua operasi sensitif.

## 20. Requirement Traceability Matrix

| Requirement ID | Module | Related Entity | Test Case |
|---|---|---|---|
| FR-POS-002 | POS | sales_transaction | TC-POS-001 |
| FR-SCT-001 | Inventory | stock_ledger | TC-SCT-001 |
| FR-FIN-001 | Finance | financial_journal | TC-FIN-001 |
| FR-SEC-004 | Security | audit_log | TC-SEC-001 |
| FR-APP-001 | Approval | approval_request | TC-APP-001 |

---

## 21. References

- MPS-VCP-001
- SAD-VCP-001
- DDD-VCP-001
- API-VCP-001
