# API Testing Postman Revision Project

This project is a complete hands-on revision set for API testing using Postman. It covers API basics, HTTP methods, status codes, headers, authorization, variables, environments, scripts, assertions, chaining, collection runner, data driven testing, Newman, and basic CI/CD thinking.

## Files

- `Pavan-Sir-API-Testing-Revision.postman_collection.json` - main Postman collection
- `QA-Environment.postman_environment.json` - Postman environment variables
- `test-data/users.csv` - data file for Collection Runner/Newman
- `test-data/users.json` - same data in JSON format
- `package.json` - Newman commands
- `revision-checklist.md` - daily topic checklist
- `test-cases.md` - manual API test case examples

## Import Into Postman

1. Open Postman.
2. Click `Import`.
3. Import:
   - `Pavan-Sir-API-Testing-Revision.postman_collection.json`
   - `QA-Environment.postman_environment.json`
4. Select environment: `API Testing QA Environment`.
5. Start from folder `01 API Basics and Health`.

## Practice Flow

Follow the folders in order:

1. API basics and health checks
2. GET requests
3. POST requests
4. PUT, PATCH, DELETE requests
5. Headers and status codes
6. Authorization
7. Variables and environments
8. Pre-request scripts
9. Tests and assertions
10. API chaining
11. Data driven testing
12. Negative testing

## APIs Used

- `https://jsonplaceholder.typicode.com` for simple REST practice
- `https://postman-echo.com` for headers, auth, query params, and echo testing

These are demo APIs. Some create/update/delete requests return success responses but do not permanently save data. That behavior is normal.

## Run With Newman

Install dependencies:

```bash
npm install
```

Run the full collection:

```bash
npm test
```

Run data driven tests with CSV:

```bash
npm run test:data
```

Run and generate an HTML report:

```bash
npm run test:report
```

## What To Revise In Every Request

For each request, check:

- Request method
- Endpoint URL
- Params
- Headers
- Body
- Status code
- Response time
- Response body
- Postman tests
- Variables used or saved

## Final Mini Project Task

After finishing all folders, create your own folder named `My Practice APIs` and add:

- One GET request
- One POST request
- One PUT or PATCH request
- One DELETE request
- At least 5 assertions
- At least 1 environment variable
- At least 1 chained value from a previous response
- One negative test

