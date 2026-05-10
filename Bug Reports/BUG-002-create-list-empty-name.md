# BUG-002 — API Allows Creating a List with Empty Name

## Summary
Sending a POST request to create a list with an empty `name` field does not return a validation error — the list is created successfully with an empty name.

## Environment
| Field | Value |
|---|---|
| **Tool** | Postman |
| **API** | Trello REST API v1 |
| **Endpoint** | `POST /boards/{id}/lists` |
| **Date Found** | 2025-05-10 |

## Severity
- [ ] Critical
- [x] High
- [ ] Medium
- [ ] Low

## Priority
- [x] High
- [ ] Medium
- [ ] Low

## Status
`Open`

## Related Test Case
`TC-INV-010`

---

## Steps to Reproduce
1. Send `POST` request to `/boards/{{board_id}}/lists`
2. Set param `name=` (empty string)
3. Use valid `api_key` and `token`
4. Observe response

## Expected Result
- Status: `400 Bad Request`
- Response indicates name field is required and cannot be empty

## Actual Result
- Status: `200 OK`
- List created successfully with an empty name
- Response returns a valid list object with `"name": ""`

---

## Impact
- Users can end up with unnamed lists in their boards
- Data integrity issue — a list without a name has no context or meaning
- Any UI built on this API would display a blank list name to the end user

## Notes
This is a missing server-side validation bug. The API should reject empty string values for required fields like `name` the same way it rejects a missing `idList` on card creation.
