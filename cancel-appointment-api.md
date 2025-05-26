# 📘 API Specification: Cancel Appointment

## Endpoint
**POST** `/chatbotapi/appointment/cancel`  
**Base URL**: `http://localhost:8010`

---

## Purpose
This API is called when a **user opts to cancel their appointment** via WhatsApp. The cancellation reason is submitted by the user and recorded in the system.

---

## Request

### URL
```
POST /chatbotapi/appointment/cancel
```

### Headers
| Header        | Value              |
|---------------|--------------------|
| Content-Type  | application/json   |

### Request Body
```json
{
  "eventId": 3,
  "reason": "travelling.."
}
```

| Field   | Type   | Required | Description                                |
|---------|--------|----------|--------------------------------------------|
| eventId | number | Yes      | Unique ID of the appointment to cancel.    |
| reason  | string | Yes      | Reason for cancellation provided by user.  |

---

## Responses

### ✅ 200 OK – Appointment Cancelled

```json
{
  "success": true,
  "data": null,
  "messageToUser": "Your appointment with General Medicine (Alnahda Hospital ) on 2025-05-30 has been cancelled",
  "message": "Your appointment has been cancelled",
  "status": 200,
  "timestamp": "2025-05-26T15:20:48.385271800Z",
  "errorCode": null,
  "traceId": "29872c9326a54a54"
}
```

---

### ❌ 400 Bad Request – Already Cancelled (Arabic)

```json
{
  "success": false,
  "data": null,
  "messageToUser": "تم إلغاء الموعد مسبقًا.",
  "message": "Appointment is already cancelled.",
  "status": 400,
  "timestamp": "2025-05-26T15:17:38.726208100Z",
  "errorCode": "APPT-002",
  "traceId": "c7ef723083424dac"
}
```

---

### ❌ 400 Bad Request – Already Cancelled (English)

```json
{
  "success": false,
  "data": null,
  "messageToUser": "Appointment is already cancelled.",
  "message": "Appointment is already cancelled.",
  "status": 400,
  "timestamp": "2025-05-26T15:19:06.406288800Z",
  "errorCode": "APPT-002",
  "traceId": "84310c1e44f34ca5"
}
```

---

## Notes
- This API ensures that a cancelled appointment is not cancelled again.
- Responses include user-facing localized messages.
- The `reason` is stored for audit and analytics.
