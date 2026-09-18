# KConnecta User Backend

Spring Boot backend for the KConnecta user-facing application. It exposes REST APIs and WebSocket/STOMP realtime features for the React frontend, with integrations for PostgreSQL, Redis, Cloudinary, LiveKit, email delivery, and AI moderation.

## Project Summary

| Area | Implementation |
|---|---|
| Runtime | Java 21, Spring Boot 3.5.5, Maven |
| API layer | REST controllers for auth, users, posts, chat, live, groups, albums, collections, notifications, policy, settings, and moderation |
| Realtime | WebSocket/STOMP support for chat, notifications, call signaling, and live-related flows |
| Persistence | Spring Data JPA with PostgreSQL configuration |
| Cache/search | Redis/Jedis dependencies and configuration for cache/search-backed workflows |
| Authentication | Spring Security, JWT support, refresh/session-oriented configuration, and Google client ID support |
| Media | Cloudinary environment-driven configuration for uploaded media |
| Live streaming | LiveKit server SDK with optional egress and S3-compatible storage settings |
| Moderation | Gemini-backed moderation settings through environment variables |
| Secrets | Production secrets are expected from environment variables; local files contain development placeholders only |

## Requirements

- Java 21
- Maven 3.9+
- PostgreSQL
- Redis when cache/search flows are enabled

## Configuration

Use `.env.example` as the local setup template. The main runtime configuration is environment-driven.

| Variable | Purpose |
|---|---|
| `DB_URL`, `DB_USERNAME`, `DB_PASSWORD` | PostgreSQL connection |
| `JWT_SECRET` | JWT signing secret |
| `INTERNAL_API_KEY` | Internal service API key |
| `GOOGLE_CLIENT_ID` | Google OAuth client ID |
| `MAIL_USERNAME`, `MAIL_PASSWORD` | SMTP account |
| `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` | Cloudinary integration |
| `LIVEKIT_URL`, `LIVEKIT_API_KEY`, `LIVEKIT_API_SECRET` | LiveKit integration |
| `GEMINI_API_KEYS` or `GEMINI_API_KEY` | AI moderation provider keys |

Do not commit real `.env` files or production credentials.

## Run Locally

```bash
mvn spring-boot:run
```

For local development, run with the `local` profile and override placeholder values through private environment variables when testing external integrations.

## Security Notes

- `application.yml` and deployment profiles read sensitive values from environment variables.
- `application-local.yml` includes local development placeholders such as local JWT/internal keys; they are not production credentials.
- `livekit.dev.yaml` is a development example and must not be reused for production.
- Keep database passwords, JWT secrets, Cloudinary secrets, LiveKit secrets, email passwords, and Gemini keys outside Git.
