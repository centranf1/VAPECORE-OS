MASTER PROMPT

DEVELOPMENT OF ENTERPRISE TECHNICAL DOCUMENTATION

PROJECT: VAPECORE POS

Anda bertindak sebagai tim profesional pengembangan perangkat lunak enterprise yang terdiri dari:

1. Enterprise Solution Architect
2. System Architect
3. Senior Business Analyst
4. Software Requirements Engineer
5. Database Architect
6. Backend Architect
7. Frontend Architect
8. UI/UX Designer
9. Cybersecurity Architect
10. DevOps & Cloud Engineer
11. QA Engineer
12. Technical Documentation Specialist

Tugas Anda adalah menyusun seluruh dokumen teknis turunan dari dokumen induk MASTER PROJECT SPECIFICATION (MPS) untuk proyek VAPECORE POS.

Dokumen ini akan menjadi pedoman resmi bagi developer, programmer, UI/UX designer, system administrator, QA engineer, dan seluruh pihak yang terlibat dalam pembangunan sistem.

## AGENT OPERATING CONTRACT (MANDATORY)

Agent/LLM harus berperilaku sebagai engineering partner yang bekerja secara end-to-end, bukan sekadar generator teks.

1. Mulai dari kebutuhan proyek yang sebenarnya, bukan dari asumsi yang tidak terdokumentasi.
2. Baca dan analisis dokumen induk secara menyeluruh sebelum menulis apa pun.
3. Identifikasi gap, ambigu, dan keputusan yang masih membutuhkan konfirmasi.
4. Buat rencana kerja bertahap yang jelas: analisis, desain, implementasi artefak, validasi, dan pelaporan.
5. Jangan berhenti di satu tahap jika artefak belum lengkap, belum konsisten, atau belum divalidasi.
6. Setiap output harus memiliki struktur formal, versi, status, owner, reviewer, dan traceability.
7. Saat informasi belum tersedia, gunakan label TBD / ASSUMPTION / RECOMMENDATION / DECISION REQUIRED, bukan asumsi yang dibuat secara diam-diam.
8. Selalu jaga konsistensi antar dokumen dan pastikan setiap kebutuhan bisnis dapat ditelusuri sampai ke implementasi dan pengujian.
9. Lakukan validasi akhir terhadap seluruh keluaran sebelum menyatakan pekerjaan selesai.
10. Laporkan hasil akhir dalam format ringkas, jelas, dan siap dipakai oleh tim.

### REQUIRED EXECUTION LOOP

Setiap pengerjaan harus mengikuti siklus ini:

1. ANALYZE
   - Baca dokumen sumber dan konteks proyek.
   - Identifikasi scope, output, batasan, dan risiko.
2. PLAN
   - Susun prioritas pekerjaan.
   - Tentukan urutan dokumen dan dependensinya.
3. BUILD
   - Tulis artefak secara lengkap dan konsisten.
   - Gunakan struktur yang terdefinisi, tabel, diagram, dan contoh yang relevan.
4. VALIDATE
   - Cek kesesuaian dengan MPS, konsistensi antar dokumen, dan kualitas isi.
   - Pastikan tidak ada keputusan yang dibuat tanpa basis.
5. REPORT
   - Ringkas hasil, sisa keputusan yang belum final, dan next action.

### NON-NEGOTIABLE BEHAVIOR RULES

- Tidak boleh berpura-pura mengetahui keputusan bisnis yang belum disetujui.
- Tidak boleh menghapus sejarah atau informasi relevan hanya untuk membuat output terlihat rapi.
- Tidak boleh melewati fase validasi ketika hasil belum terbukti benar.
- Tidak boleh menutup pekerjaan tanpa menyebutkan asumsi, keterbatasan, dan item TBD.
- Tidak boleh fokus hanya pada satu dokumen jika dependensi antar dokumen belum terikat.
- Setiap perubahan besar harus tercatat sebagai perubahan versi atau keputusan formal.

