# Test Cases — Trello API Testing

**Project:** Trello REST API  
**Tool:** Postman + Newman  
**Tester:** Mahmoud Ahmed  
**Result:** 133/133 Assertions Passed  
**Status Legend:** ✅ Pass | ❌ Fail | ⏳ Not Run

---

## SETUP FOLDER

> Purpose: Create test data used by all feature folders. Runs first.

### TC-001 | Create Org

| Field           | Detail                                          |
| --------------- | ----------------------------------------------- |
| **Method**      | POST                                            |
| **Endpoint**    | `/organizations`                                |
| **Params**      | `displayName=APIs testing workspace`            |
| **Assertions**  | Status code is 200 / Response time under 2000ms |
| **Post-Script** | Sets `org_id` environment variable              |
| **Status**      | ✅                                              |

---

### TC-002 | Get Org

| Field          | Detail                                                                                                      |
| -------------- | ----------------------------------------------------------------------------------------------------------- |
| **Method**     | GET                                                                                                         |
| **Endpoint**   | `/organizations/{{org_id}}`                                                                                 |
| **Assertions** | Status code is 200 / Response time under 2000ms / Organization name is correct / Organization id is correct |
| **Status**     | ✅                                                                                                          |

---

### TC-003 | Create Board

| Field           | Detail                                                                                |
| --------------- | ------------------------------------------------------------------------------------- |
| **Method**      | POST                                                                                  |
| **Endpoint**    | `/boards`                                                                             |
| **Params**      | `name=first_board&idOrganization={{org_id}}`                                          |
| **Assertions**  | Status code is 200 / Response time under 2000ms / Board was created with correct name |
| **Post-Script** | Sets `board_id` environment variable                                                  |
| **Status**      | ✅                                                                                    |

---

### TC-004 | Get Board

| Field          | Detail                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------ |
| **Method**     | GET                                                                                        |
| **Endpoint**   | `/boards/{{board_id}}`                                                                     |
| **Assertions** | Status code is 200 / Response time under 2000ms / Board ID matches / Board name is correct |
| **Status**     | ✅                                                                                         |

---

### TC-005 | Create List

| Field           | Detail                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------ |
| **Method**      | POST                                                                                                   |
| **Endpoint**    | `/boards/{{board_id}}/lists`                                                                           |
| **Params**      | `name=To Do`                                                                                           |
| **Assertions**  | Status code is 200 / Response time under 2000ms / List name is correct / List belongs to correct board |
| **Post-Script** | Sets `list_id` environment variable                                                                    |
| **Status**      | ✅                                                                                                     |

---

### TC-006 | Get List

| Field          | Detail                                                            |
| -------------- | ----------------------------------------------------------------- |
| **Method**     | GET                                                               |
| **Endpoint**   | `/lists/{{list_id}}`                                              |
| **Assertions** | Status code is 200 / Response time under 2000ms / List ID matches |
| **Status**     | ✅                                                                |

---

### TC-007 | Create Card

| Field           | Detail                                                                                                |
| --------------- | ----------------------------------------------------------------------------------------------------- |
| **Method**      | POST                                                                                                  |
| **Endpoint**    | `/cards`                                                                                              |
| **Params**      | `name=first_card&idList={{list_id}}`                                                                  |
| **Assertions**  | Status code is 200 / Response time under 2000ms / Card name is correct / Card belongs to correct list |
| **Post-Script** | Sets `card_id` environment variable                                                                   |
| **Status**      | ✅                                                                                                    |

---

### TC-008 | Get Card

| Field          | Detail                                                            |
| -------------- | ----------------------------------------------------------------- |
| **Method**     | GET                                                               |
| **Endpoint**   | `/cards/{{card_id}}`                                              |
| **Assertions** | Status code is 200 / Response time under 2000ms / Card ID matches |
| **Status**     | ✅                                                                |

---

### TC-009 | Create CheckList

| Field           | Detail                                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------------- |
| **Method**      | POST                                                                                                            |
| **Endpoint**    | `/checklists`                                                                                                   |
| **Params**      | `idCard={{card_id}}&name=QA Checklist`                                                                          |
| **Assertions**  | Status code is 200 / Response time under 2000ms / Checklist name is correct / Checklist belongs to correct card |
| **Post-Script** | Sets `checklist_id` environment variable                                                                        |
| **Status**      | ✅                                                                                                              |

---

### TC-010 | Get CheckList

| Field          | Detail                                                                 |
| -------------- | ---------------------------------------------------------------------- |
| **Method**     | PUT                                                                    |
| **Endpoint**   | `/checklists/{{checklist_id}}`                                         |
| **Assertions** | Status code is 200 / Response time under 2000ms / Checklist ID matches |
| **Status**     | ✅                                                                     |

---

## BOARD FOLDER

### TC-011 | Create Board

| Field          | Detail                                                                            |
| -------------- | --------------------------------------------------------------------------------- |
| **Method**     | POST                                                                              |
| **Endpoint**   | `/boards`                                                                         |
| **Params**     | `name=second_board`                                                               |
| **Assertions** | Status code is 200 / Response time under 2000ms / Board created with correct name |
| **Status**     | ✅                                                                                |

