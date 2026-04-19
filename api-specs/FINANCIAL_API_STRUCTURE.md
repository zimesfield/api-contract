# Financial API - OpenAPI Specification Collection

This directory contains a modular OpenAPI 3.0.3 specification for the Financial API in the Zimesfield platform, following the same structure as the User API.

## Directory Structure

```
api-specs/
├── financial-api.yaml                    # Main API definition (root entry point)
├── paths/
│   └── financial/
│       ├── record-transaction.yaml       # POST /financial/transactions
│       ├── get-transaction.yaml          # GET /financial/transactions/{transactionId}
│       ├── verify-transaction.yaml       # POST /financial/transactions/{transactionId}/verify
│       ├── reverse-transaction.yaml      # POST /financial/transactions/{transactionId}/reverse
│       ├── transactions-by-contributor.yaml # GET /financial/transactions/contributor/{contributorId}
│       ├── transactions-by-category.yaml # GET /financial/transactions/category/{category}
│       └── transactions-by-type.yaml     # GET /financial/transactions/type/{transactionType}
└── common/
    └── components/
        └── financial/
            └── schema.yaml               # All schema definitions
```

## File Descriptions

### Main API File
- **financial-api.yaml**: Root OpenAPI specification that defines servers, tags, and references all paths and schemas.

### Path Definitions
Each file in `paths/financial/` contains operation definitions:

1. **record-transaction.yaml**
   - `POST /financial/transactions`: Record a new financial transaction
   - Returns: FinancialTransactionResponse (201 Created)

2. **get-transaction.yaml**
   - `GET /financial/transactions/{transactionId}`: Retrieve transaction by ID
   - Returns: FinancialTransactionResponse (200 OK)

3. **verify-transaction.yaml**
   - `POST /financial/transactions/{transactionId}/verify`: Verify/approve transaction
   - Returns: FinancialTransactionResponse (200 OK)

4. **reverse-transaction.yaml**
   - `POST /financial/transactions/{transactionId}/reverse`: Reverse/cancel transaction
   - Returns: FinancialTransactionResponse (200 OK)

5. **transactions-by-contributor.yaml**
   - `GET /financial/transactions/contributor/{contributorId}`: List transactions by contributor (paginated, filtered)
   - Returns: Array of FinancialTransactionResponse with PageMetadata

6. **transactions-by-category.yaml**
   - `GET /financial/transactions/category/{category}`: List transactions by category (paginated, filtered)
   - Returns: Array of FinancialTransactionResponse with PageMetadata

7. **transactions-by-type.yaml**
   - `GET /financial/transactions/type/{transactionType}`: List transactions by type (paginated, filtered)
   - Returns: Array of FinancialTransactionResponse with PageMetadata

### Schema Definitions
**common/components/financial/schema.yaml** contains:

- **RecordFinancialTransactionRequest**: Required fields for recording transactions
- **VerifyFinancialTransactionRequest**: Fields for transaction verification
- **ReverseFinancialTransactionRequest**: Fields for transaction reversal
- **FinancialTransactionResponse**: Complete transaction data model
- **FinancialTransactionStatus**: Enum (PENDING, VERIFIED, REVERSED, CANCELLED)
- **PageMetadata**: Pagination information
- **ErrorResponse**: Standard error response structure

## Key Features

✅ **Modular Design**: Each endpoint is defined in a separate file for maintainability
✅ **Schema Reusability**: All schemas are centralized in a single file and referenced throughout
✅ **Consistent Structure**: Follows the same pattern as user and announcement APIs
✅ **Security**: OAuth2 security scheme applied to all endpoints
✅ **Pagination Support**: List endpoints support pagination with page/size parameters
✅ **Tenant Isolation**: X-Tenant-ID header required on all endpoints
✅ **Advanced Filtering**: Date range and status filtering on list endpoints
✅ **Transaction Workflow**: Supports PENDING → VERIFIED → REVERSED/CANCELLED lifecycle

## Transaction Types

- **DONATION**: Charitable contributions
- **CONTRIBUTION**: General contributions
- **EXPENSE**: Organizational expenses
- **INCOME**: General income
- **TRANSFER**: Internal transfers

## Payment Methods

- **CASH**: Cash payments
- **CHECK**: Check payments
- **CREDIT_CARD**: Credit card payments
- **BANK_TRANSFER**: Bank transfers
- **ONLINE**: Online payments
- **OTHER**: Other payment methods

## Usage

The `financial-api.yaml` can be used to:
- Generate API client code
- Generate API server stubs
- Generate API documentation
- Validate API requests/responses
- Generate mock servers

## Server Endpoints

- **Development**: `http://localhost:8082/api`
- **Production**: `https://api.zimesfield.com/api`

## Security Scheme

OAuth2 with implicit flow is configured with the following scopes:
- `read:financial` - Read financial transactions
- `write:financial` - Create and modify financial transactions
- `verify:financial` - Verify financial transactions
- `reverse:financial` - Reverse financial transactions

## File Sizes

- financial-api.yaml: 163 lines (~2.5KB)
- Endpoint files: 950-1888 lines (7 files total ~10KB)
- schema.yaml: 5855 lines (~5.8KB)
- Total: ~18.3KB modular specification

This Financial API specification provides a complete contract for managing financial transactions, including recording, verification, reversal, and comprehensive querying capabilities with advanced filtering options.
