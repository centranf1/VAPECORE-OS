# API TECHNICAL SPECIFICATION

Document ID: API-VCP-001
Version: 1.0.0
Status: Baseline
Project: VAPECORE POS
Owner: Backend Architecture Team
Base URL: /api/v1

---

## 1. API Overview

API VAPECORE POS menyediakan seluruh layanan backend untuk modul POS, inventory, warehouse, finance, HR, approval, reporting, dan security. API dirancang untuk menjalankan transaksi operasi bisnis secara aman, konsisten, transparan, dan mudah diaudit. Semua request dan response mengikuti format yang terdokumentasi agar frontend, integrator, dan sistem eksternal dapat berinteraksi dengan pola yang konsisten.

## 2. API Standards

- Base URL: `/api/v1`
- Content-Type: `application/json`
- Response format standardized
- All timestamps in ISO-8601 with timezone
- UTF-8 encoding
- Structured error payload
- Idempotency support on all mutating endpoints
- Correlation ID on each request for tracing

## 3. REST API Architecture

### 3.1 Architectural Design

- Resource-oriented REST endpoints
- HTTP verbs: GET, POST, PUT, PATCH, DELETE
- Soft delete for business records when required
- Event-driven side effects from transactional services
- Clear separation between read models and command operations

### 3.2 API Responsibilities

- Validate input and business rules
- Check role and branch scope
- Commit transactional data
- Emit events for downstream consumers
- Record audit logs for sensitive actions

## 4. API Versioning

- Versioning via path: `/api/v1/...`
- Breaking changes require new version release
- Backward compatibility maintained where feasible
- Version-specific documentation generated from code

## 5. Authentication

- JWT access token in Authorization header
- Refresh token rotation
- Session expiration policy
- MFA for privileged roles
- Re-authentication on suspicious or changed session context

## 6. Authorization

- Role-based permission model
- Branch and warehouse scope enforcement
- Resource ownership validation
- Backend enforcement mandatory; frontend permission only for user experience

## 7. Request Standards

### 7.1 Request Headers

| Header | Required | Description |
|---|---|---|
| Authorization | Yes | Bearer token |
| Content-Type | Yes | application/json |
| X-Request-Id | Recommended | Correlation ID |
| Idempotency-Key | Conditional | Required for mutating operations |
| X-Tenant-Id | Conditional | For multi-tenant scenarios |

### 7.2 Query Parameters

| Parameter | Purpose |
|---|---|
| page | Pagination index |
| limit | Row count |
| sort | Sort field |
| order | asc / desc |
| filter | Business filter |
| fromDate | Lower time range |
| toDate | Upper time range |

## 8. Response Standards

### 8.1 Success Response

```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "status": "COMPLETED"
  },
  "meta": {
    "requestId": "req_123",
    "timestamp": "2026-10-30T12:00:00+07:00"
  }
}
```

### 8.2 Error Response

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Quantity must be greater than zero",
    "details": [
      { "field": "qty", "issue": "Must be > 0" }
    ]
  },
  "meta": {
    "requestId": "req_123",
    "timestamp": "2026-10-30T12:00:00+07:00"
  }
}
```

## 9. Error Handling

| Error Code | Meaning |
|---|---|
| VALIDATION_ERROR | Input failed validation |
| AUTH_REQUIRED | Missing or invalid token |
| FORBIDDEN | Not authorized |
| NOT_FOUND | Resource not found |
| CONFLICT | Duplicate or invalid state |
| RATE_LIMITED | Too many requests |
| INTERNAL_ERROR | Unhandled server error |

## 10. Validation Standards

- All validation occurs server-side
- Business validation before commit
- DTO-based schema validation
- Rejections for invalid price, quantity, dates, and status transitions

## 11. Pagination

### Standard Query Parameters
- `page` default 1
- `limit` default 20, max 100

### Example response

```json
{
  "data": [],
  "meta": {
    "page": 1,
    "limit": 20,
    "totalItems": 120,
    "totalPages": 6
  }
}
```

## 12. Filtering

The API supports searches such as:
- branchId
- warehouseId
- status
- dateFrom
- dateTo
- productId
- supplierId
- userId

## 13. Sorting

- Sorting allowed only on whitelisted fields
- Example: `?sort=createdAt&order=desc`

## 14. Rate Limiting

| Endpoint Class | Limit |
|---|---|
| Public auth endpoints | 10 req/min |
| General API | 200 req/min |
| Sensitive endpoints | 50 req/min |

## 15. Idempotency

Required for:
- POS sale creation
- Payment settlement
- Refund processing
- Stock transfer approval/confirmation
- Journal posting
- Supplier sync operations

Use `Idempotency-Key` header for POST/PUT/PATCH where safe.

## 16. Transaction Handling

- Use DB transaction for all financial and stock-altering commands.
- Commit only after validation and authorization succeed.
- Record audit event after successful state change.
- Use outbox or message queue for downstream event propagation.

## 17. Webhook Architecture

### Event Examples
- payment.status.updated
- stock.transfer.approved
- approval.requested
- report.export.completed
- supplier.invoice.received

### Webhook Security
- HMAC signature validation
- Replay protection via timestamp and nonce
- Retry with exponential backoff

## 18. API Security

- TLS 1.2+
- Strict CORS policy
- Secret management and rotation
- Sensitive endpoints require backend validation
- Protection against injection, enumeration, and abuse patterns

## 19. API Documentation

- OpenAPI/Swagger generated from NestJS decorators
- Request examples included
- Permission and auth requirements documented at endpoint level
- Version-specific docs retained for each release

## 20. Endpoint Catalog

### 20.1 Authentication

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| POST | `/api/v1/auth/login` | Login user | No | Public |
| POST | `/api/v1/auth/refresh` | Refresh access token | No | Public |
| POST | `/api/v1/auth/logout` | Logout session | Yes | AUTH_LOGOUT |

### 20.2 Users and Roles

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/users` | List users | Yes | USER_READ |
| POST | `/api/v1/users` | Create user | Yes | USER_CREATE |
| PATCH | `/api/v1/users/:id` | Update user | Yes | USER_UPDATE |
| GET | `/api/v1/roles` | List roles | Yes | ROLE_READ |

