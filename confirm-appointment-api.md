# 📘 API Specification: Confirm Appointment

## Endpoint
**POST** `/chatbotapi/appointment/confirm`  
**Base URL**: `http://localhost:8010`

---

## Purpose
This API is triggered when a **patient confirms their appointment** via WhatsApp. It is used in response to the **appointment reminder messages** sent by MOH (Ministry of Health).

---

## Request

### URL
```
POST /chatbotapi/appointment/confirm
```

### Headers
| Header        | Value              |
|---------------|--------------------|
| Content-Type  | application/json   |

### Request Body
```json
{
  "eventId": 3,
  "userLanguage": "ar"
}
```

| Field         | Type     | Required | Description                                    |
|---------------|----------|----------|------------------------------------------------|
| eventId       | number   | Yes      | Unique ID of the appointment.                 |
| userLanguage  | string   | Yes      | User's preferred language (e.g., "en", "ar"). |

---

## Responses

### ✅ 200 OK – Arabic Confirmation

```json
{
  "success": true,
  "data": null,
  "messageToUser": "تم تأكيد موعدك مع الطب العام (المستشفى المركزي) في ٢٦ مايو ٢٠٢٥",
  "message": "Your appointment with الطب العام(المستشفى المركزي) on ٢٦ مايو ٢٠٢٥ is confirmed",
  "status": 200,
  "timestamp": "2025-05-26T15:07:41.408332700Z",
  "errorCode": null,
  "traceId": "fb68d7a460b64e1b"
}
```

---

### ✅ 200 OK – English Confirmation

```json
{
  "success": true,
  "data": null,
  "messageToUser": "Your appointment with GENERAL MEDICINE(DGIT) on 2025-05-26 is confirmed",
  "message": "Your appointment with GENERAL MEDICINE(DGIT) on 2025-05-26 is confirmed",
  "status": 200,
  "timestamp": "2025-05-26T15:08:19.001075700Z",
  "errorCode": null,
  "traceId": "c5d8d6a8c7894b9c"
}
```

---

## Notes
- `eventId` identifies the appointment in the central MOH system.
- `userLanguage` is used to personalize the response in the user’s preferred language (currently supports Arabic and English).
- This endpoint does not return any `data` object; it only confirms the appointment and provides a message to the user.
- `messageToUser` is intended for WhatsApp replies, localized for better user experience.