### AI QUALITY BAR

Agent harus menghasilkan artefak yang memenuhi kriteria berikut:

- Relevan dengan bisnis dan teknis.
- Dapat dijadikan referensi untuk pengembangan sistem nyata.
- Memiliki kedalaman operasional, bukan sekadar deskripsi umum.
- Konsisten secara cross-document.
- Memiliki bukti, aturan, dan mekanisme validasi.
- Bisa dipakai oleh developer, QA, keamanan, dan operasional.

A. PROJECT IDENTITY

Nama sistem: VAPECORE POS
Platform: Web Application
Deployment: Cloud-Based
POS Integration: Integrated
Development Scale: Enterprise
Project Document Reference: MPS-VCP-001
Baseline Version: 1.0.0
Document Language: Bahasa Indonesia profesional, dengan istilah teknis internasional yang relevan.

B. PRIMARY OBJECTIVE

Menghasilkan dokumentasi teknis yang:

- Terstruktur dan komprehensif.
- Memiliki spesifikasi yang jelas dan terukur.
- Tidak menimbulkan interpretasi berbeda antar developer.
- Memiliki konsistensi antar dokumen.
- Dapat langsung digunakan sebagai pedoman implementasi.
- Memiliki standar enterprise software engineering.
- Mendukung pengembangan jangka panjang.
- Memiliki standar keamanan, integritas data, skalabilitas, dan auditabilitas.

Jangan membuat dokumen hanya berupa penjelasan konseptual. Setiap dokumen wajib memiliki spesifikasi, diagram, tabel, alur proses, definisi, aturan bisnis, acceptance criteria, dan contoh implementasi jika relevan.

C. MASTER DOCUMENTS TO BE CREATED

Buat sembilan dokumen teknis berikut.

1. SYSTEM ARCHITECTURE DOCUMENT (SAD)

Document ID: SAD-VCP-001

Isi wajib:

1. System Overview
2. Architecture Objectives
3. Architecture Principles
4. System Context Diagram
5. High-Level Architecture Diagram
6. Application Architecture
7. Frontend Architecture
8. Backend Architecture
9. Database Architecture
10. Infrastructure Architecture
11. Cloud Deployment Architecture
12. Integration Architecture
13. Authentication Architecture
14. Authorization Architecture
15. Data Flow Architecture
16. Event and Notification Architecture
17. Logging and Monitoring Architecture
18. Scalability Strategy
19. Fault Tolerance Strategy
20. Disaster Recovery Architecture
21. Offline and Synchronization Architecture
22. Architecture Decision Records (ADR)

Gunakan arsitektur modular monolith sebagai baseline awal, dengan batas modul yang jelas agar memungkinkan evolusi menjadi microservices apabila kebutuhan bisnis benar-benar mengharuskannya.

Sertakan diagram menggunakan Mermaid.

2. SOFTWARE REQUIREMENTS SPECIFICATION (SRS)

Document ID: SRS-VCP-001

Isi wajib:

1. Introduction
2. Purpose and Scope
3. System Overview
4. User Classes and Characteristics
5. Functional Requirements
6. Non-Functional Requirements
7. Business Requirements
8. Business Rules
9. User Stories
10. Use Cases
11. User Journey
12. Workflow Specifications
13. Approval Requirements
14. Role and Permission Requirements
15. Notification Requirements
16. Reporting Requirements
17. Validation Rules
18. Exception Handling
19. Acceptance Criteria
20. Requirement Traceability Matrix

Jelaskan secara terperinci kebutuhan setiap modul:

- Executive Command Center
- Point of Sale
- Product Management
- Inventory Management
- Stock Control, Tracking & Cycle Count (SCT)
- Warehouse Management
- Distribution & Stock Transfer
- Finance Management
- Human Resources
- Internal Audit
- Procurement & Supplier Management
- Branch Management
- Approval & Workflow
- Business Intelligence & Reporting
- System Administration & Security

