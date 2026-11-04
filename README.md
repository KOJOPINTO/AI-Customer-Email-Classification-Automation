# AI-Powered Customer Email Classification & Recovery Automation

## Project Overview

This project is an AI-powered customer support automation system built with **Make.com, Google Gemini, Google Sheets, and Gmail**.

It automatically analyzes incoming customer emails, classifies them by category, sentiment, and urgency, and routes them through appropriate customer-support workflows.

The system also includes retry handling, error logging, duplicate prevention, email status tracking, and a manual email recovery process.

## Business Problem

Businesses receive customer inquiries with different levels of urgency. Manually reviewing, prioritizing, and responding to every email can delay customer support and increase operational workload.

This automation helps businesses organize incoming inquiries, identify urgent cases, and improve response management.

## Technologies Used

- Make.com – Workflow automation and integration
- Google Gemini API – AI-powered email classification
- Google Sheets – Customer inquiry tracking and error logging
- Gmail – Automated email notifications
- JSON – Structured AI response processing

## Key Features

### 1. AI-Powered Email Classification
Gemini analyzes customer messages and returns structured information:
- Category
- Sentiment
- Urgency
- Summary

### 2. Priority-Based Routing
Customer inquiries are routed into:
- High priority
- Medium priority
- Low priority

Each route has its own Google Sheets tracking and Gmail notification actions.

### 3. Duplicate Prevention
Google Sheets Search Rows checks whether a customer email already exists before a new record is created.

### 4. Automatic Retry Handling
If the first Gemini API request fails, the workflow waits and attempts a second request.

### 5. Error Logging
Failed AI processing attempts are recorded in a separate Google Sheets tab for monitoring and troubleshooting.

### 6. Email Status Tracking
Customer records are updated with:
- Sent
- Not Sent

The status is updated after the Gmail action completes.

### 7. Manual Email Recovery
A separate Make.com scenario searches for records marked:
- Email Status = Not Sent
- Resend Request = Yes

It resends the customer email and updates the original record after successful processing.

The recovery scenario is scheduled to check for resend requests every 15 minutes.

## Workflow Architecture

```text
Customer Email / Webhook
          |
          v
   Gemini AI Analysis
          |
          v
       JSON Parse
          |
          v
    Priority Router
     /     |     \
   High  Medium   Low
     \     |     /
      Google Sheets
          |
          v
     Gmail Notification
          |
          v
    Update Email Status

AI Request Failure
          |
          v
       Wait 30 sec
          |
          v
     Gemini Retry
          |
          v
      JSON Parse
          |
          v
      Retry Router
          |
          v
   Priority Processing

Gmail Failure
          |
          v
   Update Existing Record
       Not Sent
          |
          v
   Manual Follow-up

Manual Recovery Scenario
          |
          v
   Search Resend Requests
          |
          v
      Gmail Resend
          |
          v
   Update Existing Record
          |
          v
    Sent / No Follow-up
```

## Business Benefits

- Reduces manual email classification.
- Helps prioritize urgent customer inquiries.
- Improves visibility into customer support activity.
- Reduces duplicate inquiry records.
- Provides visibility into processing failures.
- Supports recovery of emails that were not sent.
- Helps small businesses organize customer support operations.

## Testing and Validation

The workflow was tested using sample customer inquiries and simulated processing failures.

Testing covered:
- AI classification and JSON parsing.
- High, Medium, and Low priority routing.
- Duplicate inquiry prevention.
- Gemini API retry handling.
- Error logging.
- Email status updates.
- Manual email recovery.

## Important Considerations

- AI classifications should be reviewed where business decisions are sensitive.
- Email status `Sent` confirms that Gmail accepted the send operation; it does not guarantee delivery or that the customer read the email.
- The duplicate prevention rule uses customer email as its matching key, so repeat inquiries from the same email address may be blocked.
- Sample or synthetic customer data should be used during development. Avoid sending confidential customer information to AI services without appropriate privacy and security review.

## Project Purpose

This project demonstrates practical skills in AI integration, business process automation, API integration, workflow design, data management, error handling, and customer-support process improvement.

**Developer:** Solomon Pinto  
**Focus:** AI Automation | Business Process Automation | Data Analytics | IT Support
