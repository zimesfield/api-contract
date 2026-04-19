# ProfileNest API - Complete Unified API Specification

## Overview

The **ProfileNest API** (`profilenest-api.yaml`) is now a comprehensive unified OpenAPI 3.0.3 specification that combines **four complete API domains** into a single, cohesive API contract for the Zimesfield platform.

## API Domains Integrated

### 1. **Announcements API** (8 endpoints)
- Create, publish, archive announcements
- Status workflow: DRAFT → SCHEDULED → PUBLISHED → ARCHIVED
- Advanced filtering by category, creator, status
- Pagination support

### 2. **User API** (9 endpoints)
- User registration and authentication
- Account management (password changes, resets)
- Admin user operations
- Keycloak OAuth2 integration

### 3. **Financial API** (7 endpoints)
- Transaction recording and management
- Verification and reversal workflows
- Advanced filtering by contributor, category, type, date ranges
- Multiple transaction types: DONATION, CONTRIBUTION, EXPENSE, INCOME, TRANSFER

### 4. **Attendance API** (5 endpoints)
- Check-in/check-out functionality
- Status management: PRESENT, ABSENT, LATE, EXCUSED
- User and status-based querying with date filters
- Device and location tracking

## File Structure

```
api-specs/
├── profilenest-api.yaml                    # Unified API specification (233 lines)
├── paths/
│   ├── announcement/                      # 8 announcement endpoint files
│   ├── user/                              # 9 user endpoint files
│   ├── financial/                         # 7 financial endpoint files
│   └── attendance/                        # 5 attendance endpoint files
└── common/
    └── components/
        ├── announcement/                  # Announcement schemas
        ├── user/                          # User schemas
        ├── financial/                     # Financial schemas
        └── attendance/                    # Attendance schemas
```

## Complete Endpoint Inventory

### Announcements (8 endpoints)
- `POST /announcements` - Create announcement
- `GET/PUT /announcements/{id}` - Get/update announcement
- `POST /announcements/{id}/publish` - Publish announcement
- `POST /announcements/{id}/archive` - Archive announcement
- `GET /announcements/published` - List published (paginated)
- `GET /announcements/pinned` - List pinned
- `GET /announcements/category/{cat}` - Filter by category (paginated)
- `GET /announcements/creator/{id}` - Filter by creator (paginated)

### User Management (9 endpoints)
- `POST /internal/auth/authenticate` - Authenticate user
- `GET /api/admin/users/{login}` - Get managed user
- `GET /api/activate` - Activate account
- `GET /api/authenticated` - Check authentication
- `GET /api/account` - Get account info
- `POST /api/register` - Register user
- `POST /api/account/change-password` - Change password
- `POST /api/account/reset-password/init` - Initiate reset
- `POST /api/account/reset-password/finish` - Complete reset

### Financial Transactions (7 endpoints)
- `POST /financial/transactions` - Record transaction
- `GET /financial/transactions/{id}` - Get transaction
- `POST /financial/transactions/{id}/verify` - Verify transaction
- `POST /financial/transactions/{id}/reverse` - Reverse transaction
- `GET /financial/transactions/contributor/{id}` - By contributor (filtered/paginated)
- `GET /financial/transactions/category/{cat}` - By category (filtered/paginated)
- `GET /financial/transactions/type/{type}` - By type (filtered/paginated)

### Attendance Tracking (5 endpoints)
- `POST /attendance/checkin` - Check in user
- `POST /attendance/checkout` - Check out user
- `GET/PUT /attendance/{id}` - Get/update attendance record
- `GET /attendance/user/{id}` - By user (filtered/paginated)
- `GET /attendance/status/{status}` - By status (filtered/paginated)

## Security & Authentication

### Security Schemes (3 options)
- **oauth2**: Implicit flow with comprehensive scopes
- **oauth**: Keycloak authorization code flow
- **openId**: OpenID Connect with Keycloak

### OAuth2 Scopes (11 total)
- **Announcements**: read, write, delete
- **Financial**: read, write, verify, reverse
- **Attendance**: read, write, checkin, checkout

## API Tags (7 categories)
- Announcements, Register, Authenticate, Account, Admin, Financial, Attendance

## Servers (3 configurations)
- **Development**: `http://localhost:8082/api`
- **Production**: `https://api.profilenext.com/api`
- **User Service**: `{protocol}://{environment}/services/user` (with variables)

## Schema Inventory (25+ schemas)

### Announcement Schemas (7)
- Create/Update/Publish requests, Response, Status, PageMetadata, ErrorResponse

### User Schemas (9)
- User, ManagedUserVM, PasswordChangeDTO, KeyAndPasswordVM, UserDTO, LoginVM, JWTToken, Problem

### Financial Schemas (5)
- Record/Verify/Reverse requests, Response, Status

### Attendance Schemas (4)
- CheckIn/CheckOut/Update requests, Response

### Shared Schemas (2)
- PageMetadata, ErrorResponse (reused across domains)

## Key Features

✅ **Unified API Contract** - Single specification for all platform functionality
✅ **Modular Architecture** - Each domain maintains separate files for easy maintenance
✅ **Consistent Security** - Unified authentication across all domains
✅ **Advanced Filtering** - Date ranges, pagination, status filters throughout
✅ **Workflow Support** - Status lifecycles for announcements, financial transactions, attendance
✅ **Tenant Isolation** - X-Tenant-ID headers on all endpoints
✅ **Comprehensive Coverage** - User management, content, finance, and attendance tracking

## Usage

The `profilenest-api.yaml` can be used for:
- **Code Generation**: Generate client/server code for all APIs
- **API Documentation**: Generate unified documentation (Swagger UI, etc.)
- **Mock Servers**: Create mock implementations for testing
- **API Validation**: Validate requests/responses against the complete schema
- **Integration**: Import into API management tools, Postman collections, etc.

## File Statistics

- **profilenest-api.yaml**: 233 lines (~7.1KB) - Unified specification
- **Individual APIs**: 4 separate API files (announcement, user, financial, attendance)
- **Endpoint Files**: 29 total endpoint definition files
- **Schema Files**: 4 domain-specific schema files
- **Total Modular Files**: 37 files across all APIs

## Integration Benefits

- **Single Source of Truth**: One API specification for the entire platform
- **Consistent Patterns**: Unified security, pagination, error handling
- **Easy Maintenance**: Modular structure allows independent updates
- **Developer Experience**: Single import for all platform APIs
- **Documentation**: Unified API documentation and testing

This ProfileNest API specification provides a complete, production-ready contract for building comprehensive applications that require user management, content management, financial tracking, and attendance monitoring in the Zimesfield platform.
