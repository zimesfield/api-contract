# Attendance API - OpenAPI Specification Collection

This directory contains a modular OpenAPI 3.0.3 specification for the Attendance API in the Zimesfield platform, following the same structure as the User API.

## Directory Structure

```
api-specs/
├── attendance-api.yaml                    # Main API definition (root entry point)
├── paths/
│   └── attendance/
│       ├── checkin.yaml                   # POST /attendance/checkin
│       ├── checkout.yaml                  # POST /attendance/checkout
│       ├── get-update-attendance.yaml     # GET/PUT /attendance/{attendanceId}
│       ├── attendance-by-user.yaml        # GET /attendance/user/{userId}
│       └── attendance-by-status.yaml      # GET /attendance/status/{status}
└── common/
    └── components/
        └── attendance/
            └── schema.yaml               # All schema definitions
```

## File Descriptions

### Main API File
- **attendance-api.yaml**: Root OpenAPI specification that defines servers, tags, and references all paths and schemas.

### Path Definitions
Each file in `paths/attendance/` contains operation definitions:

1. **checkin.yaml**
   - `POST /attendance/checkin`: Check in a user
   - Returns: AttendanceResponse (201 Created)

2. **checkout.yaml**
   - `POST /attendance/checkout`: Check out a user
   - Returns: AttendanceResponse (200 OK)

3. **get-update-attendance.yaml**
   - `GET /attendance/{attendanceId}`: Retrieve attendance record by ID
   - `PUT /attendance/{attendanceId}`: Update attendance status
   - Returns: AttendanceResponse (200 OK)

4. **attendance-by-user.yaml**
   - `GET /attendance/user/{userId}`: List attendance records for a user (paginated, date-filtered)
   - Returns: Array of AttendanceResponse with PageMetadata

5. **attendance-by-status.yaml**
   - `GET /attendance/status/{status}`: List attendance records by status (paginated, date-filtered)
   - Returns: Array of AttendanceResponse with PageMetadata

### Schema Definitions
**common/components/attendance/schema.yaml** contains:

- **CheckInRequest**: Required fields for user check-in (userId, location)
- **CheckOutRequest**: Required fields for user check-out (userId)
- **UpdateAttendanceStatusRequest**: Fields for updating attendance status
- **AttendanceResponse**: Complete attendance record data model
- **PageMetadata**: Pagination information
- **ErrorResponse**: Standard error response structure

## Key Features

✅ **Modular Design**: Each endpoint is defined in a separate file for maintainability
✅ **Schema Reusability**: All schemas are centralized in a single file and referenced throughout
✅ **Consistent Structure**: Follows the same pattern as user and other APIs
✅ **Security**: OAuth2 security scheme applied to all endpoints
✅ **Pagination Support**: List endpoints support pagination with page/size parameters
✅ **Tenant Isolation**: X-Tenant-ID header required on all endpoints
✅ **Advanced Filtering**: Date range filtering on user attendance queries
✅ **Status Management**: Support for PRESENT, ABSENT, LATE, EXCUSED statuses

## Attendance Status Types

- **PRESENT**: User is present/checked in
- **ABSENT**: User is absent
- **LATE**: User arrived late
- **EXCUSED**: User has excused absence

## Check-in/Check-out Workflow

1. **Check-in**: User provides userId, location, optional device/notes
2. **Check-out**: User provides userId, optional notes
3. **Status Updates**: Admin can update status to ABSENT, LATE, EXCUSED
4. **Querying**: Filter by user, status, date ranges with pagination

## Usage

The `attendance-api.yaml` can be used to:
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
- `read:attendance` - Read attendance records
- `write:attendance` - Create and modify attendance records
- `checkin:attendance` - Check in users
- `checkout:attendance` - Check out users

## File Sizes

- attendance-api.yaml: 163 lines (~1.9KB)
- Endpoint files: 1161-2500 lines (5 files total ~9KB)
- schema.yaml: 3055 lines (~3KB)
- Total: ~14KB modular specification

## Integration Notes

- **Device Tracking**: Optional device field for audit trails
- **Location Tracking**: Required location field for check-ins
- **Notes Support**: Optional notes for check-in, check-out, and status updates
- **Time Tracking**: Automatic timestamps for check-in/check-out times
- **Conflict Prevention**: Prevents double check-ins/check-outs

This Attendance API specification provides a complete contract for managing user attendance tracking, including check-in/check-out workflows, status management, and comprehensive querying capabilities with advanced filtering options.
