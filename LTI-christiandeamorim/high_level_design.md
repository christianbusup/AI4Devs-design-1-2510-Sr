# High-Level System Design (LTI on Google Cloud)

This document outlines the high-level architecture for the LTI Talent Operating System, leveraging **Google Cloud Platform (GCP)** to ensure scalability, security, and advanced AI capabilities.

## 1. Architecture Overview

The system follows a **Microservices Architecture** to ensure modularity and scalability, with a strong emphasis on **Event-Driven** patterns for asynchronous processing (AI tasks, notifications).

### Key Components

#### A. Frontend (Client Layer)
- **Web Application**: Built with React/Next.js.
- **Hosting**: **Firebase Hosting** (for fast content delivery) or **Cloud Run** (for SSR).
- **CDN**: **Cloud CDN** to cache static assets globally.

#### B. API Gateway & Security
- **API Gateway**: Manages API traffic, routing, and rate limiting.
- **Load Balancer**: **Global External HTTP(S) Load Balancer** for routing traffic to backend services.
- **Authentication**: **Identity Platform (Firebase Auth)** for secure user authentication (SSO, MFA).

#### C. Backend Services (Compute)
We will use **Cloud Run** (Serverless Containers) for the core application services. This allows for auto-scaling to zero and handling traffic spikes efficiently.
- **Core Service**: Manages Users, Job Roles, Organizations.
- **ATS Service**: Manages Applications, Pipelines, Workflows.
- **Interview Service**: Handles Scheduling (Calendar integrations) and Scorecards.
- **Integration Service**: **Cloud Functions** to handle webhooks and connectors with external HRIS (Workday, ADP).

#### D. Data Layer
- **Relational Database**: **Cloud SQL for PostgreSQL**. Stores structured data (Users, Jobs, Applications, relational integrity).
- **NoSQL / Real-time**: **Firestore**. Stores flexible data (Scorecards, Feedback forms) and powers real-time features (Notifications, Chat).
- **Object Storage**: **Cloud Storage**. Stores candidate resumes (PDFs), profile photos, and other unstructured media.

#### E. AI & Machine Learning (The "Brain")
- **Vertex AI**: The core platform for all AI operations.
    - **AutoML / Custom Models**: For Candidate Ranking and Bias Detection.
    - **Gemini API**: Powers the **AI Twin** (Chatbot, Auto-scheduling, Summarization).
- **Data Pipeline**: **Dataflow** for processing analytics data.
- **Data Warehouse**: **BigQuery** for storing historical data for "Organizational Bias Detection" and analytics.

#### F. Asynchronous Messaging
- **Pub/Sub**: Decouples services.
    - *Example*: When a candidate applies, an event is published. The "AI Ranking Service" subscribes to this to process the resume asynchronously.

## 2. Architecture Diagram

![alt text](system-architecture.png)

## 3. Design Decisions & Rationale

1.  **Cloud Run vs. Kubernetes (GKE)**:
    *   *Decision*: **Cloud Run**.
    *   *Rationale*: LTI is a startup. Cloud Run offers a lower operational overhead (serverless) while still using containers, allowing for easy migration to GKE later if complexity grows.

2.  **Cloud SQL (PostgreSQL)**:
    *   *Rationale*: The core data (Applications, Jobs) is highly relational and requires strong consistency. PostgreSQL is the industry standard.

3.  **Vertex AI**:
    *   *Rationale*: Provides a unified platform for both generative AI (Gemini for the "Twin") and predictive AI (Ranking/Bias), simplifying the ML Ops pipeline.

4.  **Pub/Sub**:
    *   *Rationale*: Critical for the "Agentic" nature. The AI agents need to react to events (e.g., "Candidate replied", "Interview finished") without blocking the main user flow.

## 4. Architectural Q&A & Key Considerations

### 1. User Roles & Workflows
*   **Recruiters**: Focus on high-level pipeline management and sourcing strategy. Their workflow is heavily supported by the **AI Twin** for scheduling and initial screening. They interact primarily with the **ATS Service** and **AI Agent** outputs.
*   **Hiring Managers**: Focus on **Role Intake** (defining requirements) and **Evaluation** (Scorecards). They interact with the **Core Service** (for role definition) and **Interview Service** (for feedback).
*   **Candidates**: Interact with the **Web Application** for applying and the **AI Twin** (via chat/email) for scheduling.
*   **Admins**: Manage system configuration, integrations, and view **Organizational Bias** analytics.

### 2. External Systems & Integrations
Beyond HRIS (Workday/ADP) and Calendars, the system requires:
*   **Video Conferencing (Zoom/Google Meet/Teams)**: Essential for the **AI Interview Agent** to generate meeting links dynamically.
*   **Sourcing Channels (LinkedIn/Indeed)**: For the **AI Twin** to monitor passive candidates and trigger outreach.
*   **Communication Platforms (Slack/Teams)**: For real-time notifications to Hiring Managers (e.g., "Feedback SLA" alerts).

### 3. AI-Driven Features Highlighted
The architecture explicitly isolates these features in the **Vertex AI** and **AI Agent Service** components:
*   **Candidate Ranking**: Handled by custom AutoML models triggered by application submission.
*   **Bias Detection**: Continuous monitoring model running on data in BigQuery/Firestore.
*   **Chatbot (AI Twin)**: Powered by **Gemini Pro**, managing candidate interaction.
*   **Auto-scheduling**: A logic flow within the AI Agent interacting with Calendar APIs.
*   **Summarization**: Gemini processing interview transcripts and resumes.

### 4. Diagram Focus
The provided architecture diagram focuses on **High-Level Service Interactions** and **Event-Driven Flows**.
*   *Why?* The complexity of LTI lies in the *orchestration* between standard CRUD operations (ATS) and autonomous agents.
*   *Detail*: We explicitly show the **Pub/Sub** event bus to demonstrate how the "AI Brain" is decoupled from the transactional core, ensuring that heavy AI processing doesn't slow down the user experience.

