## Sensitive Data
| Data | Where Stored | Protection |
|---|---|---|
| SECRET_KEY | Env (.env/prod.env) | Pydantic SecretStr, not in code |
| User passwords | Postgres users table | bcrypt hash + per-user salt |
| JWT tokens | Client Authorization header | HS256 signature (pyjwt) |
| Database credentials | DATABASE_URL env | Env config only |

## Trust Boundaries
| Caller | Callee | Auth Method |
|---|---|---|
| API client | FastAPI routes | JWT in Authorization header (Token prefix) |
| FastAPI app | PostgreSQL | DATABASE_URL credentials |
| GitHub Actions | Docker Hub | DOCKER_USER/DOCKER_PASSWORD secrets |

## Security Requirements
- SECRET_KEY must be provided for JWT signing/verification
- Authorization header must use Token prefix
- Passwords must be hashed with bcrypt + salt
- DATABASE_URL must be set before startup

## Security Checklist
JWT validation on protected routes: pass
Password hashing with bcrypt: pass
CORS origins restricted: fail (allowed_hosts default "*")
Secrets committed to repo: pass (uses .env.example)
