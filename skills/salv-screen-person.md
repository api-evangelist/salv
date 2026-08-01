---
name: Screen a person against sanctions, PEP and adverse-media lists
description: Run a screening check on a person and inspect the resulting hits.
api: openapi/salv-aml-openapi-original.yml
operations: [addPersonV2, checkPerson, getScreeningAlertHits]
---

# Screen a person

Use the Salv AML API to screen an individual/entity against sanctions, PEP/RCA and adverse-media lists.

## Auth
Obtain an OAuth2 token via the client-credentials flow at `https://app.salv.com/oauth/token` (sandbox: `https://demo.salv.com/oauth/token`) with scope `aml`. Cache the token — tokens are long-lived and the token endpoint is limited to 10 req/min per IP. Send it as `Authorization: Bearer <token>`.

## Steps
1. Create (or reference) the person with `addPersonV2` (`POST /v2/persons`).
2. Run screening with `checkPerson` (`POST /v1/persons/{id}/screening-checks`).
3. If a screening alert is raised, retrieve its matches with `getScreeningAlertHits` (`GET /v1/screening-alerts/{screeningAlertId}/hits`).

## Notes
- Errors are JSON (not RFC 9457): 400 bad request, 401 unauthorized, 404 not found, 422 person exists, 500 server error.
- Screening results also arrive asynchronously via the `SCREENING_ALERT_CREATED` webhook (see asyncapi/salv-webhooks.yml).
- No idempotency key is supported; a duplicate person returns 422.