---

### TC-012 | Get Board

| Field          | Detail                                                                               |
| -------------- | ------------------------------------------------------------------------------------ |
| **Method**     | GET                                                                                  |
| **Endpoint**   | `/boards/{{board_id}}`                                                               |
| **Assertions** | Status code is 200 / Response time under 2000ms / Board ID matches / Name is correct |
| **Status**     | ✅                                                                                   |

---

### TC-013 | Update Board

| Field           | Detail                                                                         |
| --------------- | ------------------------------------------------------------------------------ |
| **Method**      | PUT                                                                            |
| **Endpoint**    | `/boards/{{board_id}}`                                                         |
| **Params**      | `name=updated_board_name`                                                      |
| **Assertions**  | Status code is 200 / Response time under 2000ms / Board name updated correctly |
| **Post-Script** | Sets `board_name` variable to updated name                                     |
| **Status**      | ✅                                                                             |

---

### TC-014 | Get All Boards (verify update)

| Field          | Detail                                                                                                     |
| -------------- | ---------------------------------------------------------------------------------------------------------- |
| **Method**     | GET                                                                                                        |
| **Endpoint**   | `/members/me/boards`                                                                                       |
| **Assertions** | Status code is 200 / Response time under 2000ms / Response is an array / Updated board name exists in list |
| **Status**     | ✅                                                                                                         |

---

## LIST FOLDER

### TC-015 | Create List

| Field          | Detail                                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **Method**     | POST                                                                                              |
| **Endpoint**   | `/boards/{{board_id}}/lists`                                                                      |
| **Params**     | `name=In Progress`                                                                                |
| **Assertions** | Status code is 200 / Response time under 2000ms / List name is correct / Belongs to correct board |
| **Status**     | ✅                                                                                                |

---

### TC-016 | Get List

| Field          | Detail                                                            |
| -------------- | ----------------------------------------------------------------- |
| **Method**     | GET                                                               |
| **Endpoint**   | `/lists/{{list_id}}`                                              |
| **Assertions** | Status code is 200 / Response time under 2000ms / List ID matches |
| **Status**     | ✅                                                                |

---

### TC-017 | Update List

| Field           | Detail                                                                        |
| --------------- | ----------------------------------------------------------------------------- |
| **Method**      | PUT                                                                           |
| **Endpoint**    | `/lists/{{list_id}}`                                                          |
| **Params**      | `name=Done`                                                                   |
| **Assertions**  | Status code is 200 / Response time under 2000ms / List name updated correctly |
| **Post-Script** | Sets `list_name` to updated value                                             |
| **Status**      | ✅                                                                            |

---

### TC-018 | Get List (verify update)

| Field          | Detail                                               |
| -------------- | ---------------------------------------------------- |
| **Method**     | GET                                                  |
| **Endpoint**   | `/lists/{{list_id}}`                                 |
| **Assertions** | Status code is 200 / List name matches updated value |
| **Status**     | ✅                                                   |

---

### TC-019 | Archive List

| Field          | Detail                                                                |
| -------------- | --------------------------------------------------------------------- |
| **Method**     | PUT                                                                   |
| **Endpoint**   | `/lists/{{list_id}}/closed`                                           |
| **Params**     | `value=true`                                                          |
| **Assertions** | Status code is 200 / Response time under 2000ms / List closed is true |
| **Status**     | ✅                                                                    |

---

### TC-020 | Get All Archived Lists (verify archive)

| Field          | Detail                                                 |
| -------------- | ------------------------------------------------------ |
| **Method**     | GET                                                    |
| **Endpoint**   | `/boards/{{board_id}}/lists/closed`                    |
| **Assertions** | Status code is 200 / Archived list appears in response |
| **Status**     | ✅                                                     |

---

### TC-021 | Unarchive List

| Field          | Detail                                                                 |
| -------------- | ---------------------------------------------------------------------- |
| **Method**     | PUT                                                                    |
| **Endpoint**   | `/lists/{{list_id}}/closed`                                            |
| **Params**     | `value=false`                                                          |
| **Assertions** | Status code is 200 / Response time under 2000ms / List closed is false |
| **Status**     | ✅                                                                     |

---

### TC-022 | Get All Lists (verify unarchive)

| Field          | Detail                                          |
| -------------- | ----------------------------------------------- |
| **Method**     | GET                                             |
| **Endpoint**   | `/boards/{{board_id}}/lists`                    |
| **Assertions** | Status code is 200 / List appears in open lists |
| **Status**     | ✅                                              |

---

## CARD FOLDER

### TC-023 | Create Card

| Field          | Detail                                                                                                                     |
| -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Method**     | POST                                                                                                                       |
| **Endpoint**   | `/cards`                                                                                                                   |
| **Params**     | `name=second_card&idList={{list_id}}`                                                                                      |
| **Assertions** | Status code is 200 / Response time under 2000ms / Card name is correct / Card belongs to correct list / Card is not closed |
| **Status**     | ✅                                                                                                                         |

