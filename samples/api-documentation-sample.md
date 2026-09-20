# VTran Design Check API

**Document ID:** API-VT-001  
**Version:** 1.0  
**Status:** Portfolio Sample  
**Last Updated:** June 2026

---

## Purpose

This document describes the REST API for the **VTran Design Check Service**.

The API allows developers to submit design files for automated structural checks and retrieve the results programmatically. It is intended for teams that want to integrate design checks into automated development and validation pipelines.

---

## Base URL

```text
https://api.vtran-example.com/v1
```

All requests and responses use JSON.

---

## Authentication

All API requests require a Bearer token.

**Example header:**

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
```

You can generate an access token from the developer portal under **Account → API Keys**.

---

## Common Request Headers

| Header          | Required | Description                                                          |
| --------------- | -------- | -------------------------------------------------------------------- |
| `Authorization` | Yes      | Bearer access token used to authenticate the request.                |
| `Content-Type`  | Yes      | Media type of the request body. Use `application/json`.              |
| `Accept`        | No       | Media type expected in the response. Defaults to `application/json`. |

---

# Endpoints

## 1. Submit a Design Check

**POST** `/checks`

Sends a design file for checking. The check runs asynchronously. The response returns a `check_id` that you can use to track the check.

### Request Body

| Field             | Type   | Required | Description                                                                                         |
| ----------------- | ------ | -------- | --------------------------------------------------------------------------------------------------- |
| `design_file_url` | string | Yes      | URL of the design file to be checked.                                                               |
| `ruleset`         | string | No       | Rule set to apply. Defaults to `standard`.                                                          |
| `severity`        | string | No       | Minimum severity to report. Valid values are `info`, `warning`, and `error`. Defaults to `warning`. |

### Example Request

```bash
curl -X POST https://api.vtran-example.com/v1/checks \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "design_file_url": "https://storage.example.com/designs/top_module.def",
    "ruleset": "strict",
    "severity": "error"
  }'
```

### Success Response

**202 Accepted**

```json
{
  "check_id": "chk_9f3a2b",
  "status": "queued",
  "submitted_at": "2026-06-15T10:30:00Z"
}
```

| Field          | Type   | Description                                 |
| -------------- | ------ | ------------------------------------------- |
| `check_id`     | string | Unique ID assigned to the design check.     |
| `status`       | string | Current status of the check.                |
| `submitted_at` | string | Date and time when the check was submitted. |

The check runs in the background. Use the `check_id` with the **Get Check Status** endpoint to check its progress.

---

## 2. Get Check Status

**GET** `/checks/{check_id}`

Returns the current status of a design check.

### Path Parameter

| Parameter  | Type   | Required | Description             |
| ---------- | ------ | -------- | ----------------------- |
| `check_id` | string | Yes      | ID of the design check. |

### Example Request

```bash
curl https://api.vtran-example.com/v1/checks/chk_9f3a2b \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Accept: application/json"
```

### Success Response

**200 OK**

```json
{
  "check_id": "chk_9f3a2b",
  "status": "completed",
  "submitted_at": "2026-06-15T10:30:00Z",
  "completed_at": "2026-06-15T10:34:18Z"
}
```

### Status Values

| Status      | Description                                           |
| ----------- | ----------------------------------------------------- |
| `queued`    | The check has been submitted and is waiting to start. |
| `running`   | The design is currently being checked.                |
| `completed` | The check has finished successfully.                  |
| `failed`    | The check could not be completed.                     |

Once the status is `completed`, the results are available for retrieval.

---

## Error Responses

The API returns an error when a request cannot be completed.

### Example Error Response

**400 Bad Request**

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The design_file_url field is required."
  }
}
```

### Common Errors

| HTTP Status | Error Code        | Description                                                       |
| ----------- | ----------------- | ----------------------------------------------------------------- |
| `400`       | `INVALID_REQUEST` | The request is missing a required field or contains invalid data. |
| `401`       | `UNAUTHORIZED`    | The access token is missing or invalid.                           |
| `404`       | `NOT_FOUND`       | The specified check could not be found.                           |
| `500`       | `INTERNAL_ERROR`  | An unexpected error occurred while processing the request.        |

---

## Example Workflow

A typical design check follows these steps:

1. Submit a design file using `POST /checks`.
2. Save the `check_id` returned in the response.
3. Use `GET /checks/{check_id}` to check the status.
4. When the status is `completed`, retrieve the check results.

```text
Submit Design
      ↓
Receive check_id
      ↓
Check Status
      ↓
Completed?
      ↓
Retrieve Results
```

---

## API Summary

| Operation             | Method | Endpoint             |
| --------------------- | ------ | -------------------- |
| Submit a design check | `POST` | `/checks`            |
| Get check status      | `GET`  | `/checks/{check_id}` |

---
