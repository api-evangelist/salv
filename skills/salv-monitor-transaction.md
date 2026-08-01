---
name: Monitor a transaction and handle the alert
description: Add a transaction, run monitoring checks, and read any alert raised.
api: openapi/salv-aml-openapi-original.yml
operations: [addTransaction, runTransactionMonitoringChecks, getAlert, publicUpdateAlertStatus]
---

# Monitor a transaction

Detect suspicious transaction patterns with Salv real-time (ONLINE) monitoring.

## Auth
OAuth2 client-credentials token (scope `aml`) as `Authorization: Bearer <token>`.

## Steps
1. Add the transaction for a person with `addTransaction` (`POST /v1/persons/{personId}/transactions`).
2. Run monitoring with `runTransactionMonitoringChecks` (`POST /v1/transactions/{transactionId}/monitoring-checks`).
3. Fetch any raised alert with `getAlert` (`GET /v1/alerts/{alertId}`).
4. Resolve it by setting its status with `publicUpdateAlertStatus` (`PUT /v1/alerts/status`).

## Notes
- Alerts also fire the `ALERT_CREATED` / `ALERT_STATUS_UPDATED` webhooks (asyncapi/salv-webhooks.yml).
- A 500 "Execution of monitoring checks failed" should be retried with backoff.
