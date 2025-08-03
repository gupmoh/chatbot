# 📘 API Specification: Reschedule Appointment

## Endpoint
**POST** `{baseURL}/appointment/rescheduleByTime`  
**Base URL**: `{{see the mail}}`

---

## Purpose
This API is triggered when a **user selects an available free slot** from WhatsApp to **reschedule their appointment**.

---

## Request

### URL
```
POST /chatbotapi/appointment/rescheduleByTime
```

### Headers
| Header        | Value              |
|---------------|--------------------|
| Content-Type  | application/json   |

### Request Body
```json
{
  "eventId": 3,
  "availableDt": "2025-08-05",
  "availableTime": "10:30",
  "userLanguage":"ar",
  "messageid":""

}
```

| Field        | Type   | Required | Description                                  |
|--------------|--------|----------|----------------------------------------------|
| eventId      | number | Yes      | Unique ID of the existing appointment.       |
| availableDt  | string | Yes      | Selected new date for rescheduling (`YYYY-MM-DD`). |
| availableTime  | string | Yes      | Selected new time for rescheduling (`YYYY-MM-DD`). |
| userLanguage  | string   | No      | User's preferred language (e.g., "en", "ar"). |
| messageid  | string | No      |   whatsApp messageid /  either eventId or messageid is required  |

Note: either eventid or message id must be provided
---

## Responses

### ✅ 200 OK – Rescheduling Success

```json
{
  "success": true,
  "data": null,
  "messageToUser": "Appoinment rescheduled successfully",
  "message": "Appoinment rescheduled successfully(528055)",
  "status": 200,
  "timestamp": "2025-05-26T15:41:19.433897600Z",
  "errorCode": null,
  "traceId": "094351a2c48c4166"
}
```

---

### ❌ 404 Not Found – Invalid Event ID

```json
{
  "success": false,
  "data": null,
  "messageToUser": null,
  "message": "Appointment not found for eventId: 113",
  "status": 404,
  "timestamp": "2025-05-26T15:53:59.650606800Z",
  "errorCode": "APPT-404",
  "traceId": "1ba762d5b73c4a58"
}
```

---

## Notes
- `availableDt` must match one of the dates retrieved from the `/nextAvailableDates` API.
- The API validates the event ID and reschedules only if it is active and valid.
