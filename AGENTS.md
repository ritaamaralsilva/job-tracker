# Job Tracker — Project Instructions

## Project goal

Build a local-first application that automatically tracks job applications by analysing Gmail messages and extracting relevant application events.

The application must track applications, companies, positions, application dates, interviews, assessments, rejections, offers, follow-ups and communication history.

Historical tracking starts on 1 November 2026.

## Architecture

- Backend: Python 3.12+, FastAPI, SQLAlchemy 2.
- Database: SQLite, with Alembic migrations.
- Frontend: React, TypeScript and Vite.
- AI: Ollama running locally, using Qwen3 14B.
- Email integration: Gmail API with OAuth2.
- Testing: Pytest for backend; frontend tests to be introduced when needed.
- Scheduling: macOS launchd for daily scans.
- Deployment: local macOS environment. No cloud infrastructure required.

## Architecture principles

1. Keep business logic independent of the LLM.
2. The LLM must never access or modify the database directly.
3. All database operations must pass through validated backend services.
4. Use structured JSON outputs and validate them with Pydantic.
5. Preserve the source of every detected event.
6. Avoid duplicate messages and events.
7. Uncertain classifications or application matches must be flagged for manual review.
8. Never send emails automatically.
9. Keep credentials, OAuth tokens and personal email data out of Git.
10. Prefer simple, modular implementations over unnecessary frameworks.

## Core domain entities

- Application
- ApplicationEvent
- SourceMessage
- ScanRun

## Application statuses

- Applied
- Acknowledged
- Under Review
- Interview
- Assessment
- Awaiting Feedback
- Offer
- Rejected
- Withdrawn

"No Response" should be calculated from inactivity rather than treated as a terminal application status.

## Event types

- APPLICATION_SUBMITTED
- APPLICATION_CONFIRMED
- APPLICATION_VIEWED
- INTERVIEW_INVITATION
- INTERVIEW_SCHEDULED
- INTERVIEW_COMPLETED
- ASSESSMENT_REQUESTED
- REJECTION_RECEIVED
- OFFER_RECEIVED
- FOLLOW_UP_SENT
- FEEDBACK_RECEIVED

## AI agent principles

The local AI agent will:
- Classify incoming messages.
- Extract company, position, event type, dates and relevant details.
- Suggest matching existing applications.
- Request manual review when confidence is insufficient.
- Suggest follow-up actions.

The agent must use explicitly defined backend tools. It must not have unrestricted database or filesystem access.

## Development workflow

- Implement one milestone at a time.
- Do not implement future milestones prematurely.
- Run relevant tests after every implementation task.
- Do not silently change existing architecture or dependencies.
- Explain important design decisions.
- Report modified files, commands executed, test results and known limitations.
- Stop and report blockers rather than inventing solutions.

## Privacy and security

All email processing and AI inference should run locally wherever possible. Gmail access must use read-only permissions initially. OAuth credentials and tokens must never be committed to the repository.