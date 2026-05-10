# Trello API Testing — Postman

## Summary
End-to-end API testing project for Trello REST APIs using Postman and Newman.

- 33 requests executed
- 133 assertions
- 0 failures

---

## API Coverage

| Module | Requests | Assertions |
|---|---|---|
| Setup | 8 | 41 |
| Board | 4 | 15 |
| List | 8 | 33 |
| Card | 4 | 18 |
| CheckList | 3 | 11 |
| Organization (Workspace) | 2 | 6 |
| Teardown | 4 | 9 |
| **Total** | **33** | **133** |

---

## Validations Performed

- Status code validation
- Response time under 2000ms
- Response body validation
- Parent-child relationship validation
- Verification GET requests after POST/PUT operations
- Authentication negative testing (401 Unauthorized)

---

## Tools Used

- Postman
- Newman
- Trello REST API

---

## Features

- CRUD API testing
- Dynamic environment variables
- Automated test scripts
- Collection runner execution
- Newman CLI execution

---

## How to Run

### Using Postman
1. Import:
   - `Collections/Collection.json`
   - `Environment/Environment_template.json`

2. Add your:
   - `api_key`
   - `token`

3. Run the collection using Collection Runner

---

### Using Newman

```bash
newman run Collection.json -e Environment_template.json
