# Next Available Time Blocks API

**Endpoint:**  
`POST {basepath}/chatbotapi/appointment/nextAvailableTimeBlocks`

---

## Description

Fetches the next available appointment time slots for a specific event on the given date.

---

## Request

### Headers

| Key            | Value             | Required |
|----------------|-------------------|----------|
| Content-Type   | application/json  | Yes      |

### Body

```json
{
    "eventId": 453,
    "availableDate": "31-08-2025"
}
```

#### Parameters

| Field          | Type      | Format       | Required | Description                                |
|----------------|-----------|--------------|----------|--------------------------------------------|
| `eventId`      | `integer` |              | Yes      | Unique identifier of the event.            |
| `availableDate`| `string`  | `dd-MM-yyyy` | Yes      | Date for which time slots are requested.   |

---

## Response

### Success Response

```json
{
    "success": true,
    "data": [
        {
            "appTime": "08:10"
        },
        {
            "appTime": "08:20"
        },
        {
            "appTime": "08:30"
        },
        {
            "appTime": "08:40"
        },
        {
            "appTime": "08:50"
        }
    ],
    "messageToUser": null,
    "message": "5 Record(s) Found (eventId:453)",
    "status": 200,
    "timestamp": "2025-08-03T08:29:18.702053300Z",
    "errorCode": null,
    "traceId": "11aa0f71cf1f4442"
}
```

---

### Error Response

```json
{
    "success": false,
    "data": null,
    "messageToUser": "Invalid date format",
    "message": "Validation failed",
    "status": 400,
    "timestamp": "2025-08-03T08:31:00Z",
    "errorCode": "INVALID_DATE",
    "traceId": "abcd1234efgh5678"
}
```

---

## Response Fields

| Field            | Type      | Description                                                   |
|------------------|-----------|---------------------------------------------------------------|
| `success`        | `boolean` | Indicates if the API call was successful.                     |
| `data`           | `array`   | List of available time slots (`appTime`).                     |
| `messageToUser`  | `string`  | Optional user-facing message.                                 |
| `message`        | `string`  | Technical message with record count or status description.    |
| `status`         | `integer` | HTTP status code.                                             |
| `timestamp`      | `string`  | Timestamp of the response in ISO format.                      |
| `errorCode`      | `string`  | Optional error code (only present on failure).                |
| `traceId`        | `string`  | Unique trace ID for debugging/log correlation.                |

---

## Notes

- The `availableDate` must be passed in `dd-MM-yyyy` format.
- Time slots are returned in 24-hour format (`HH:mm`).
- Ensure that the `eventId` is valid; otherwise, an error will be returned.

---

## Sample Curl

```bash
curl -X POST http://localhost:8091/chatbotapi/appointment/nextAvailableTimeBlocks   -H "Content-Type: application/json"   -d '{
    "eventId": 453,
    "availableDate": "31-08-2025"
  }'
```
