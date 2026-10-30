# BUSINESS PROCESS & SOP DOCUMENT

Document ID: SOP-VCP-001
Version: 1.1.0
Status: Baseline
Project: VAPECORE POS
Owner: Operations & Process Excellence Team

---

## 1. Business Process Overview

Dokumen SOP ini menetapkan tata kelola proses operasional utama VAPECORE POS agar aktivitas bisnis terdokumentasi, konsisten, diaudit, dan dapat dikendalikan. Setiap proses harus memiliki owner, kontrol, bukti, serta mekanisme eskalasi bila terjadi deviasi.

Tujuan SOP adalah menegakkan prinsip segregation of duties, memastikan proses operasional tidak tergantung pada satu individu, dan menjaga integritas data transaksional serta financial.

## 2. Organization Structure

| Position | Department | Responsibilities |
|---|---|---|
| Board / Owner | Executive | Strategic direction and policy approval |
| Executive Manager | Management | Performance monitoring and escalation |
| Finance Manager | Finance | Ledger, cash, closing, and accounting review |
| Store Manager | Store Operations | Daily sales oversight, stock control, cash reconciliation |
| Warehouse Manager | Warehouse | Receiving, transfer, stock accuracy, inventory audit |
| Procurement Manager | Procurement | Purchase requisition, supplier coordination, PO approval |
| HR Manager | HR | Employee lifecycle, attendance, payroll, shift control |
| Internal Audit Lead | Audit | Independence review, control testing |
| System Administrator | IT / Security | User provisioning, logs, access governance |

## 3. Department Responsibilities

- Store Operations: sales transactions, cash handling, issue resolution, receipt management.
- Warehouse: receiving, storage, transfer, cycle count, discrepancy handling.
- Finance: AP/AR, journal posting, reconciliation, period close.
- HR: attendance capture, shift assignment, payroll, offboarding.
- Procurement: PR, PO, supplier evaluation, invoice verification.
- Audit: independent review of log integrity and control compliance.

## 4. Operational Authority Matrix

| Role | Authority |
|---|---|
| Cashier | Create sales, print receipt, open/close shift, accept valid payment |
| Store Manager | Approve discount, refund, stock adjustment, and cash variance escalation |
| Warehouse Staff | Receive goods, do stock movement, support cycle count |
| Warehouse Manager | Approve transfer, receiving discrepancies, and operational warehouse decisions |
| Procurement Officer | Create PR and PO, reject invalid supplier invoice |
| Finance Manager | Review journals, reconcile cash, approve closing |
| HR Manager | Approve attendance and payroll allocation |
| Internal Audit | Read-only review of logs and transactions |
| System Admin | Provision accounts, revoke access, maintain audit configuration |

## 5. Segregation of Duties

Proses ini harus dijaga tanpa adanya single-point control yang memungkinkan pelanggaran atau fraud.

- Cashier tidak dapat menyetujui refund atau override discount yang dibuat sendiri.
- User yang membuat purchase order tidak boleh menjadi approver default untuk PO yang sama.
- Petugas gudang tidak boleh menyetujui transfer yang dikerjakan sendiri tanpa approval sanering.
- Internal audit tidak dapat mengubah data historis transaksi.
- User dengan akses ke pembelian tidak otomatis diberikan hak untuk menyetujui pembayaran.

## 6. Approval Matrix

| Activity | Requestor | Approver | Threshold |
|---|---|---|---|
| POS discount | Cashier | Store Manager | Above limit |
| Refund | Cashier | Store Manager | Above limit |
| Stock adjustment | Store Manager | Warehouse or Finance Manager | Above tolerance |
| Stock transfer | Warehouse | Warehouse Manager | All |
| Purchase order | Procurement | Procurement Head / Finance | Budget threshold |
| Journal posting | Finance | Finance Manager | All |
| Payroll | HR | HR Manager / Finance | All |
| User access role change | Admin | Security Admin / Owner | All |

## 7. Standard Operating Procedures

### SOP-POS-001: Sales Transaction
- Purpose: Ensure correct sale execution and revenue recording.
- Scope: Store cashier and POS terminal.
- Responsible Department: Store Operations.
- Authorized Roles: cashier, store_manager.
- Procedure Steps:
  1. Login to POS using registered account.
  2. Validate shift status and open cash float.
  3. Search product or scan SKU/barcode.
  4. Validate quantity, price, and discount rule.
  5. Capture payment and print receipt.
  6. Save transaction, update stock ledger, and post journal event.
- Approval Requirements: discount and refund require manager approval beyond threshold.
- Control Points: stock validation, payment method check, receipt generation, ledger update.
- Exception Handling: failed payment, stock insufficiency, invalid discount, and duplicate transaction reference.
- Evidence: transaction record, receipt, cash count, audit log.

### SOP-POS-002: Refund and Void
- Initiate refund request with original transaction reference.
- Check customer eligibility, payment method, and settlement status.
- Route request to authorized approver.
- If approved, create compensation entry and update ledger.
- Audit all steps and retain supporting documents.

