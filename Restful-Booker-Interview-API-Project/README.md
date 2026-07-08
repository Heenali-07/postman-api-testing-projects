# Restful-Booke-API/README.md

This project is designed for API testing interview preparation using Postman and Newman.

It covers:

- API test case writing
- Positive scenarios
- Negative scenarios
- Authentication testing
- Authorization testing
- API chaining
- Schema validation
- Token handling
- Newman execution
- Basic CI/CD understanding

## API Used

Base URL:

```text
https://restful-booker.herokuapp.com
```

Main endpoints:

```text
POST /auth
GET /booking
POST /booking
GET /booking/:id
PUT /booking/:id
PATCH /booking/:id
DELETE /booking/:id
```

## Files

- `Restful-Booker-Interview-Project.postman_collection.json` - Postman collection
- `Restful-Booker-QA.postman_environment.json` - Postman environment
- `test-cases.md` - manual test cases
- `interview-notes.md` - interview explanations
- `api-documentation.md` - API documentation practice
- `package.json` - Newman commands
- `.github/workflows/newman.yml` - CI/CD example

## Import In Postman

1. Open Postman.
2. Click `Import`.
3. Import:
   - `Restful-Booker-Interview-Project.postman_collection.json`
   - `Restful-Booker-QA.postman_environment.json`
4. Select environment:
   - `Restful Booker QA`

## Recommended Run Order

Run requests in this order:

1. `01 Health Check`
2. `02 Auth Testing`
3. `03 Booking Positive Flow`
4. `04 API Chaining`
5. `05 Schema Validation`
6. `06 Negative Testing`
7. `07 Authorization Deep Practice`

## Documentation Practice

Use `api-documentation.md` to revise how API documentation is written and read. It includes endpoint purpose, method, URL, headers, request body, response body, status codes, and test points.

## Important Notes

Restful Booker is a public demo API. Sometimes public demo APIs may be slow or temporarily unstable. If a test fails due to timeout or server issue, re-run once before assuming your test is wrong.

Some negative responses from this API are not perfectly designed. For example, invalid login returns `200 OK` with a failure message instead of `401 Unauthorized`. This is useful for interviews because you can explain that API behavior should follow documentation, but you can also report poor API design.

## Run With Newman

Install dependencies:

```bash
npm install
```

Run collection:

```bash
npm test
```

Run with CLI and HTML report:

```bash
npm run test:report
```

## Interview Pitch

You can explain this project like this:

> I created a Restful Booker API testing project in Postman. I covered positive CRUD scenarios, negative testing, authentication, authorization, API chaining, and schema validation. I used environment variables to store base URL, token, and booking ID. I used pre-request scripts for dynamic test data and Post-response scripts for assertions. I also prepared Newman commands so the collection can run from command line or CI/CD pipeline.