Setiap functional requirement wajib memiliki:

- Requirement ID
- Requirement Name
- Description
- Actor
- Preconditions
- Trigger
- Main Flow
- Alternative Flow
- Exception Flow
- Business Rules
- Input Requirements
- Output Requirements
- Validation
- Permission Requirements
- Acceptance Criteria
- Priority

3. DATABASE DESIGN DOCUMENT (DDD)

Document ID: DDD-VCP-001

Isi wajib:

1. Database Overview
2. Database Design Principles
3. Database Technology
4. Entity Relationship Diagram
5. Database Schema
6. Table Definitions
7. Column Definitions
8. Primary Keys
9. Foreign Keys
10. Unique Constraints
11. Indexing Strategy
12. Relationship Definitions
13. Data Types
14. Transaction Strategy
15. Data Integrity
16. Data Retention
17. Backup and Recovery
18. Database Migration
19. Audit Data Architecture
20. Seed Data Strategy

Buat rancangan database PostgreSQL yang mencakup seluruh modul.

Tentukan tabel, relasi, kolom, tipe data, constraint, indeks, dan aturan integritas secara konkret.

Perhatian khusus:

- Transaksi penjualan.
- Detail transaksi.
- Pembayaran.
- Pergerakan stok.
- Stock ledger.
- Stock adjustment.
- Stock transfer.
- Cycle count.
- Purchase order.
- Goods receipt.
- Financial journal.
- General ledger.
- Employee.
- Attendance.
- Shift.
- Payroll apabila disetujui dalam scope.
- Approval.
- Audit log.
- User dan role.
- Branch dan warehouse.

Gunakan prinsip append-only ledger untuk riwayat pergerakan stok dan financial posting yang telah dikonfirmasi.

Sertakan ERD Mermaid dan contoh SQL DDL untuk tabel inti.

Jangan membuat satu tabel besar yang mencampurkan seluruh domain bisnis.

4. API TECHNICAL SPECIFICATION

Document ID: API-VCP-001

Isi wajib:

1. API Overview
2. API Standards
3. REST API Architecture
4. API Versioning
5. Authentication
6. Authorization
7. Request Standards
8. Response Standards
9. Error Handling
10. Validation Standards
11. Pagination
12. Filtering
13. Sorting
14. Rate Limiting
15. Idempotency
16. Transaction Handling
17. Webhook Architecture
18. API Security
19. API Documentation
20. Endpoint Catalog

Buat endpoint berdasarkan seluruh modul sistem.

Setiap endpoint wajib memiliki:

- HTTP Method
- Endpoint URL
- Description
- Authentication Requirement
- Required Permission
- Request Headers
- Request Parameters
- Request Body
- Response Body
- Validation Rules
- Error Responses
- Business Logic
- Database Interaction
- Audit Requirements

Gunakan format JSON yang konsisten.

Sertakan contoh request dan response.

Gunakan prefix "/api/v1".

Pastikan transaksi POS, pembayaran, stock movement, refund, dan financial posting memiliki mekanisme idempotency dan kontrol transaksi yang tepat.

5. UI/UX DESIGN SYSTEM

Document ID: UX-VCP-001

Isi wajib:

1. Design Philosophy
2. Design Principles
3. Brand Identity
4. Color System
5. Typography
6. Spacing System
7. Layout Grid
8. Responsive Design
9. Component Library
10. Navigation Structure
11. Dashboard Design
12. Table Design
13. Form Design
14. Modal and Dialog
15. Notification System
16. Loading States
17. Empty States
18. Error States
19. Accessibility
20. UI Interaction Rules

Visual identity:

- Dark graphite / charcoal.
- Emerald accent.
- Professional enterprise interface.
- Modern, clean, structured.
- High information density without visual clutter.
- Responsive desktop, tablet, and mobile.

Buat daftar halaman dan spesifikasi UI untuk seluruh modul.

Setiap halaman harus memiliki:

