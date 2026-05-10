# BUG-001 — Invalid Board ID Returns 400 Instead of 404

## Summary
When sending a GET request with a non-existent but valid-format board ID, the API returns 400 Bad Request instead of the expected 404 Not Found.

## Environment
| Field | Value |
|---|---|
| **Tool** | Postman |
| **API** | Trello REST API v1 |
| **Endpoint** | `GET /boards/{id}` |
| **Date Found** | 2025-05-10 |

## Severity
- [ ] Critical
- [ ] High
- [x] Medium
- [ ] Low

## Priority
- [ ] High
- [x] Medium
- [ ] Low

## Status
`Open`

## Related Test Case
`TC-INV-007`

---

## Steps to Reproduce
1. Send `GET` request to `/boards/5f3e2d1c4b8a9c7f6e5d4a3b`
2. Use valid `api_key` and `token`
3. Observe response

## Expected Result
- Status: `404 Not Found`
- Response indicates the board does not exist

## Actual Result
- Status: `400 Bad Request`
- Response body: `"invalid id"`

---

## Notes
REST API best practices state that:
- `400` = bad request format / malformed input
- `404` = resource not found

A valid-format ID that simply doesn't exist should return `404`, not `400`.
This is an API design inconsistency — Trello uses `400` for both malformed IDs and non-existent resources.
