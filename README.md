# chatbot
The API Specification for WhatsApp ChatBot 
# 📦 API Response Structure – Standard Format

All chatbot APIs follow a **uniform response structure** for consistency, debuggability, and ease of integration. The JSON structure below illustrates both success and error scenarios.

---

## 🔄 Sample Error Response

```json
{
  "success": false,
  "data": null,
  "messageToUser": null,
  "message": "No appointment found for eventId: 13111",
  "status": 404,
  "timestamp": "2025-05-26T15:24:44.020125100Z",
  "errorCode": "APPT-404",
  "traceId": "9927f06ede6c40e0"
}
```

---

## 🧩 Field Definitions

| Field           | Type          | Description |
|------------------|---------------|-------------|
| `success`        | boolean       | **Business status flag.** Indicates whether the user’s action was successfully processed by the system, regardless of HTTP status code. <br> - `true` = Operation was successful <br> - `false` = Business validation failed, record not found, etc. |
| `data`           | any / null    | **Payload returned from the API.** <br>May be: <ul><li>an object (single item)</li><li>an array (multiple records)</li><li>`null` if there's no data to return.</li></ul> |
| `messageToUser`  | string / null | **User-facing message**, localized based on the `userLanguage` selected during chatbot onboarding (e.g., Arabic or English). Safe to display to end users. |
| `message`        | string        | **System/internal message**, always in **English**. Intended for debugging and logs. Not shown to the user. |
| `status`         | number        | Mirrors the **HTTP status code** of the response. Examples: `200`, `400`, `404` |
| `timestamp`      | string (ISO)  | ISO timestamp when the response was generated. Useful for **debugging** and **audit**. |
| `errorCode`      | string / null | Custom error code to classify known errors (e.g., `"APPT-404"` for "Appointment Not Found"). |
| `traceId`        | string        | Unique ID for tracing logs and API requests across systems. |

---

## ✅ Success Response Example

```json
{
  "success": true,
  "data": null,
  "messageToUser": "Your appointment has been confirmed successfully.",
  "message": "Appointment confirmed (eventId: 3)",
  "status": 200,
  "timestamp": "2025-05-26T10:20:00Z",
  "errorCode": null,
  "traceId": "abc123def456ghi789"
}
```

---

## 📝 Notes & Best Practices

- Use `success` to determine business result, not just `status` code.
- `messageToUser` is optional and shown only when the message is relevant for the end user.
- `message`, `errorCode`, and `traceId` are essential for backend logs and support.
- `data` varies by API — check endpoint-specific schema for details.
