# Manual API Test Cases

## GET Posts

| Test Case ID | Scenario | Steps | Expected Result |
|---|---|---|---|
| API_GET_001 | Get all posts | Send GET request to `/posts` | Status code is 200 and response is an array |
| API_GET_002 | Get one valid post | Send GET request to `/posts/1` | Status code is 200 and `id` is 1 |
| API_GET_003 | Get invalid post | Send GET request to `/posts/999999` | API returns empty object or not found behavior |

## POST Post

| Test Case ID | Scenario | Steps | Expected Result |
|---|---|---|---|
| API_POST_001 | Create post with valid body | Send POST request with title, body, userId | Status code is 201 and response contains id |
| API_POST_002 | Create post with dynamic data | Use pre-request script values in body | Response contains submitted title/body |

## PUT/PATCH/DELETE

| Test Case ID | Scenario | Steps | Expected Result |
|---|---|---|---|
| API_PUT_001 | Update full post | Send PUT request to `/posts/1` | Status code is 200 and response has updated values |
| API_PATCH_001 | Update title only | Send PATCH request to `/posts/1` | Status code is 200 and title is updated |
| API_DELETE_001 | Delete post | Send DELETE request to `/posts/1` | Status code is 200 |

## Authorization

| Test Case ID | Scenario | Steps | Expected Result |
|---|---|---|---|
| API_AUTH_001 | Valid basic auth | Send request with correct username/password | Status code is 200 and authenticated is true |
| API_AUTH_002 | Invalid basic auth | Send request with wrong credentials | Status code is 401 |
| API_AUTH_003 | Bearer token header | Send request with Authorization header | Header is received by API |

## Negative Testing

| Test Case ID | Scenario | Steps | Expected Result |
|---|---|---|---|
| API_NEG_001 | Invalid endpoint | Send request to wrong endpoint | Status code is 404 |
| API_NEG_002 | Invalid method | Send unsupported method where possible | Proper error response is returned |
| API_NEG_003 | Missing required data | Send incomplete body | API should reject or show demo API limitation |

