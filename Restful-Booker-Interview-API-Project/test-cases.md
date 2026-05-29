# API Test Cases

## Authentication

| Test Case ID | Scenario | Method | Endpoint | Test Data | Expected Result |
|---|---|---|---|---|---|
| RB_AUTH_001 | Generate token with valid credentials | POST | `/auth` | username `admin`, password `password123` | Status 200, token is generated |
| RB_AUTH_002 | Generate token with invalid credentials | POST | `/auth` | wrong username/password | API returns failure reason |
| RB_AUTH_003 | Validate token is saved | POST | `/auth` | valid credentials | Token is stored in environment variable |

## Positive Booking Scenarios

| Test Case ID | Scenario | Method | Endpoint | Test Data | Expected Result |
|---|---|---|---|---|---|
| RB_BOOK_001 | Get all booking IDs | GET | `/booking` | NA | Status 200, response is array |
| RB_BOOK_002 | Create booking with valid data | POST | `/booking` | valid booking body | Status 200, booking ID is generated |
| RB_BOOK_003 | Get created booking by ID | GET | `/booking/:id` | saved booking ID | Status 200, booking details returned |
| RB_BOOK_004 | Update booking with token | PUT | `/booking/:id` | valid token and body | Status 200, booking is updated |
| RB_BOOK_005 | Partially update booking | PATCH | `/booking/:id` | valid token and partial body | Status 200, selected fields updated |
| RB_BOOK_006 | Delete booking with token | DELETE | `/booking/:id` | valid token | Status 201 or successful delete response |

## API Chaining

| Test Case ID | Scenario | Source API | Target API | Expected Result |
|---|---|---|---|---|
| RB_CHAIN_001 | Save token from auth API | POST `/auth` | PUT/PATCH/DELETE booking | Token is reused successfully |
| RB_CHAIN_002 | Save booking ID from create booking API | POST `/booking` | GET `/booking/:id` | Created booking is fetched |
| RB_CHAIN_003 | Use booking ID in update API | POST `/booking` | PUT `/booking/:id` | Same booking is updated |

## Schema Validation

| Test Case ID | Scenario | Endpoint | Expected Result |
|---|---|---|---|
| RB_SCHEMA_001 | Validate create booking response schema | POST `/booking` | Response has bookingid and booking object |
| RB_SCHEMA_002 | Validate booking object schema | GET `/booking/:id` | firstname, lastname, totalprice, depositpaid, bookingdates, additionalneeds fields are correct types |
| RB_SCHEMA_003 | Validate booking ID list schema | GET `/booking` | Response is array of objects with bookingid number |

## Negative Scenarios

| Test Case ID | Scenario | Method | Endpoint | Expected Result |
|---|---|---|---|---|
| RB_NEG_001 | Get booking with invalid ID | GET | `/booking/999999999` | Status 404 |
| RB_NEG_002 | Update booking without token | PUT | `/booking/:id` | Status 403 |
| RB_NEG_003 | Delete booking without token | DELETE | `/booking/:id` | Status 403 |
| RB_NEG_004 | Update booking with invalid token | PUT | `/booking/:id` | Status 403 |
| RB_NEG_005 | Create booking with invalid/missing data | POST | `/booking` | API should reject or return server error depending on demo API behavior |

## Defect Reporting Example

If invalid login returns `200 OK` with a failure message, report it like this:

```text
Title: Invalid login returns 200 OK instead of 401 Unauthorized
Steps:
1. Send POST /auth with invalid credentials.
2. Observe status code and response.
Actual Result:
API returns 200 OK with reason "Bad credentials".
Expected Result:
API should return 401 Unauthorized or 400 Bad Request according to API standards.
Impact:
Client applications may treat failed login as successful because of 200 status.
```

