# API Documentation Template

# API Name

Short Description on what is the purpose of the API.

---

## Endpoint

```
[HTTP METHOD] /your/api/endpoint/
```

## Authentication Required

- Yes
- No

---

## Request

### Method

`GET` | `POST` | `PUT` | `PATCH` | `DELETE`

### Headers

| Key           | Value            | Required | Description            |
| ------------- | ---------------- | -------- | ---------------------- |
| Authorization | Bearer \<token\> | Yes      | User access token      |
| Content-Type  | application/json | Yes      | Format of request body |

### Request Parameters

#### Path Parameters

| Parameter | Type    | Required | Description         |
| --------- | ------- | -------- | ------------------- |
| id        | integer | Yes      | Resource identifier |

#### Query Parameters (for GET):

| Name    | Type   | Required | Description               |
| ------- | ------ | -------- | ------------------------- |
| example | string | No       | Optional filter parameter |

#### Body Parameters (for POST/PUT/PATCH):

```json
{
  "example": "value",
  "another_example": 123
}
```

| Field           | Type    | Required | Description                  |
| --------------- | ------- | -------- | ---------------------------- |
| example         | string  | Yes      | Description of the field     |
| another_example | integer | No       | Description of another field |

---

## Response

### Success Response

**Status Code**: `200 OK` | `201 Created`

**Sample Response**:

```json
{
  "id": 1,
  "name": "Sample",
  "created_at": "2025-04-12T12:00:00Z"
}
```

| Field      | Type     | Description           |
| ---------- | -------- | --------------------- |
| id         | integer  | Unique identifier     |
| name       | string   | Name of the resource  |
| created_at | datetime | Timestamp of creation |

---

### Error Responses

**Status Code**: `400 Bad Request`

```json
{
  "error": "Invalid input data"
}
```

**Status Code**: `401 Unauthorized`

```json
{
  "detail": "Authentication credentials were not provided."
}
```

**Status Code**: `404 Not Found`

```json
{
  "detail": "Resource not found."
}
```

| Code | Meaning               | When it happens                |
| ---- | --------------------- | ------------------------------ |
| 400  | Bad Request           | Invalid data sent              |
| 401  | Unauthorized          | Missing or invalid token       |
| 403  | Forbidden             | No permission for the resource |
| 404  | Not Found             | Resource doesn't exist         |
| 500  | Internal Server Error | Unexpected server-side issue   |

---

## Examples

### cURL

```bash
curl -X GET https://api.example.com/endpoint/ \
  -H "Authorization: Bearer <your_token>"
```

### JavaScript (fetch)

```javascript
fetch("https://api.example.com/endpoint/", {
  headers: {
    Authorization: "Bearer <your_token>",
    "Content-Type": "application/json",
  },
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

---

## Notes

- Add any special conditions or additional logic here.
- E.g., "Returns empty array if no results found."
- E.g., "Date format must be YYYY-MM-DD."

---

## Related Endpoints

- `POST /your/api/endpoint/` - Create a new resource
- `PUT /your/api/endpoint/{id}/` - Update a resource
- `DELETE /your/api/endpoint/{id}/` - Delete a resource

---

## Rate Limiting

- Maximum 100 requests per minute
- Exceeding this limit will return a `429 Too Many Requests` status code