### SOP-CASH-001: Opening Cash
- Verify opening float amount before shift begins.
- Record the cash float in cashier shift data.
- Validate by store manager or designated supervisor.
- Save evidence of opening cash count and approval.

### SOP-CASH-002: Closing Cash
- Count actual cash at end of shift.
- Compare with expected value from sales and refunds.
- Document variance and escalate when beyond threshold.
- Close shift after manager confirmation and record final reconciliation.

## 8. Inventory and Warehouse Procedures

### SOP-INV-001: Goods Receiving
- Match goods receipt with PO and supplier delivery note.
- Check quantity, condition, and label accuracy.
- Record receiving result in receiving log.
- Update stock ledger and receiving status.
- Escalate if mismatch or damaged goods are detected.

### SOP-INV-002: Stock Adjustment
- Initiate adjustment request with reason code and supporting evidence.
- Validate difference against tolerance level.
- Obtain approval if threshold exceeds policy.
- Post adjustment transaction to stock ledger and finance ledger where applicable.
- Save approval and evidence as audit package.

### SOP-TRF-001: Internal Transfer
1. Create transfer request from source warehouse or branch.
2. Validate stock availability and destination capacity.
3. Route for approval according to transfer policy.
4. Execute transfer when approved.
5. Update source and destination stock ledger.
6. Reconcile receiving side confirmation.

### SOP-CYCLE-001: Cycle Count
- Schedule counting based on product risk and warehouse frequency.
- Count inventory at selected location and time.
- Compare system quantity with physical count.
- Record variance and create discrepancy ticket.
- Manager reviews and approves correction before system posting.

## 9. Finance and Procurement Procedures

### SOP-FIN-001: Journal Posting
- Journal entries are created only for valid business events.
- Finance verifies account selections, amount, and source document.
- If duplicate or inconsistent, reject and escalate to finance manager.

### SOP-FIN-002: Period Closing
- Prepare closing checklist for sales, cash, stock, AR/AP, and payroll.
- Reconcile ledger with operational records.
- Manager approval is required before final closure.

### SOP-PROC-001: Purchase Requisition and PO
- Procurement prepares requisition with justification and budget reference.
- Buyer creates purchase order and approves according to delegated authority.
- Supplier invoice is matched to PO and receipt before final payment.
- All actions are retained in approval and invoice logs.

## 10. HR and Attendance Process

### SOP-HR-001: Employee Onboarding
- Create employee record with role, branch assignment, and employment data.
- Validate employment documents and assign access rights.
- Configure shift and attendance rules.

### SOP-HR-002: Attendance and Shift
- Attendance captured by time clock or mobile validation.
- Shift assignment reviewed by manager.
- Payroll input generated only after attendance approval.

## 11. Internal Audit and Compliance

### SOP-AUD-001: Audit Review
- Auditor reviews logs, transactions, and approval evidence for selected period.
- Findings are classified by severity, root cause, and corrective action.
- Evidence and final disposition retained for review.

### SOP-AUD-002: Control Testing
- Test key controls around sales, stock movement, cash reconciliation, and access management.
- Failures trigger corrective action request with due owner.

## 12. Incident Handling and Escalation

| Incident Type | Response |
|---|---|
| Payment failure | Retry if safe, document failure, notify support and finance |
| Stock discrepancy | Freeze affected product, investigate, approve correction |
| Unauthorized access | Disable account, review logs, notify security lead |
| Invoice mismatch | Escalate procurement and finance review |
| Cash variance | Document variance and seek manager approval |

### Escalation Levels
- Severity 1: Immediate alert to system admin, operations leader, and management.
- Severity 2: Notify department head and relevant owner within the same business day.
- Severity 3: Resolve by operational owner with documentation.

## 13. Service Levels and KPIs

| KPI | Target |
|---|---|
| Sales transaction completion rate | > 99% |
| Stock variance | < 0.5% |
| Cash variance | < 0.1% |
| Approval SLA | < 2 hours |
| Audit finding closure | > 90% within timeline |
| Incident response SLA | Depends on severity and service category |

## 14. Evidence and Records

Setiap proses operasional harus menyimpan bukti yang cukup untuk review dan audit. Bukti dapat berupa:
- transaction log
- receipt or invoice
- approval note
- discrepancy ticket
- screenshot or exported report
- signed reconciliation form

## 15. Related Documents

- MPS-VCP-001
- SAD-VCP-001
- SRS-VCP-001
- DDD-VCP-001
- API-VCP-001
- SEC-VCP-001
- QA-VCP-001
- DEVOPS-VCP-001
- TDCM-VCP-001

---

## 16. Review and Governance

- SOP harus direview minimal per kuartal atau ketika terjadi perubahan proses signifikan.
- Update prosedur harus dicatat dan disetujui oleh pemilik proses.
- Jika perubahan memengaruhi keamanan, data sensitivitas, atau kontrol akuntansi, maka harus di-review bersama security dan finance.

