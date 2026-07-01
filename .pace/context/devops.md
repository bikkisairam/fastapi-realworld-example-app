## CI/CD
| Trigger | Workflow | Jobs |
|---|---|---|
| push/pull_request | .github/workflows/tests.yml | Run tests (alembic upgrade + scripts/test) |
| push/pull_request | .github/workflows/styles.yml | Lint (scripts/lint) |
| push/pull_request | .github/workflows/conduit.yml | API spec tests (newman + uvicorn) |
| push master | .github/workflows/deploy.yml | Build/push Docker image |

## Environment Variables
| Name | Required | Purpose |
|---|---|---|
| APP_ENV | yes | Select settings: dev/prod/test |
| DATABASE_URL | yes | PostgreSQL DSN for asyncpg |
| SECRET_KEY | yes | JWT signing secret |
| DEBUG | no | Enable debug mode |
| POSTGRES_USER | no | Local DB bootstrap (README) |
| POSTGRES_PASSWORD | no | Local DB bootstrap |
| POSTGRES_DB | no | Local DB bootstrap |
| POSTGRES_HOST | no | Local DB bootstrap |
| POSTGRES_PORT | no | Local DB bootstrap |
| DOCKER_USER | yes (deploy) | Docker Hub login |
| DOCKER_PASSWORD | yes (deploy) | Docker Hub login |

## Local Dev
1. poetry install
2. poetry shell
3. alembic upgrade head
4. uvicorn app.main:app --reload

## Deployment
Deploy: docker-compose up -d db && docker-compose up -d app
