# 📘 API Specification: Get Next Available Appointment Dates

## Endpoint
**POST** `/appointment/nextAvailableDates`  
**Base URL**: `{{see the mail}}`

---

## Purpose
This API returns the **next available appointment dates** for a patient's current appointment. It is used to **reschedule** when the patient is unable to attend the scheduled appointment.

The system uses the `eventId`, which uniquely identifies the patient’s existing appointment. This ID is also sent via WhatsApp during appointment reminders.

---

## Request

### URL


### Headers
| Header        | Value              |
|---------------|--------------------|
| Content-Type  | application/json   |

### Request Body
```
{
  "eventId": 3
}

✅ 200 OK - Success
{
  "success": true,
  "data": [
    { "appdt": "2025-06-22" },
    { "appdt": "2025-06-23" },
    { "appdt": "2025-06-24" },
    { "appdt": "2025-06-25" },
    { "appdt": "2025-06-26" },
    { "appdt": "2025-06-29" },
    { "appdt": "2025-06-30" },
    { "appdt": "2025-07-01" },
    { "appdt": "2025-07-02" },
    { "appdt": "2025-07-03" }
  ],
  "messageToUser": null,
  "message": "10 Record(s) Found (eventId:3)",
  "status": 200,
  "timestamp": "2025-05-26T14:37:11.525673300Z",
  "errorCode": null,
  "traceId": "2f6190f001bc41c4"
}

❌ 404 Not Found - Invalid Event ID

{
  "success": false,
  "data": null,
  "messageToUser": null,
  "message": "No appointment found for eventId: 3111",
  "status": 404,
  "timestamp": "2025-05-26T14:41:59.720014700Z",
  "errorCode": "APPT-404",
  "traceId": "677960992acb4bdf"
}

❌ 400 Bad Request - No Free Slots

{
  "success": false,
  "data": [],
  "messageToUser": "No Free slots available for the given date; Please try with another date",
  "message": "No Free slots available for the given date(EventId:3, EstCode:20068, clinicId:200, startAfterDays:1, maxDays:0)",
  "status": 400,
  "timestamp": "2025-05-26T14:43:44.706371300Z",
  "errorCode": "APPT-001",
  "traceId": "a019ff4a57ad4e5a"
}

❌ 400 Bad Request - Arabic Localized Message

{
  "success": false,
  "data": [],
  "messageToUser": "لا توجد مواعيد شاغرة في التاريخ المحدد؛ يرجى المحاولة بتاريخ آخر",
  "message": "No Free slots available for the given date(EventId:3, EstCode:20068, clinicId:200, startAfterDays:1, maxDays:0)",
  "status": 400,
  "timestamp": "2025-05-26T14:44:30.665651600Z",
  "errorCode": "APPT-001",
  "traceId": "fd8779f9ccd34996"
}
```
Notes
The eventId is required and uniquely identifies an appointment.

This API supports multilingual responses for messageToUser.

The date format in the data field is YYYY-MM-DD.

Used as part of chatbot-driven rescheduling logic.
