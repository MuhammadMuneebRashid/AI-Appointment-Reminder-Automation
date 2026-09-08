# 📅 AI Appointment Reminder Automation

An intelligent **n8n workflow** that automatically monitors upcoming appointments and sends personalized reminder emails to customers approximately **24 hours before their scheduled appointment**.

The workflow uses **Google Sheets** for appointment management, **Google Gemini AI** for generating professional reminder emails, and **Gmail** for automated delivery. After successfully sending a reminder, the appointment status is updated in Google Sheets.

---

## 🚀 Overview

Managing appointment reminders manually can be time-consuming and can lead to missed notifications.

This automation eliminates that manual work by:

* Checking appointments automatically on a scheduled basis
* Identifying appointments occurring approximately 24 hours later
* Generating personalized reminder emails using AI
* Customizing reminders based on the appointment service
* Sending reminders directly through Gmail
* Recording reminder activity in a separate Google Sheet
* Updating the original appointment status after the email is sent

The workflow is designed to provide a reliable and scalable appointment reminder system.

---

## ✨ Features

* ⏰ **Automated Scheduling** — Runs automatically every day at the configured time.
* 📊 **Google Sheets Integration** — Reads appointment information directly from Google Sheets.
* 🧠 **AI-Powered Emails** — Uses Google Gemini to generate professional reminder messages.
* 📅 **24-Hour Reminder Detection** — Filters appointments that are approximately 24 hours away.
* ✉️ **Automated Gmail Delivery** — Sends reminder emails directly to customers.
* 🎯 **Service-Based Routing** — Supports different reminder flows depending on the appointment service.
* 📝 **Reminder Logging** — Stores reminder information in a dedicated Google Sheet.
* ✅ **Status Tracking** — Updates the original appointment record to `sent` after the reminder is delivered.
* 🔄 **Fully Automated Workflow** — Requires no manual intervention once configured.

---

## 🔄 Workflow Architecture

```text
Schedule Trigger
       ↓
Get Appointments from Google Sheets
       ↓
JavaScript Date/Time Filter
       ↓
Find Appointments ~24 Hours Away
       ↓
AI Agent + Google Gemini
       ↓
Generate Structured Reminder
       ↓
Edit Fields
       ↓
Log Reminder in Google Sheets
       ↓
Service-Based Switch
       ↓
Send Reminder via Gmail
       ↓
Update Appointment Status
```

---

## 🧩 Workflow Components

### 1. Schedule Trigger

The workflow starts automatically using an n8n Schedule Trigger.

It is configured to run at the specified scheduled time and check the appointment database for upcoming appointments.

---

### 2. Get Appointments

The workflow retrieves appointment records from **Google Sheets**.

Appointment information includes fields such as:

* Name
* Email
* Phone
* Appointment Date
* Appointment Time
* Duration
* Service
* Row Number
* Status

---

### 3. JavaScript Date & Time Filter

A JavaScript Code node calculates the time remaining until each appointment.

Only appointments approximately **24 hours away** are passed to the next stage.

The workflow uses a tolerance window of approximately:

```text
23.5 hours → 24.5 hours
```

This helps ensure that the reminder is triggered reliably around the 24-hour mark.

---

### 4. AI Agent

The selected appointment information is passed to an **AI Agent powered by Google Gemini**.

The AI generates a professional reminder email based on the customer's appointment details and service.

The generated output follows a structured format containing:

```json
{
  "row_number": "",
  "service": "",
  "subject": "",
  "mail": ""
}
```

This makes the AI response easier to process within the rest of the workflow.

---

### 5. Service-Based Routing

The workflow uses a Switch node to route the reminder according to the appointment service.

Supported service values include:

* `followup`
* `demo`
* `Consultation`
* `meeting`

Each service is connected to its own Gmail sending branch.

---

### 6. Reminder Logging

Before sending the email, the workflow appends appointment information to a dedicated **Reminder Google Sheet**.

This provides a separate record of reminder activity and can be useful for tracking and auditing.

---

