---
language: python
package_manager: poetry
test_runner: pytest
test_command: "poetry run ./scripts/test"
test_file_pattern: "tests/**/*.py"
require_tests: true
---
## Module Map
| Directory | Language | Purpose |
|---|---|---|
| app | Python | FastAPI application entrypoint |
| app/api | Python | HTTP routes, deps, errors |
| app/core | Python | settings, logging, startup |
| app/db | Python/SQL | asyncpg repos + SQL queries |
| app/models | Python | Pydantic domain + schemas |
| app/services | Python | auth/jwt utilities |
| app/resources | Python | API message strings |
| tests | Python | pytest suite |
| scripts | Bash | lint/test helpers |
| postman | JSON/Bash | API spec tests |

## Tech Stack
| Component | Technology |
|---|---|
| Web framework | FastAPI, Starlette |
| ASGI server | Uvicorn |
| DB access | asyncpg, aiosql, pypika |
| Migrations | Alembic |
| Auth | JWT (pyjwt), passlib bcrypt |
| Validation | Pydantic |
| Logging | loguru |
| Testing | pytest, httpx, asgi-lifespan |

## System Architecture
| Flow | Details |
|---|---|
| HTTP request | FastAPI app in app/main.py with CORS + exception handlers |
| API routing | /api prefix includes auth, users, profiles, articles, comments, tags |
| Data access | Repositories use asyncpg connection pool + aiosql queries |
| Startup/shutdown | connect_to_db/close_db_connection in app/db/events.py |

## Key Interfaces & Contracts
| Interface | Details |
|---|---|
| API base path | /api (AppSettings.api_prefix) |
| Auth header | Authorization: "Token <jwt>" (RWAPIKeyHeader) |
| Error shape | {"errors": [...]} in http_error_handler/http422_error_handler |
| Config | env vars via BaseSettings (.env, prod.env) |

## Coding Conventions
| Area | Standard |
|---|---|
| Formatting | black, isort (scripts/format) |
| Linting | flake8 (wemake), mypy (scripts/lint) |
| Pydantic style | RWModel alias_generator camelCase |
| Error handling | raise HTTPException with strings from app/resources/strings.py |

## Test Patterns
| Pattern | Details |
|---|---|
| Runner | pytest via scripts/test |
| Fixtures | tests/conftest.py app/client/token fixtures |
| Async tests | pytest.mark.asyncio + httpx AsyncClient |
| DB isolation | FakeAsyncPGPool transaction rollback |
