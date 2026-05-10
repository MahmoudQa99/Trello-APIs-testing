# Invalid Scenarios — Trello API Testing

**Project:** Trello REST API  
**Tool:** Postman  
**Tester:** Mahmoud Ahmed  
**Type:** Negative Testing — Invalid Params, Auth, and Edge Cases  
**Status Legend:** ✅ Pass | ❌ Fail | ⏳ Not Run

---

## AUTH / CREDENTIALS

### TC-INV-001 | Request with invalid API key

| Field                 | Detail                            |
| --------------------- | --------------------------------- |
| **Method**            | GET                               |
| **Endpoint**          | `/members/me`                     |
| **Params**            | `key=INVALIDKEY&token={{token}}`  |
| **Expected Status**   | 401 Unauthorized                  |
| **Expected Response** | `"invalid key"`                   |
| **Assertion**         | `pm.response.to.have.status(401)` |
| **Status**            | ✅                                |

---

### TC-INV-002 | Request with invalid token

| Field                 | Detail                               |
| --------------------- | ------------------------------------ |
| **Method**            | GET                                  |
| **Endpoint**          | `/members/me`                        |
| **Params**            | `key={{api_key}}&token=INVALIDTOKEN` |
| **Expected Status**   | 401 Unauthorized                     |
| **Expected Response** | `"invalid app token"`                |
| **Assertion**         | `pm.response.to.have.status(401)`    |
| **Status**            | ✅                                   |

---

### TC-INV-003 | Request with missing token

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/members/me`                     |
| **Params**          | `key={{api_key}}` (no token)      |
| **Expected Status** | 401 Unauthorized                  |
| **Assertion**       | `pm.response.to.have.status(401)` |
| **Status**          | ✅                                |

---

### TC-INV-004 | Request with missing API key

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/members/me`                     |
| **Params**          | `token={{token}}` (no key)        |
| **Expected Status** | 401 Unauthorized                  |
| **Assertion**       | `pm.response.to.have.status(401)` |
| **Status**          | ✅                                |

---

## BOARD — Invalid Scenarios

### TC-INV-005 | Create board with empty name

| Field                 | Detail                                    |
| --------------------- | ----------------------------------------- |
| **Method**            | POST                                      |
| **Endpoint**          | `/boards`                                 |
| **Params**            | `name=` (empty)                           |
| **Expected Status**   | 400 Bad Request                           |
| **Expected Response** | Error message indicating name is required |
| **Assertion**         | `pm.response.to.have.status(400)`         |
| **Status**            | ✅                                        |

---

### TC-INV-006 | Get board with invalid ID

| Field                 | Detail                            |
| --------------------- | --------------------------------- |
| **Method**            | GET                               |
| **Endpoint**          | `/boards/INVALIDBOARDID123`       |
| **Expected Status**   | 400 Bad Request                   |
| **Expected Response** | `"invalid id"`                    |
| **Assertion**         | `pm.response.to.have.status(400)` |
| **Status**            | ✅                                |

---

### TC-INV-007 | Get board with non-existent ID

| Field               | Detail                             |
| ------------------- | ---------------------------------- |
| **Method**          | GET                                |
| **Endpoint**        | `/boards/5f3e2d1c4b8a9c7f6e5d4a3b` |
| **Expected Status** | 404 Not Found                      |
| **Assertion**       | `pm.response.to.have.status(404)`  |
| **Status**          | ❌                                 |
| **Bug Report**          | BUG-001                                |

---

### TC-INV-008 | Update board with empty name

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | PUT                               |
| **Endpoint**        | `/boards/{{board_id}}`            |
| **Params**          | `name=` (empty)                   |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-009 | Delete board with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | DELETE                            |
| **Endpoint**        | `/boards/INVALIDID`               |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

## LIST — Invalid Scenarios