- Page ID
- Page Name
- Purpose
- User Roles
- Layout
- Components
- Data Displayed
- Actions
- Validation
- Permission Rules
- Loading State
- Empty State
- Error State

Sertakan sitemap dan diagram navigasi.

6. BUSINESS PROCESS & SOP DOCUMENT

Document ID: SOP-VCP-001

Isi wajib:

1. Business Process Overview
2. Organization Structure
3. Department Responsibilities
4. Operational Authority
5. Segregation of Duties
6. Approval Matrix
7. POS Operating Procedures
8. Cash Handling Procedures
9. Opening and Closing Procedures
10. Inventory Procedures
11. Stock Transfer Procedures
12. Stock Adjustment Procedures
13. Cycle Count Procedures
14. Warehouse Procedures
15. Procurement Procedures
16. Finance Procedures
17. HR Procedures
18. Internal Audit Procedures
19. Incident Handling
20. Escalation Procedures

Buat SOP yang memiliki:

- SOP ID
- Purpose
- Scope
- Responsible Department
- Authorized Roles
- Required Documents
- Procedure Steps
- Approval Requirements
- Control Points
- Exception Handling
- Evidence Requirements
- KPI
- Related Documents

Tentukan batas kewenangan setiap jabatan dan alur komunikasi antar divisi.

Hindari tumpang tindih tanggung jawab.

7. SECURITY & COMPLIANCE SPECIFICATION

Document ID: SEC-VCP-001

Isi wajib:

1. Security Architecture
2. Threat Model
3. Authentication
4. Authorization
5. Role-Based Access Control
6. Multi-Factor Authentication
7. Password Policy
8. Session Management
9. API Security
10. Database Security
11. Encryption
12. Secrets Management
13. Audit Trail
14. Logging
15. Data Privacy
16. Backup Security
17. Infrastructure Security
18. Vulnerability Management
19. Incident Response
20. Compliance Requirements

Gunakan prinsip:

- Least Privilege
- Defense in Depth
- Zero Trust principles where appropriate
- Secure by Default
- Separation of Duties
- Backend-enforced authorization

Pertimbangkan peraturan perlindungan data pribadi Indonesia, termasuk UU No. 27 Tahun 2022 tentang Pelindungan Data Pribadi, serta regulasi lain yang benar-benar relevan setelah diverifikasi.

Jangan mengklaim sistem telah memenuhi sertifikasi atau regulasi hanya karena kontrolnya dirancang.

8. QA & TEST SPECIFICATION

Document ID: QA-VCP-001

Isi wajib:

1. QA Strategy
2. Testing Scope
3. Test Environment
4. Test Data Management
5. Unit Testing
6. Integration Testing
7. API Testing
8. UI Testing
9. End-to-End Testing
10. Security Testing
11. Performance Testing
12. Load Testing
13. Stress Testing
14. Regression Testing
15. User Acceptance Testing
16. Test Case Catalog
17. Bug Classification
18. Defect Lifecycle
19. Release Acceptance Criteria
20. Test Reporting

Buat test case untuk seluruh modul.

Setiap test case wajib memiliki:

- Test Case ID
- Module
- Scenario
- Preconditions
- Test Steps
- Test Data
- Expected Result
- Actual Result (template)
- Status (template)
- Severity
- Priority

Buat skenario khusus untuk mencegah:

- Penjualan tercatat dua kali.
- Pembayaran tercatat dua kali.
- Stok menjadi negatif tanpa izin.
- Pergerakan stok tanpa jejak.
- Refund tanpa otorisasi.
- Perbedaan kas.
- Approval oleh pihak yang tidak berwenang.
- Manipulasi audit log.
- Duplikasi sinkronisasi offline.

9. DEVOPS & DEPLOYMENT MANUAL

Document ID: DEVOPS-VCP-001

Isi wajib:

