# API Contract Documentation Reference

## What is an API Contract Doc?
A precise, developer-facing document describing an API endpoint or set of endpoints: what they do, how to call them, what they return, and how errors are handled. The goal is that a developer reading this doc can use the API correctly without asking anyone questions.

## Minimum Info Needed
Ask the user for:
1. Endpoint path(s) and HTTP method(s) (e.g. `POST /users`)
2. What does this endpoint do?
3. Request parameters / body shape (even roughly)
4. What does a success response look like?
5. What errors can it return?

If the user provides code, a schema, or example payloads — extract from those directly.

---

## Template

```markdown
# API Documentation: [Service or Resource Name]

**Base URL:** `https://api.example.com/v1`  
**Auth:** [Bearer token / API key / None]  
**Version:** [v1 / v2]  
**Last Updated:** [YYYY-MM-DD]

---

## Table of Contents

- [Endpoint 1 Name](#endpoint-1)
- [Endpoint 2 Name](#endpoint-2)

---

## Authentication

[How does auth work? What header/param? Where do they get the token?]

```http
Authorization: Bearer <token>
```

[Any rate limits? Quotas?]

---

## Endpoints

---

### [Endpoint Name] {#endpoint-1}

`[METHOD] /path/to/endpoint`

[One sentence: what does this endpoint do?]

#### Request

**Headers**

| Header | Required | Description |
|---|---|---|
| `Authorization` | Yes | Bearer token |
| `Content-Type` | Yes | `application/json` |

**Path Parameters**

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | Yes | The resource ID |

**Query Parameters**

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `limit` | integer | No | 20 | Max results to return (1-100) |
| `offset` | integer | No | 0 | Pagination offset |

**Request Body**

```json
{
  "field_name": "string",        // Required. Description of field.
  "another_field": 123,          // Optional. Description.
  "nested": {
    "key": "value"
  }
}
```

| Field | Type | Required | Description |
|---|---|---|---|
| `field_name` | string | Yes | [Description, constraints, example] |
| `another_field` | integer | No | [Description, default, range] |

#### Response

**Success — `200 OK`** (or `201 Created`, etc.)

```json
{
  "id": "usr_abc123",
  "created_at": "2024-01-15T10:30:00Z",
  "data": {
    "field": "value"
  }
}
```

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique resource identifier |
| `created_at` | ISO 8601 | Timestamp of creation |

#### Errors

| Status | Code | Description |
|---|---|---|
| `400` | `VALIDATION_ERROR` | Request body failed validation. Check `errors` field. |
| `401` | `UNAUTHORIZED` | Missing or invalid auth token. |
| `403` | `FORBIDDEN` | Token doesn't have permission for this resource. |
| `404` | `NOT_FOUND` | Resource with given ID doesn't exist. |
| `429` | `RATE_LIMITED` | Too many requests. See `Retry-After` header. |
| `500` | `INTERNAL_ERROR` | Server error. Retry with exponential backoff. |

**Error response shape:**
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable description",
    "errors": [
      { "field": "email", "message": "Invalid email format" }
    ]
  }
}
```

#### Example

**Request:**
```http
POST /users HTTP/1.1
Authorization: Bearer eyJhbGc...
Content-Type: application/json

{
  "email": "jane@example.com",
  "name": "Jane Doe"
}
```

**Response:**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": "usr_abc123",
  "email": "jane@example.com",
  "name": "Jane Doe",
  "created_at": "2024-01-15T10:30:00Z"
}
```

---

## Changelog

| Version | Date | Change |
|---|---|---|
| v1.1 | 2024-01-15 | Added `limit` param to GET /users |
| v1.0 | 2024-01-01 | Initial release |
```

---

## Quality Checklist

Before finishing, verify:
- [ ] Every parameter documented (required/optional, type, constraints)
- [ ] At least one full request/response example per endpoint
- [ ] All error codes listed with plain-English descriptions
- [ ] Auth method clearly explained
- [ ] Base URL included
- [ ] Response fields documented (not just shown in JSON)
- [ ] No endpoint says "returns user data" — be specific about what fields
