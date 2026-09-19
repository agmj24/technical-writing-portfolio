# API Documentation (Sanitized Sample)

> Everything below describes a fictional API — `DRC Check Service` — built to show how I structure and write API documentation. No real endpoints, product names, or customer data are used.

## A note before you read this

I put this together the way I'd actually approach a new API doc set at work: start with what a developer needs before they touch a single endpoint, then get into the reference detail. A lot of API docs jump straight to endpoint tables and skip the "why would I call this" part, which is usually where people actually get stuck.

## Overview

The DRC Check Service lets you submit a design file for a design rule check (DRC) and retrieve the results programmatically, instead of running the check through the desktop application. It's meant for teams who want to fold DRC checks into an automated build or CI pipeline.

Base URL:
```
https://api.example-eda.com/v1
```

All requests and responses use JSON.

## Authentication

Every request needs an API key, sent as a header:

```
Authorization: Bearer <your_api_key>
```

You can generate a key from your account settings page. Keys don't expire, but you can revoke and regenerate them at any time — if a key is compromised, revoke it immediately rather than waiting for a scheduled rotation.

## Endpoints

### Submit a DRC Job

```
POST /drc-jobs
```

Submits a design file for checking. This is asynchronous — the call returns a job ID right away, and the check itself runs in the background (larger designs can take several minutes).

**Request body**

| Field | Type | Required | Description |
|---|---|---|---|
| `design_file_url` | string | Yes | A signed URL pointing to the design file. |
| `ruleset` | string | No | Rule set to apply. Defaults to `standard`. |
| `callback_url` | string | No | If provided, we'll POST the results here when the job finishes instead of you having to poll. |

**Example request**

```bash
curl -X POST https://api.example-eda.com/v1/drc-jobs \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "design_file_url": "https://storage.example.com/designs/top_module.def",
    "ruleset": "strict"
  }'
```

**Example response**

```json
{
  "job_id": "drc_8f2a1c",
  "status": "queued",
  "submitted_at": "2026-03-14T09:12:00Z"
}
```

### Get Job Status / Results

```
GET /drc-jobs/{job_id}
```

Returns the current status of a job. Once `status` is `completed`, the response includes a `results` object with the violation summary.

**Example response (completed job)**

```json
{
  "job_id": "drc_8f2a1c",
  "status": "completed",
  "results": {
    "violations": 3,
    "severity_breakdown": {
      "error": 1,
      "warning": 2
    },
    "report_url": "https://api.example-eda.com/v1/drc-jobs/drc_8f2a1c/report"
  }
}
```

### Job Status Values

| Status | Meaning |
|---|---|
| `queued` | Job received, waiting to run. |
| `running` | Check is in progress. |
| `completed` | Finished — see `results`. |
| `failed` | Job could not complete. Check `error_message` in the response. |

## Error Handling

The API uses standard HTTP status codes. A 4xx means something's wrong with the request; a 5xx means something went wrong on our end.

| Code | Meaning | Typical Cause |
|---|---|---|
| 400 | Bad Request | Missing or malformed field in the request body |
| 401 | Unauthorized | Missing or invalid API key |
| 404 | Not Found | Job ID doesn't exist, or belongs to a different account |
| 429 | Too Many Requests | Rate limit exceeded — see below |
| 500 | Internal Server Error | Something failed on our side; safe to retry |

Error responses include a message you can actually act on:

```json
{
  "error": "invalid_ruleset",
  "message": "The ruleset 'ultra-strict' does not exist. Available rulesets: standard, strict, custom."
}
```

## Rate Limits

100 requests per minute per API key. If you go over that, you'll get a 429 with a `Retry-After` header telling you how many seconds to wait. For bulk submissions, it's worth batching design files into fewer, larger jobs rather than firing off one request per file.

## Why I structured it this way

Async job endpoints are the part people usually mess up in docs — you submit something, get back an ID, and then have to go figure out on your own how to check on it. I always document the submit and status-check calls together, right next to each other, with a note about polling vs. callbacks, because that's the actual workflow a developer follows. Splitting the two into separate, distant sections in the doc structure just makes people flip back and forth.
