# Technical Architecture

This document outlines the proposed technical architecture for the Reminder Application.

## 1. Frontend
    - **Framework:** Progressive Web App (PWA)
        - HTML, CSS, JavaScript
        - Stimulus or a lightweight JavaScript framework for interactivity if needed beyond basic Rails UJS.
        - Tailwind CSS for styling (as indicated by `application.tailwind.css`).
    - **Key Responsibilities:**
        - Rendering UI components.
        - Handling user input and interactions.
        - Communicating with the backend API.
        - Managing PWA service worker for offline capabilities and push notifications.

## 2. Backend
    - **Framework:** Ruby on Rails 8
        - **API:** RESTful or GraphQL API for communication with the frontend.
        - **Database:** PostgreSQL (common choice for Rails, robust).
        - **Background Jobs:** Sidekiq (or similar like GoodJob if using `queue.yml`) for handling:
            - Email sending
            - PWA notification dispatch
            - AI processing tasks
    - **Key Responsibilities:**
        - User authentication and authorization.
        - Business logic for creating, managing, and scheduling reminders and warranties.
        - Storing and retrieving data from the database.
        - Interfacing with notification services.
        - Executing AI scheduling algorithms.

## 3. AI Module
    - **Language/Framework:** Ruby, potentially utilizing Ruby-based machine learning libraries (e.g., `ruby-fann`, `rumale`, `tensorflow.rb` for TensorFlow bindings if necessary, or simpler rule-based systems).
    - **Integration:**
        - Implemented as Ruby classes/modules within the Rails application.
        - Background jobs (Sidekiq/GoodJob) can be used for computationally intensive AI tasks to avoid blocking web requests.
        - For Natural Language Processing (NLP) tasks, consider Ruby gems that can perform text analysis or integrate with external NLP APIs if a purely Ruby solution is not sufficient for the desired complexity.
    - **Key Responsibilities:**
        - Analyzing reminder data.
        - Learning user patterns.
        - Providing scheduling recommendations.
        - Potentially NLP for understanding reminder text (e.g., extracting keywords, intent).

## 4. Database Schema (High-Level)
    - `users` (id, email, encrypted_password, name, notification_preferences, created_at, updated_at)
    - `reminders` (id, user_id, title, description, due_date, recurrence_rule, priority, completed_at, created_at, updated_at)
    - `notifications` (id, reminder_id, user_id, type (email, pwa, in_app), sent_at, status, created_at, updated_at)
    - `warranties` (id, user_id, product_name, purchase_date, expiry_date, document_path, notes, created_at, updated_at)
    - `ai_scheduling_data` (id, user_id, data_points for learning user behavior)

## 5. PWA Specifics
    - **Service Worker (`service-worker.js`):**
        - Caching strategies for offline access.
        - Handling push notification events.
    - **Manifest File (`manifest.json.erb`):**
        - Defines app name, icons, start URL, display mode, etc.

## 6. Key Rails Gems/Features to Utilize
    - **Action Mailer:** For email notifications.
    - **WebPush (or similar gem):** For PWA push notifications (Rails 8 might have built-in improvements).
    - **Active Job:** For queuing background tasks.
    - **Devise (or similar):** For user authentication.
    - **Pundit (or similar):** For authorization.
    - **Active Storage:** For uploading and storing warranty documents.

## 7. Deployment (Example with Kamal)
    - Docker for containerization (as suggested by `Dockerfile` and `docker-entrypoint`).
    - Kamal for deployment (as suggested by `bin/kamal` and `config/deploy.yml`).
    - Server (e.g., VPS, cloud provider like Heroku, AWS, DigitalOcean).
    - Puma as the application server (as per `config/puma.rb`).

## 8. Development & Tooling
    - **Version Control:** Git
    - **Testing:** RSpec or Minitest (default Rails)
    - **Linters:** RuboCop (as per `bin/rubocop`)
    - **CI/CD:** GitHub Actions, GitLab CI, etc.

This architecture aims for a balance between leveraging the strengths of Rails for rapid development and incorporating modern PWA and AI capabilities.