### TC-INV-010 | Create list with empty name

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | POST                              |
| **Endpoint**        | `/boards/{{board_id}}/lists`      |
| **Params**          | `name=` (empty)                   |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ❌                       |
| **Bug Report**          | BUG-002                       |

---

### TC-INV-011 | Create list on invalid board ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | POST                              |
| **Endpoint**        | `/boards/INVALIDID/lists`         |
| **Params**          | `name=Test List`                  |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-012 | Get list with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/lists/INVALIDLISTID`            |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-013 | Archive list with invalid value

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | PUT                               |
| **Endpoint**        | `/lists/{{list_id}}/closed`       |
| **Params**          | `value=maybe` (not boolean)       |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

## CARD — Invalid Scenarios

### TC-INV-014 | Create card with no list ID

| Field                 | Detail                            |
| --------------------- | --------------------------------- |
| **Method**            | POST                              |
| **Endpoint**          | `/cards`                          |
| **Params**            | `name=Test Card` (no idList)      |
| **Expected Status**   | 400 Bad Request                   |
| **Expected Response** | Error: invalid value for idList   |
| **Assertion**         | `pm.response.to.have.status(400)` |
| **Status**            | ✅                                |

---

### TC-INV-015 | Create card with invalid list ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | POST                              |
| **Endpoint**        | `/cards`                          |
| **Params**          | `name=Test Card&idList=INVALIDID` |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-016 | Get card with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/cards/INVALIDCARDID`            |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-017 | Update card with invalid due date format

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | PUT                               |
| **Endpoint**        | `/cards/{{card_id}}`              |
| **Params**          | `due=not-a-date`                  |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-018 | Delete card with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | DELETE                            |
| **Endpoint**        | `/cards/INVALIDID`                |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

## CHECKLIST — Invalid Scenarios

### TC-INV-019 | Create checklist with no card ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | POST                              |
| **Endpoint**        | `/checklists`                     |
| **Params**          | `name=My Checklist` (no idCard)   |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-020 | Create checklist with invalid card ID

| Field               | Detail                               |
| ------------------- | ------------------------------------ |
| **Method**          | POST                                 |
| **Endpoint**        | `/checklists`                        |
| **Params**          | `idCard=INVALIDID&name=My Checklist` |
| **Expected Status** | 400 Bad Request                      |
| **Assertion**       | `pm.response.to.have.status(400)`    |
| **Status**          | ✅                                   |

---

### TC-INV-021 | Get checklist with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/checklists/INVALIDID`           |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-022 | Update checklist with empty name

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | PUT                               |
| **Endpoint**        | `/checklists/{{checklist_id}}`    |
| **Params**          | `name=` (empty)                   |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-023 | Delete checklist with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | DELETE                            |
| **Endpoint**        | `/checklists/INVALIDID`           |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

## ORG (WORKSPACE) — Invalid Scenarios

### TC-INV-024 | Create org with empty display name

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | POST                              |
| **Endpoint**        | `/organizations`                  |
| **Params**          | `displayName=` (empty)            |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-025 | Get org with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | GET                               |
| **Endpoint**        | `/organizations/INVALIDORGID`     |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

### TC-INV-026 | Delete org with invalid ID

| Field               | Detail                            |
| ------------------- | --------------------------------- |
| **Method**          | DELETE                            |
| **Endpoint**        | `/organizations/INVALIDID`        |
| **Expected Status** | 400 Bad Request                   |
| **Assertion**       | `pm.response.to.have.status(400)` |
| **Status**          | ✅                                |

---

## Execution Summary

| Feature            | Total Invalid TCs | Passed | Failed |
| ------------------ | ----------------- | ------ | ------ |
| Auth / Credentials | 4                 | 4      | -      |
| Board              | 5                 | 4      | 1      |
| List               | 4                 | 3      | 1      |
| Card               | 5                 | 5      | -      |
| CheckList          | 5                 | 5      | -      |
| Org (Workspace)    | 3                 | 3      | -      |
| **Total**          | **26**            | 24      | 2      |
