# ProfileNest API - Combined Announcement and User API

## Overview

The **ProfileNest API** (`profilenest-api.yaml`) is a unified OpenAPI 3.0.3 specification that combines the Announcement API and User API into a single comprehensive API contract for managing user profiles and announcements in the Zimesfield platform.

## File Structure

```
api-specs/
├── profilenest-api.yaml          # Combined API specification (163 lines)
├── announcement-api.yaml         # Original announcement API
├── user-api.yaml                 # Original user API
├── paths/
│   ├── announcement/             # 8 announcement endpoint files
│   └── user/                     # 9 user endpoint files
└── common/
    └── components/
        ├── announcement/         # Announcement schemas
        └── user/                 # User schemas
```

## API Components

### 1. **Info & Metadata**
- **Title**: ProfileNest API
- **Version**: 1.0.0
- **Description**: REST API for managing user profiles and announcements
- **License**: Apache 2.0

### 2. **Servers** (3 configurations)
- **Development**: `http://localhost:8082/api`
- **Production**: `https://api.zimesfield.com/api`
- **User Service**: `{protocol}://{environment}/services/user` (with variables for localhost, dev, staging, prod)

### 3. **Tags** (5 categories)
- **Announcements**: Announcement management operations
- **Register**: User registration
- **Authenticate**: User authentication
- **Account**: User account management
- **Admin**: Administrative user operations

### 4. **Security Schemes** (3 options)
- **oauth2**: Implicit flow for announcements (scopes: read, write, delete)
- **oauth**: Authorization code flow with Keycloak (scopes: openid, email, profile)
- **openId**: OpenID Connect with Keycloak configuration

### 5. **Paths** (17 total endpoints)

#### Announcement Endpoints (8)
- `POST /announcements` - Create announcement
- `GET /announcements/{announcementId}` - Get announcement
- `PUT /announcements/{announcementId}` - Update announcement
- `POST /announcements/{announcementId}/publish` - Publish announcement
- `POST /announcements/{announcementId}/archive` - Archive announcement
- `GET /announcements/published` - List published announcements
- `GET /announcements/pinned` - List pinned announcements
- `GET /announcements/category/{category}` - Filter by category
- `GET /announcements/creator/{creatorId}` - Filter by creator

#### User Endpoints (9)
- `POST /internal/auth/authenticate` - Authenticate user
- `GET /api/admin/users/{login}` - Get managed user
- `GET /api/activate` - Activate user account
- `GET /api/authenticated` - Check authentication status
- `GET /api/account` - Get user account
- `POST /api/register` - Register new user
- `POST /api/account/change-password` - Change password
- `POST /api/account/reset-password/init` - Initiate password reset
- `POST /api/account/reset-password/finish` - Complete password reset

### 6. **Schemas** (17 total)

#### Announcement Schemas (7)
- `CreateAnnouncementRequest`, `UpdateAnnouncementRequest`, `PublishAnnouncementRequest`
- `AnnouncementResponse`, `AnnouncementStatus`, `PageMetadata`, `ErrorResponse`

#### User Schemas (9)
- `User`, `ManagedUserVM`, `PasswordChangeDTO`, `KeyAndPasswordVM`
- `UserDTO`, `LoginVM`, `JWTToken`, `Problem`

#### Shared Schema (1)
- `Problem` (from common schemas)

## Key Features

✅ **Unified API Contract** - Single specification for both user and announcement management
✅ **Modular Architecture** - Maintains separate endpoint and schema files for easy maintenance
✅ **Multi-Server Support** - Supports different environments and service architectures
✅ **Flexible Security** - Multiple authentication options (OAuth2, OpenID Connect)
✅ **Comprehensive Coverage** - All user lifecycle and announcement workflow operations
✅ **Consistent Structure** - Follows OpenAPI best practices and existing patterns

## Usage

The `profilenest-api.yaml` can be used for:
- **Code Generation**: Generate client/server code for both user and announcement APIs
- **API Documentation**: Generate unified documentation (Swagger UI, etc.)
- **Mock Servers**: Create mock implementations for testing
- **API Validation**: Validate requests/responses against the combined schema
- **Integration**: Import into API management tools, Postman collections, etc.

## File Size
- **profilenest-api.yaml**: 163 lines (~4.9KB)
- **Total Combined**: All referenced files maintain their original sizes and structure

This unified API specification provides a complete contract for building applications that need both user management and announcement functionality in the Zimesfield platform.