### 20.3 POS

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| POST | `/api/v1/pos/transactions` | Create sales transaction | Yes | POS_CREATE_SALE |
| GET | `/api/v1/pos/transactions/:id` | Get transaction detail | Yes | POS_READ |
| POST | `/api/v1/pos/refunds` | Process refund | Yes | POS_REFUND |
| POST | `/api/v1/pos/voids` | Void transaction | Yes | POS_VOID |
| GET | `/api/v1/pos/shifts/:id` | Shift detail | Yes | SHIFT_READ |
| POST | `/api/v1/pos/shifts/open` | Open cashier shift | Yes | SHIFT_OPEN |
| POST | `/api/v1/pos/shifts/close` | Close cashier shift | Yes | SHIFT_CLOSE |

### 20.4 Product

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/products` | List products | Yes | PRODUCT_READ |
| POST | `/api/v1/products` | Create product | Yes | PRODUCT_CREATE |
| PATCH | `/api/v1/products/:id` | Update product | Yes | PRODUCT_UPDATE |
| GET | `/api/v1/products/:id/stock` | Get stock info | Yes | STOCK_READ |

### 20.5 Inventory and Warehouse

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/inventory/ledger` | Stock ledger | Yes | STOCK_LEDGER_READ |
| POST | `/api/v1/inventory/adjustments` | Stock adjustment | Yes | STOCK_ADJUST |
| POST | `/api/v1/warehouse/transfers` | Create stock transfer | Yes | STOCK_TRANSFER_CREATE |
| PATCH | `/api/v1/warehouse/transfers/:id/approve` | Approve transfer | Yes | STOCK_TRANSFER_APPROVE |
| POST | `/api/v1/cycle-counts` | Create cycle count | Yes | CYCLE_COUNT_CREATE |
| POST | `/api/v1/warehouse/receipts` | Goods receipt | Yes | GOODS_RECEIPT_CREATE |

### 20.6 Finance

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/finance/journals` | List journal | Yes | FINANCE_JOURNAL_READ |
| POST | `/api/v1/finance/journals` | Post journal | Yes | FINANCE_POST_JOURNAL |
| GET | `/api/v1/finance/ledger` | General ledger | Yes | FINANCE_LEDGER_READ |
| POST | `/api/v1/finance/reconciliation` | Cash reconciliation | Yes | CASH_RECONCILE |

### 20.7 Procurement

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/procurement/suppliers` | List suppliers | Yes | SUPPLIER_READ |
| POST | `/api/v1/procurement/purchase-orders` | Create PO | Yes | PO_CREATE |
| PATCH | `/api/v1/procurement/purchase-orders/:id/approve` | Approve PO | Yes | PO_APPROVE |
| POST | `/api/v1/procurement/goods-receipts` | Receive goods | Yes | GR_CREATE |

### 20.8 Approval

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/approvals/requests` | List approval requests | Yes | APPROVAL_READ |
| POST | `/api/v1/approvals/requests` | Create approval request | Yes | APPROVAL_CREATE |
| PATCH | `/api/v1/approvals/requests/:id/approve` | Approve request | Yes | APPROVAL_APPROVE |

### 20.9 Reporting

| Method | Endpoint | Description | Auth | Permission |
|---|---|---|---|---|
| GET | `/api/v1/reports/dashboard` | Dashboard metrics | Yes | REPORT_DASHBOARD |
| GET | `/api/v1/reports/financial` | Financial report | Yes | REPORT_FINANCE |
| GET | `/api/v1/reports/inventory` | Inventory report | Yes | REPORT_INVENTORY |

---

## 21. Example Request / Response

### Create Sales Transaction

Request:

```http
POST /api/v1/pos/transactions
Authorization: Bearer <token>
Idempotency-Key: pos-transaction-001
Content-Type: application/json
```

```json
{
  "branchId": "b1",
  "cashierId": "u1",
  "items": [
    { "productId": "p1", "qty": 2, "unitPrice": 150000 }
  ],
  "payments": [
    { "method": "QRIS", "amount": 300000 }
  ]
}
```

Response:

```json
{
  "success": true,
  "data": {
    "transactionId": "txn_001",
    "transactionNo": "POS-2026-0001",
    "status": "COMPLETED"
  }
}
```

## 22. Security Notes

- Protect all write endpoints with authorization.
- Audit every sensitive operation.
- Use parameterized queries and DTO validation.
- Validate permissions before DB write.
- Record correlation ID for cross-system traceability.

## 23. Open Questions

- Detailed payment gateway specification.
- Exact branch and warehouse scope.
- Discount and refund thresholds.
- Multi-tenant strategy timeline.

## 24. References

- MPS-VCP-001
- SAD-VCP-001
- SRS-VCP-001
- DDD-VCP-001
- SEC-VCP-001

