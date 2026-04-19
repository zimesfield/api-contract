# Announcement API - OpenAPI Specification Collection

This directory contains a modular OpenAPI 3.0.3 specification for the Announcement API in the Zimesfield platform.

## Directory Structure

```
api-specs/
├── announcement-api.yaml                    # Main API definition (root entry point)
├── paths/
│   └── announcement/
│       ├── create.yaml                      # POST /announcements
│       ├── get-update.yaml                  # GET/PUT /announcements/{announcementId}
│       ├── publish.yaml                     # POST /announcements/{announcementId}/publish
│       ├── archive.yaml                     # POST /announcements/{announcementId}/archive
│       ├── published.yaml                   # GET /announcements/published
│       ├── pinned.yaml                      # GET /announcements/pinned
│       ├── category.yaml                    # GET /announcements/category/{category}
│       └── creator.yaml                     # GET /announcements/creator/{creatorId}
└── common/
    └── components/
        └── announcement/
            └── schema.yaml                  # All schema definitions
```

## File Descriptions

### Main API File
- **announcement-api.yaml**: Root OpenAPI specification that defines servers, tags, and references all paths and schemas.

### Path Definitions
Each file in `paths/announcement/` contains operation definitions:

1. **create.yaml**
   - `POST /announcements`: Create a new announcement in draft status
   - Returns: AnnouncementResponse (201 Created)

2. **get-update.yaml**
   - `GET /announcements/{announcementId}`: Retrieve an announcement by ID
   - `PUT /announcements/{announcementId}`: Update draft or scheduled announcement
   - Returns: AnnouncementResponse (200 OK)

3. **publish.yaml**
   - `POST /announcements/{announcementId}/publish`: Publish an announcement
   - Returns: AnnouncementResponse (200 OK)

4. **archive.yaml**
   - `POST /announcements/{announcementId}/archive`: Archive a published announcement
   - Returns: AnnouncementResponse (200 OK)

5. **published.yaml**
   - `GET /announcements/published`: List published announcements (paginated)
   - Returns: Array of AnnouncementResponse with PageMetadata

6. **pinned.yaml**
   - `GET /announcements/pinned`: Get pinned announcements
   - Returns: Array of AnnouncementResponse

7. **category.yaml**
   - `GET /announcements/category/{category}`: List announcements by category (paginated)
   - Returns: Array of AnnouncementResponse with PageMetadata

8. **creator.yaml**
   - `GET /announcements/creator/{creatorId}`: List announcements by creator (paginated)
   - Returns: Array of AnnouncementResponse with PageMetadata

### Schema Definitions
**common/components/announcement/schema.yaml** contains:

- **CreateAnnouncementRequest**: Required fields for creating announcements
- **UpdateAnnouncementRequest**: Optional fields for updating announcements
- **PublishAnnouncementRequest**: Fields for publishing announcements
- **AnnouncementResponse**: Complete announcement data model
- **AnnouncementStatus**: Enum (DRAFT, SCHEDULED, PUBLISHED, ARCHIVED)
- **PageMetadata**: Pagination information
- **ErrorResponse**: Error response structure

## Key Features

✅ **Modular Design**: Each endpoint is defined in a separate file for maintainability
✅ **Schema Reusability**: All schemas are centralized in a single file and referenced throughout
✅ **Consistent Structure**: Follows the same pattern as tenant API definitions
✅ **Security**: OAuth2 security scheme applied to all endpoints
✅ **Pagination Support**: List endpoints support pagination with page and size parameters
✅ **Tenant Isolation**: X-Tenant-ID header required on all endpoints
✅ **Comprehensive Error Responses**: Standard error response schema for all failures

## Usage

The `announcement-api.yaml` can be used to:
- Generate API client code
- Generate API server stubs
- Generate API documentation
- Validate API requests/responses
- Generate mock servers

## Supported Servers

- **Development**: `http://localhost:8082/api`
- **Production**: `https://api.zimesfield.com/api`

## Security Scheme

OAuth2 with implicit flow is configured with the following scopes:
- `read:announcements` - Read announcements
- `write:announcements` - Create and modify announcements
- `delete:announcements` - Delete announcements