---

### TC-024 | Get Card

| Field          | Detail                                                                                   |
| -------------- | ---------------------------------------------------------------------------------------- |
| **Method**     | GET                                                                                      |
| **Endpoint**   | `/cards/{{card_id}}`                                                                     |
| **Assertions** | Status code is 200 / Response time under 2000ms / Card ID matches / Card in correct list |
| **Status**     | ✅                                                                                       |

---

### TC-025 | Update Card

| Field          | Detail                                                                                                        |
| -------------- | ------------------------------------------------------------------------------------------------------------- |
| **Method**     | PUT                                                                                                           |
| **Endpoint**   | `/cards/{{card_id}}`                                                                                          |
| **Params**     | `name=updated_card&desc=updated description`                                                                  |
| **Assertions** | Status code is 200 / Response time under 2000ms / Card name updated correctly / Description updated correctly |
| **Status**     | ✅                                                                                                            |

---

### TC-026 | Get All Cards (verify update)

| Field          | Detail                                                                       |
| -------------- | ---------------------------------------------------------------------------- |
| **Method**     | GET                                                                          |
| **Endpoint**   | `/lists/{{list_id}}/cards`                                                   |
| **Assertions** | Status code is 200 / Response is an array / Updated card name exists in list |
| **Status**     | ✅                                                                           |

---

## CHECKLIST FOLDER

### TC-027 | Create CheckList

| Field          | Detail                                                                                                |
| -------------- | ----------------------------------------------------------------------------------------------------- |
| **Method**     | POST                                                                                                  |
| **Endpoint**   | `/checklists`                                                                                         |
| **Params**     | `idCard={{card_id}}&name=Second Checklist`                                                            |
| **Assertions** | Status code is 200 / Response time under 2000ms / Checklist name is correct / Belongs to correct card |
| **Status**     | ✅                                                                                                    |

---

### TC-028 | Get CheckList

| Field          | Detail                                                                 |
| -------------- | ---------------------------------------------------------------------- |
| **Method**     | GET                                                                    |
| **Endpoint**   | `/checklists/{{checklist_id}}`                                         |
| **Assertions** | Status code is 200 / Response time under 2000ms / Checklist ID matches |
| **Status**     | ✅                                                                     |

---

### TC-029 | Update CheckList

| Field          | Detail                                                                             |
| -------------- | ---------------------------------------------------------------------------------- |
| **Method**     | PUT                                                                                |
| **Endpoint**   | `/checklists/{{checklist_id}}`                                                     |
| **Params**     | `name=Updated Checklist`                                                           |
| **Assertions** | Status code is 200 / Response time under 2000ms / Checklist name updated correctly |
| **Status**     | ✅                                                                                 |

---

## TEARDOWN FOLDER

> Purpose: Clean up all test data created during the run. Runs last.

### TC-030 | Delete CheckList

| Field          | Detail                                          |
| -------------- | ----------------------------------------------- |
| **Method**     | DELETE                                          |
| **Endpoint**   | `/checklists/{{checklist_id}}`                  |
| **Assertions** | Status code is 200 / Response time under 2000ms |
| **Status**     | ✅                                              |

---

### TC-031 | Delete Card

| Field          | Detail                                          |
| -------------- | ----------------------------------------------- |
| **Method**     | DELETE                                          |
| **Endpoint**   | `/cards/{{card_id}}`                            |
| **Assertions** | Status code is 200 / Response time under 2000ms |
| **Status**     | ✅                                              |

---

### TC-032 | Delete Board

| Field          | Detail                                          |
| -------------- | ----------------------------------------------- |
| **Method**     | DELETE                                          |
| **Endpoint**   | `/boards/{{board_id}}`                          |
| **Assertions** | Status code is 200 / Response time under 2000ms |
| **Status**     | ✅                                              |

---

### TC-033 | Delete Org

| Field          | Detail                                          |
| -------------- | ----------------------------------------------- |
| **Method**     | DELETE                                          |
| **Endpoint**   | `/organizations/{{org_id}}`                     |
| **Assertions** | Status code is 200 / Response time under 2000ms |
| **Status**     | ✅                                              |

---

## Execution Summary

| Folder    | Requests | Assertions | Passed  | Failed |
| --------- | -------- | ---------- | ------- | ------ |
| Setup     | 10       | 30         | 30      | 0      |
| Board     | 4        | 14         | 14      | 0      |
| List      | 8        | 24         | 24      | 0      |
| Card      | 4        | 14         | 14      | 0      |
| CheckList | 3        | 9          | 9       | 0      |
| Teardown  | 4        | 8          | 8       | 0      |
| **Total** | **33**   | **133**    | **133** | **0**  |

---

## Newman Run Result

**Full collection run via Newman CLI**  
133 assertions — 0 failures  
Average response time: 426ms

![Newman Results](../Screenshots/newman%20d-1.PNG)
