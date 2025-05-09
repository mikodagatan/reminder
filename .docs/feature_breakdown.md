# Feature Breakdown

This document details the features of the Reminder Application.

## Core Features

### 1. User Account Management
    - Sign up (Email/Password, OAuth - Google)
    - Log in
    - Profile Management (Name, Email, Notification Preferences)
    - Password Reset

### 2. Reminder Creation & Management
    - **Simplified Reminder Form:**
        - Title/Name of the reminder
        - Optional description
        - Due Date & Time
        - Recurrence options (Daily, Weekly, Monthly, Yearly, Custom)
        - Priority level (Low, Medium, High) - *Potentially used by AI scheduler*
    - **View Reminders:**
        - List view (All, Upcoming, Overdue)
        - Calendar view (Optional - if it can be kept simple)
    - **Edit Reminders**
    - **Delete Reminders**
    - **Mark as Complete/Snooze**

### 3. Notification System
    - **Email Notifications:**
        - Send email X time before due date (configurable by user or AI)
        - Daily/Weekly digest of upcoming reminders (optional)
    - **PWA Notifications (Rails 8):**
        - Real-time push notifications to the user's device
        - Snooze/Mark complete directly from notification (if platform allows)
    - **In-App Notifications:**
        - A dedicated section within the app listing recent notifications/alerts.

### 4. AI-Powered Scheduling
    - **Smart Scheduling Suggestions:**
        - Suggest optimal reminder times based on user's past behavior, type of reminder, and stated preferences.
        - Analyze reminder descriptions (using NLP) to suggest categories or urgency.
    - **Adaptive Reminders:**
        - Adjust reminder frequency or timing if a user frequently snoozes or misses certain types of reminders.
        - Learn user's peak productivity/availability times.
    - **Automatic Rescheduling:**
        - Option to allow AI to reschedule conflicting or overdue reminders intelligently.

### 5. Warranty Tracking
    - **Warranty Input Form:**
        - Product Name
        - Purchase Date
        - Warranty Expiry Date
        - Upload receipt/warranty document (image or PDF)
        - Optional notes
    - **Warranty Reminders:**
        - Notify user X days/weeks before warranty expires.
    - **View & Manage Warranties:**
        - List of all warranties
        - Search/filter warranties

## Non-Functional Requirements

### 1. User Experience (UX) & User Interface (UI)
    - **Intuitive and Simple Design:** Prioritize ease of use above all. Minimalist interface.
    - **Responsive Design:** PWA should work seamlessly on desktop, tablet, and mobile.
    - **Accessibility:** Adhere to WCAG guidelines.

### 2. Performance
    - Fast load times.
    - Quick response for creating/editing reminders.
    - Efficient background processing for notifications and AI tasks.

### 3. Scalability
    - Architecture should support a growing number of users and reminders.

### 4. Security
    - Secure user authentication and data storage.
    - Protection against common web vulnerabilities.

### 5. Reliability
    - Notifications must be delivered reliably.
    - Data integrity for reminders and warranties.

## Future Considerations (Post-MVP)
    - Integrations with other calendars (e.g., Google Calendar, Outlook Calendar) for viewing (not necessarily managing).
    - Sharing reminders with other users of the app.
    - Location-based reminders (if PWA capabilities allow easily).
    - Gamification elements to encourage task completion.
