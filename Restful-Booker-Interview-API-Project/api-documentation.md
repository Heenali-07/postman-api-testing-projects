# API Documentation

This file is a sample API documentation document for the Restful Booker interview project.

In real projects, API documentation helps testers, developers, and automation engineers understand:

- Endpoint purpose
- HTTP method
- Request URL
- Path/query parameters
- Headers
- Authentication
- Request body
- Response body
- Status codes
- Test scenarios

## Base URL

```text
https://restful-booker.herokuapp.com
```

## Authentication

Protected update and delete APIs require authentication.

Restful Booker supports:

- Token using cookie header
- Basic Auth for some protected requests

Token format:

```text
Cookie: token={{token}}
```

Basic Auth:

```text
Username: admin
Password: password123
```

## 1. Health Check

### GET Ping

Purpose:

Check whether API server is running.

Request:

```text
GET /ping
```

Expected Status:

```text
201 Created
```

Test Points:

- Verify status code is 201.
- Verify response time is acceptable.

## 2. Create Token

### POST Auth

Purpose:

Generate authentication token.

Request:

```text
POST /auth
```

Headers:

```text
Content-Type: application/json
Accept: application/json
```

Request Body:

```json
{
  "username": "admin",
  "password": "password123"
}
```

Successful Response:

```json
{
  "token": "abc123"
}
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify status code is 200.
- Verify `token` field is present.
- Verify token is a non-empty string.
- Save token in environment variable.

Negative Scenario:

Send invalid credentials.

Expected Result:

API should not generate token. This demo API returns `200 OK` with reason `Bad credentials`, but in real APIs expected status is usually `401 Unauthorized`.

## 3. Get Booking IDs

### GET Booking

Purpose:

Fetch all booking IDs.

Request:

```text
GET /booking
```

Headers:

```text
Accept: application/json
```

Successful Response:

```json
[
  {
    "bookingid": 1
  },
  {
    "bookingid": 2
  }
]
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify response is an array.
- Verify each item has `bookingid`.
- Verify `bookingid` is a number.

## 4. Create Booking

### POST Booking

Purpose:

Create a new booking.

Request:

```text
POST /booking
```

Headers:

```text
Content-Type: application/json
Accept: application/json
```

Request Body:

```json
{
  "firstname": "Heenali",
  "lastname": "Raut",
  "totalprice": 2500,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2026-06-01",
    "checkout": "2026-06-05"
  },
  "additionalneeds": "Breakfast"
}
```

Successful Response:

```json
{
  "bookingid": 123,
  "booking": {
    "firstname": "Heenali",
    "lastname": "Raut",
    "totalprice": 2500,
    "depositpaid": true,
    "bookingdates": {
      "checkin": "2026-06-01",
      "checkout": "2026-06-05"
    },
    "additionalneeds": "Breakfast"
  }
}
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify booking ID is generated.
- Verify response body has `bookingid` and `booking`.
- Verify firstname, lastname, totalprice, depositpaid, bookingdates, and additionalneeds.
- Save `bookingid` for API chaining.
- Validate response schema.

## 5. Get Booking By ID

### GET Booking By ID

Purpose:

Fetch one booking using booking ID.

Request:

```text
GET /booking/{{bookingId}}
```

Headers:

```text
Accept: application/json
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify status code is 200.
- Verify response has booking details.
- Verify response schema.

Negative Scenario:

```text
GET /booking/999999999
```

Expected Status:

```text
404 Not Found
```

## 6. Update Booking

### PUT Booking

Purpose:

Fully update an existing booking.

Request:

```text
PUT /booking/{{bookingId}}
```

Headers:

```text
Content-Type: application/json
Accept: application/json
Cookie: token={{token}}
```

Request Body:

```json
{
  "firstname": "UpdatedHeenali",
  "lastname": "UpdatedLastName",
  "totalprice": 3500,
  "depositpaid": false,
  "bookingdates": {
    "checkin": "2026-07-01",
    "checkout": "2026-07-08"
  },
  "additionalneeds": "Dinner"
}
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify update works with valid token.
- Verify all updated fields.
- Verify request fails without token.
- Verify request fails with invalid token.

Negative Status:

```text
403 Forbidden
```

## 7. Partial Update Booking

### PATCH Booking

Purpose:

Update selected fields of booking.

Request:

```text
PATCH /booking/{{bookingId}}
```

Headers:

```text
Content-Type: application/json
Accept: application/json
Cookie: token={{token}}
```

Request Body:

```json
{
  "firstname": "PatchedName"
}
```

Expected Status:

```text
200 OK
```

Test Points:

- Verify only selected field is changed.
- Verify unchanged fields still exist.

## 8. Delete Booking

### DELETE Booking

Purpose:

Delete existing booking.

Request:

```text
DELETE /booking/{{bookingId}}
```

Headers:

```text
Cookie: token={{token}}
```

Expected Status:

```text
201 Created
```

Test Points:

- Verify booking is deleted with valid token.
- Verify delete fails without token.
- Verify delete fails with invalid token.
- Optionally call GET booking by same ID after delete and verify it is not found.

## Common Status Codes

| Status Code | Meaning | Example |
|---|---|---|
| 200 | OK | Auth success, get booking, update booking |
| 201 | Created | Ping, delete booking in this demo API |
| 400 | Bad Request | Invalid request body in many APIs |
| 401 | Unauthorized | Missing/invalid authentication in many APIs |
| 403 | Forbidden | Missing/invalid token for protected booking update/delete |
| 404 | Not Found | Invalid booking ID |
| 500 | Internal Server Error | Server issue or poorly handled invalid input |

## Interview Explanation

You can say:

> API documentation tells us how to test an API. It includes endpoint, method, URL, headers, auth type, request body, response body, status codes, and error scenarios. As a tester, I use documentation to prepare positive and negative test cases, validate response schema, identify required fields, and understand authentication and authorization rules.