### 7. Gmail Notification

The generated reminder is automatically sent to the customer's email address.

The Gmail node uses:

```text
To: Customer Email
Subject: AI Generated Subject
Message: AI Generated Reminder
```

This allows customers to receive personalized appointment reminders without manual email preparation.

---

### 8. Appointment Status Update

After the reminder email is sent, the workflow updates the corresponding appointment record in Google Sheets.

The status is changed to:

```text
sent
```

The update uses the appointment's `row_number` to identify the correct record.

---

## 🛠️ Technologies Used

| Technology        | Purpose                                    |
| ----------------- | ------------------------------------------ |
| **n8n**           | Workflow automation                        |
| **Google Sheets** | Appointment and reminder data management   |
| **Google Gemini** | AI-generated reminder emails               |
| **Gmail**         | Automated email delivery                   |
| **JavaScript**    | Appointment time calculation and filtering |

---

## 📋 Required Appointment Data

Your appointment Google Sheet should contain fields similar to:

```text
name
email
phone
appointment_date
appointment_time
duration
service
row_number
status
```

The `service` field determines which reminder route is used.

---

## ⚙️ Setup

### 1. Import the Workflow

Import the provided n8n workflow JSON into your n8n instance.

### 2. Configure Google Sheets

Connect your Google Sheets account and select:

* Appointment spreadsheet
* Appointment worksheet
* Reminder spreadsheet
* Reminder worksheet

### 3. Configure Google Gemini

Connect your Google Gemini credentials to the AI Agent.

### 4. Configure Gmail

Connect the Gmail account that will be used to send appointment reminders.

### 5. Verify Appointment Fields

Make sure your Google Sheet contains the required appointment fields and that the field names match the workflow expressions.

### 6. Activate the Workflow

After testing the workflow successfully, activate it.

The automation will then periodically check appointments and process eligible reminders automatically.

---

## 🔐 Credentials

This workflow requires authenticated connections for:

* Google Sheets
* Google Gemini
* Gmail

**Never commit credentials, API keys, OAuth tokens, spreadsheet secrets, or other sensitive information to GitHub.**

---

## 📈 Use Cases

This automation can be used for:

* Customer consultations
* Product demos
* Business meetings
* Follow-up appointments
* Service appointments
* Client onboarding
* Professional consultations
* Other scheduled customer interactions

---

## 💡 Benefits

### Save Time

Eliminates repetitive manual reminder emails.

### Improve Customer Experience

Customers receive timely and personalized appointment notifications.

### Reduce Missed Appointments

Automated reminders help customers remember upcoming appointments.

### Centralized Tracking

Appointment and reminder information remains organized in Google Sheets.

### AI-Powered Communication

Google Gemini generates professional messages based on appointment context.

### Easy to Extend

Additional services and notification channels can be added as the workflow grows.

---

## 🔮 Future Improvements

Potential enhancements include:

* WhatsApp appointment reminders
* SMS notifications
* Multiple reminder intervals
* Calendar integration
* Automatic appointment confirmation
* Reminder retry handling
* Failed-email tracking
* Customer response tracking
* HTML email templates
* Multi-language reminder generation
* Dashboard for reminder analytics

---

## 📊 Automation Result

The completed workflow provides an automated pipeline:

```text
Appointment Data
      ↓
Time-Based Detection
      ↓
AI Reminder Generation
      ↓
Service Routing
      ↓
Email Delivery
      ↓
Reminder Logging
      ↓
Appointment Status Update
```

This creates a complete **AI-powered appointment reminder system** with minimal manual intervention.

---

## 👨‍💻 Project Type

**AI Automation / n8n Workflow / Appointment Management**

Built with **n8n, Google Sheets, Google Gemini, Gmail, and JavaScript**.

---

## ⭐ Conclusion

This project demonstrates how **AI and workflow automation** can be combined to build a practical appointment management solution.

By connecting appointment data, AI-generated communication, automated email delivery, and status tracking, the workflow creates a reliable system for handling appointment reminders from start to finish.


