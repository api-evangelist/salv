---
name: Manage a custom screening list
description: Add, update, retrieve and remove records in a custom list.
api: openapi/salv-aml-openapi-original.yml
operations: [getRecords, addRecord, getRecord, updateRecord, deleteRecord]
---

# Manage a custom list

Maintain the records of a Salv custom list used for screening/monitoring.

## Auth
OAuth2 client-credentials token (scope `aml`) as `Authorization: Bearer <token>`.

## Steps
1. List existing records with `getRecords` (`GET /v1/custom-lists/{customListId}/records`).
2. Add a record with `addRecord` (`POST /v1/custom-lists/{customListId}/records`).
3. Read a single record with `getRecord` (`GET /v1/custom-lists/{customListId}/records/{id}`).
4. Update it with `updateRecord` (`PUT /v1/custom-lists/{customListId}/records/{id}`).
5. Remove it with `deleteRecord` (`DELETE /v1/custom-lists/{customListId}/records/{id}`).

## Notes
- Record changes emit `CUSTOM_LIST_RECORD_CREATED` / `_UPDATED` / `_ARCHIVED` webhooks.
- 404 means the list or record id does not exist.
