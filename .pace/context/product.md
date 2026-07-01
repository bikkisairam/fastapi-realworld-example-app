## Vision
Purpose: Backend API for RealWorld/Conduit app using FastAPI
Users: Frontend clients, API testers, backend learners

## Target Personas
| Persona | Pain Point | Goal |
|---|---|---|
| Frontend developer | Needs stable REST API | Integrate Conduit UI with backend |
| API tester | Needs predictable responses | Verify RealWorld spec compliance |
| Backend learner | Needs reference implementation | Study FastAPI patterns |

## MVP Scope
- In Scope:
  - User registration/login with JWT
  - Current user profile update
  - Profiles follow/unfollow
  - Articles CRUD + feed + favorites
  - Comments CRUD for articles
  - Tags listing
- Out of Scope:
  - Frontend UI
  - Payments or subscriptions
  - Admin moderation console
  - Multi-tenant or multi-db support

## Strategic Constraints
| Constraint | Reason |
|---|---|
| PostgreSQL required | asyncpg + DATABASE_URL in settings |
| JWT auth with "Token" prefix | authentication dependency enforces prefix |
| API served under /api | AppSettings.api_prefix |
