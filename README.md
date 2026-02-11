# Configuring Notifications for Critical Incidents

## Overview
This repository demonstrates how an email notification was configured in ServiceNow to monitor critical incidents for the Infinity (HHD) service offering. The implementation focused on creating a targeted notification, dynamically resolving recipients through service ownership, and validating notification delivery through system logs.

This project simulates a real-world scenario where stakeholders require immediate awareness when high-impact incidents affect a specific service offering.

## Use Case
As organizations manage multiple service offerings, critical incidents must be escalated quickly to the correct owners and support teams. Automated notifications ensure that high-priority issues receive prompt attention without relying on manual communication.

In this scenario, the Infinity (HHD) service required automated alerts whenever a Priority 1 incident became active. The notification was configured to notify both service ownership and the Training Technology Support group, providing timely visibility into critical service disruptions.

This project reflects a practical implementation of ServiceNow notifications for operational awareness and escalation.

## Features
- Email notification configured on the Incident table
- Conditional triggering for active Priority 1 incidents
- Scoping based on a specific service offering
- Dynamic recipient resolution using dot-walking
- Group-based notification delivery
- Dynamic subject and message content
- Validation through system email logs
  
## Technologies Used
- ServiceNow Platform
- Email Notifications
- Incident Management
- Service Offerings
- Dot-walking
- System Mailboxes

## Implementation Walkthrough

### Objective
Configure and validate an email notification that alerts service owners and a support group when a critical incident is active for the Infinity (HHD) service offering.

### Step 1: Create the Email Notification
The Email Notifications module was accessed to create a new notification record. Annotations were enabled to review system guidance during configuration. The notification was named **P1 Infinity (HHD) Incident** and associated with the **Incident** table.

### Step 2: Configure Notification Trigger Conditions
The notification was configured to send when an incident record was inserted or updated. Conditions were applied to ensure the notification triggered only when the incident was active, classified as **Priority 1 – Critical**, and associated with the **Infinity (HHD)** service offering.

<img width="1901" height="326" alt="Screen Shot 2026-02-10 at 9 06 45 PM" src="https://github.com/user-attachments/assets/fe81d8a6-4e35-4c0f-9fb3-72b74dd21daa" />

### Step 3: Configure Dynamic User Recipients
Recipient resolution was configured using dot-walking to dynamically identify users based on ownership fields. The **Service → Owned by** field was selected to notify the Training service owner. The **Service offering → Owned by** field was added to notify the Infinity (HHD) service offering owner. These fields were locked to preserve configuration integrity.

<img width="1901" height="295" alt="Screen Shot 2026-02-10 at 9 12 42 PM" src="https://github.com/user-attachments/assets/b187bebc-4215-421f-85ba-07c7b4dce1f7" />

### Step 4: Add Support Group Recipients
Group-based delivery was enabled by selecting the **Training Technology Support** group as a recipient. The group selection was locked after verification to ensure consistent delivery to the support team.

<img width="1901" height="183" alt="Screen Shot 2026-02-10 at 9 13 43 PM" src="https://github.com/user-attachments/assets/d19317a3-9373-4c39-96a4-e35723e73a46" />

### Step 5: Define Notification Content
The notification subject was configured as **IMPORTANT! P1 Infinity (HHD) Incident ${number}**, dynamically appending the incident number. The message body was configured to include a direct link to the incident record using the `${URI_REF}` variable.

<img width="1901" height="497" alt="Screen Shot 2026-02-10 at 9 16 53 PM" src="https://github.com/user-attachments/assets/e534b25c-b0b6-423a-ae6a-d705366a7310" />

### Step 6: Preview and Validate Notification Configuration
The notification preview feature was used to confirm subject formatting, message content, and recipient resolution. This validation confirmed that dynamic variables rendered correctly.

<img width="1901" height="497" alt="Screen Shot 2026-02-10 at 9 17 36 PM" src="https://github.com/user-attachments/assets/796a8ad6-8583-47af-af58-b9622fb2df83" />

### Step 7: Trigger Notification via Incident Creation
A new incident was created while impersonating **Beth Anglin**. The incident was configured with High impact and urgency, resulting in a Priority 1 classification, and associated with the Infinity (HHD) service offering. The record was saved to trigger the notification.

<img width="1901" height="394" alt="Screen Shot 2026-02-10 at 9 19 57 PM" src="https://github.com/user-attachments/assets/ff0ac862-cb29-477e-8f2c-7272d35704eb" />

### Step 8: Verify Notification Delivery
The system outbound email log was reviewed to confirm the notification was generated. The email preview validated correct subject content, recipient resolution, and functional linking to the incident record.

<img width="1901" height="216" alt="Screen Shot 2026-02-10 at 9 33 25 PM" src="https://github.com/user-attachments/assets/6e37cf61-7d50-4dbf-a1d1-bd98d8f07d8c" />

## Lessons Learned
- Notifications can be precisely scoped using service offerings and record conditions
- Dot-walking enables scalable recipient management without hardcoded users
- Service ownership fields support dynamic escalation workflows
- Group recipients ensure operational teams receive critical alerts
- System email logs are essential for validating notification behavior