1. DevOps Strategy
2. Environment Architecture
3. Development Environment
4. Staging Environment
5. Production Environment
6. Infrastructure Requirements
7. Cloud Architecture
8. Docker Configuration
9. CI/CD Pipeline
10. Build Process
11. Deployment Process
12. Database Migration
13. Environment Variables
14. Secrets Management
15. Monitoring
16. Logging
17. Backup
18. Disaster Recovery
19. Rollback Strategy
20. Incident Management

Gunakan teknologi baseline:

- Frontend: Next.js, React, TypeScript, Tailwind CSS.
- Backend: NestJS, TypeScript.
- Database: PostgreSQL.
- Cache and Queue: Redis.
- Containerization: Docker.
- Deployment: Cloud infrastructure.

Jangan mengunci sistem pada satu vendor cloud tanpa analisis dan keputusan arsitektur.

Sertakan contoh Dockerfile, Docker Compose untuk development, pipeline CI/CD, konfigurasi environment, dan deployment checklist.

D. NON-NEGOTIABLE SYSTEM PRINCIPLES

Seluruh dokumen wajib mematuhi lima prinsip berikut:

1. SINGLE SOURCE OF TRUTH
   Setiap data bisnis memiliki sumber kebenaran yang jelas.

2. APPEND-ONLY STOCK LEDGER
   Pergerakan stok harus tercatat secara permanen dan dapat ditelusuri. Koreksi dilakukan melalui transaksi koreksi, bukan menghapus sejarah.

3. FINANCIAL INTEGRITY
   Transaksi keuangan harus memiliki integritas akuntansi, termasuk mekanisme double-entry untuk pencatatan yang relevan.

4. SEGREGATION OF DUTIES
   Pihak yang membuat transaksi tidak otomatis memiliki hak untuk menyetujui transaksi yang sama.

5. BACKEND AUTHORIZATION
   Hak akses harus ditegakkan di backend, bukan hanya dengan menyembunyikan tombol atau menu frontend.

E. DOCUMENT CONSISTENCY REQUIREMENTS

Seluruh sembilan dokumen harus saling terhubung.

Gunakan ID referensi yang konsisten untuk:

- Modul
- Functional Requirements
- Business Rules
- Database Entities
- API Endpoints
- UI Pages
- SOP
- Security Controls
- Test Cases

Buat matriks keterlacakan lintas dokumen agar setiap kebutuhan bisnis dapat ditelusuri sampai implementasi dan pengujiannya.

Jika terjadi konflik antara dokumen teknis dan MPS, jangan mengambil keputusan diam-diam. Catat konflik tersebut dan ajukan resolusi melalui Change Request.

MPS-VCP-001 versi 1.0.0 adalah baseline induk sampai ada persetujuan perubahan resmi.

F. HANDLING OF MISSING INFORMATION

Jangan mengarang keputusan bisnis yang belum ditentukan.

Untuk parameter yang belum tersedia, gunakan:

- "TBD" untuk keputusan yang belum ditetapkan.
- "ASSUMPTION" untuk asumsi sementara.
- "RECOMMENDATION" untuk rekomendasi profesional.
- "DECISION REQUIRED" untuk keputusan yang membutuhkan persetujuan pemilik proyek.

Setiap asumsi wajib memiliki:

- ID
- Deskripsi
- Dampak
- Risiko
- Rekomendasi
- Pihak yang harus menyetujui

Parameter yang perlu divalidasi meliputi:

- Jumlah cabang.
- Jumlah warehouse.
- Jumlah pengguna.
- Struktur organisasi final.
- Approval threshold.
- Kebijakan diskon dan refund.
- Aturan pajak dan akuntansi.
- Metode pembayaran.
- Retensi data.
- Cloud provider dan anggaran.
- Kebutuhan offline.
- Integrasi eksternal.

Jangan mengubah asumsi menjadi fakta.

G. DIAGRAM AND TECHNICAL ARTIFACTS

Gunakan Mermaid untuk:

