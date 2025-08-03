# Send Test Reminder API

**Endpoint:**  
`POST {baseURL}/appointment/sendTestReminder/{mobileNo}`

---

## Description

Triggers a **test reminder** message to the provided mobile number.  
This API is typically used to send the test whatsapp message 

---

## Request

### Method & URL

`POST /chatbotapi/appointment/sendTestReminder/{mobileNo}`

### Path Parameter

| Parameter   | Type     | Required | Description                     |
|-------------|----------|----------|---------------------------------|
| `mobileNo`  | `string` | Yes      | Mobile number to send reminder. |

---

### Example Request

```
POST {baseURL/chatbotapi/appointment/sendTestReminder/xxxxxxxx
```

No request body is required.

---

## Response

### Success Response

```json
{
    "success": true,
    "data": null,
    "messageToUser": "1 Reminders processed ",
    "message": "1 Reminders processed ",
    "status": 200,
    "timestamp": "2025-08-03T08:52:08.791797900Z",
    "errorCode": null,
    "traceId": null
}
```

---



---

## Response Fields

| Field           | Type      | Description                                                   |
|-----------------|-----------|---------------------------------------------------------------|
| `success`       | `boolean` | Indicates if the API call was successful.                     |
| `data`          | `any`     | Will be `null` for this endpoint.                             |
| `messageToUser` | `string`  | User-friendly message summarizing the result.                 |
| `message`       | `string`  | Technical message for debugging/logging purposes.             |
| `status`        | `integer` | HTTP status code.                                             |
| `timestamp`     | `string`  | Timestamp of the response in ISO format.                      |
| `errorCode`     | `string`  | Optional error code (only present on failure).                |
| `traceId`       | `string`  | Trace ID for correlating logs (may be `null` in some cases).  |

---

## Notes

- No request body is required.
- The `mobileNo` parameter should be provided **without country code** unless otherwise specified.
- This endpoint is intended for **test purposes only** and may not send actual reminders in production.

---

## Sample Curl

```bash
curl -X POST http://localhost:8091/chatbotapi/appointment/sendTestReminder/99184212
```
