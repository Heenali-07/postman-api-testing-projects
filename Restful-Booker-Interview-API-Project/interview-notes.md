
I used Restful Booker API to create an end-to-end API testing project in Postman. I covered authentication, booking CRUD operations, positive scenarios, negative scenarios, API chaining, schema validation, and Newman execution.

## API Test Case Writing

API test cases should include:

- Test case ID
- Scenario
- Endpoint
- Method
- Headers
- Request body
- Test data
- Expected status code
- Expected response body
- Positive or negative category

## Positive Testing

Positive testing validates API behavior with valid data.

Example:

```text
Create booking with valid firstname, lastname, price, dates, and additional needs.
Expected: Status 200 and bookingid generated.
```

## Negative Testing

Negative testing validates API behavior with invalid data or invalid conditions.

Examples:

```text
Invalid booking ID
Missing token
Invalid token
Wrong credentials
Missing required fields
Wrong HTTP method
```

## Authentication Vs Authorization

Authentication checks who the user is.

Example:

```text
POST /auth with username and password.
```

Authorization checks what the user can access after authentication.

Example:

```text
PUT /booking/:id requires valid token.
```

## API Chaining

API chaining means using output of one API as input for another API.

Example:

```text
POST /auth -> save token
POST /booking -> save bookingid
GET /booking/:id -> use saved bookingid
PUT /booking/:id -> use saved token and bookingid
```

Postman code:

```javascript
const response = pm.response.json();
pm.environment.set("bookingId", response.bookingid);
```

Use in next request:

```text
{{bookingId}}
```

## Schema Validation

Schema validation checks response structure and data types.

Example:

```text
firstname should be string
totalprice should be number
depositpaid should be boolean
bookingdates should be object
```

## Newman

Newman is a command-line runner for Postman collections.

Command:

```bash
newman run collection.json -e environment.json
```

Use cases:

```text
Run API tests from terminal
Generate reports
Run regression suite
Integrate with Jenkins or GitHub Actions
```