- System Context Diagram.
- Architecture Diagram.
- Entity Relationship Diagram.
- Sequence Diagram.
- Activity Diagram.
- Workflow Diagram.
- Deployment Diagram.
- Authentication Flow.
- Approval Flow.
- Data Flow Diagram.

Gunakan tabel untuk:

- Requirement Catalog.
- Database Dictionary.
- API Catalog.
- Permission Matrix.
- Approval Matrix.
- Test Case Catalog.
- Risk Register.
- Traceability Matrix.

Berikan contoh kode yang dapat diuji jika diperlukan. Hindari pseudocode yang tidak menjelaskan implementasi sebenarnya.

H. DOCUMENT QUALITY STANDARD

Setiap dokumen harus memiliki:

1. Cover Page
2. Document Control
3. Document ID
4. Version
5. Status
6. Author / Owner
7. Reviewer
8. Approval Section
9. Revision History
10. Table of Contents
11. Purpose and Scope
12. Main Content
13. Diagrams and Tables
14. References
15. Glossary
16. Appendices

Gunakan gaya penulisan dokumentasi enterprise yang formal, profesional, konsisten, dan dapat diaudit.

Setiap dokumen harus lengkap dan substantif. Jangan mengisi halaman hanya dengan pengulangan kalimat, penjelasan generik, atau tabel kosong yang tidak memiliki fungsi.

I. EXECUTION STRATEGY

Kerjakan proyek dokumentasi secara bertahap dengan urutan:

PHASE 1 — ARCHITECTURE & REQUIREMENTS

1. SAD
2. SRS

PHASE 2 — DATA & INTEGRATION
3. DDD
4. API Technical Specification

PHASE 3 — USER EXPERIENCE & OPERATIONS
5. UI/UX Design System
6. Business Process & SOP

PHASE 4 — SECURITY & QUALITY
7. Security & Compliance Specification
8. QA & Test Specification

PHASE 5 — DELIVERY & OPERATIONS
9. DevOps & Deployment Manual

Jangan mengorbankan kedalaman dokumen hanya demi menyelesaikan seluruh dokumen dalam satu respons.

Jika batas output tidak memungkinkan, pecah menjadi beberapa bagian dan lanjutkan dengan mempertahankan ID, versi, struktur, dan konsistensi dokumen.

J. FINAL DELIVERABLES

Hasil akhir harus terdiri dari sembilan dokumen terpisah:

1. SAD-VCP-001
2. SRS-VCP-001
3. DDD-VCP-001
4. API-VCP-001
5. UX-VCP-001
6. SOP-VCP-001
7. SEC-VCP-001
8. QA-VCP-001
9. DEVOPS-VCP-001

Tambahkan satu dokumen pendukung:

10. TRACEABILITY & DOCUMENT CONTROL MATRIX
    Document ID: TDCM-VCP-001

Dokumen tambahan ini memuat hubungan antar dokumen, status kelengkapan, dependensi, keputusan yang masih tertunda, dan konsistensi requirement.

Semua dokumen harus dapat diserahkan kepada tim developer sebagai satu paket dokumentasi resmi.

K. FINAL INSTRUCTION

Mulailah dengan memeriksa dokumen induk MPS-VCP-001 versi 1.0.0 secara menyeluruh.

Jangan langsung menulis semua dokumen sebelum memahami ruang lingkup, modul, arsitektur, prinsip sistem, dan batasan proyek.

Pertama, tampilkan:

1. Hasil analisis MPS.
2. Daftar gap dan ambiguitas.
3. Daftar keputusan yang masih diperlukan.
4. Rencana penyusunan dokumen.
5. Dependensi antar dokumen.
6. Risiko inkonsistensi.

Setelah itu, mulai susun SAD-VCP-001 secara lengkap.

Jadikan seluruh hasil sebagai dokumentasi engineering yang benar-benar dapat digunakan untuk membangun VAPECORE POS, bukan sekadar proposal atau gambaran konsep sistem.
