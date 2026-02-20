# Open-Voice-Journal

Open-Voice-Journal is a self-hosted, open-source transcription platform for secure voice memo workflows across web, PWA, and mobile.

## Vision and Goals

- Record/upload audio on phone, tablet, and desktop.
- Transcribe recordings with speaker diarization.
- Click transcript text and jump to the audio timestamp.
- Export audio, transcript, and subtitles (`txt`, `md`, `srt`, `vtt`).
- Reassign speakers and attach contact information.
- Extract conversation clips and remove silence.
- Summarize transcripts with selectable AI providers/models.
- Search voice memos by metadata, full-text, and semantic meaning.
- Archive, delete, backup, and restore recordings.

## Scope

### v1

- React web app + PWA + Android (Capacitor).
- REST API + WebSocket job progress events.
- Transcription + diarization pipeline.
- Pluggable summarization provider framework.
- Server-admin monitoring/control foundation.

### v1.x

- iOS release hardening.
- Chrome extension.
- Extended mobile local-model options.

### Future

- Music identification (deferred).

## Architecture

- Frontend: React/PWA/Capacitor (prototype in `frontend/`).
- Backend: Node.js API + workers (`backend/src`).
- Data: PostgreSQL + FTS + pgvector.
- Auth: Keycloak OIDC.
- AI: local Ollama default (`qwen2.5:7b-instruct`) + provider adapters.
- Edge/TLS: Traefik + Let's Encrypt.
- Storage: MinIO/object storage.
- Queue: Redis.

## AI Provider Selection and BYO

Users can choose provider/model per summary request.

Supported provider IDs:
- `ollama_local`
- `ollama_cloud`
- `openai`
- `anthropic`
- `deepseek`
- `custom_openai`

Bring-your-own is supported via OpenAI-compatible endpoints.

Security controls:
- Encrypted secret references (no plaintext API keys).
- Redacted logs.
- Admin allowlist/denylist policy.
- Optional local-only egress policy (`LOCAL_ONLY_SUMMARIZATION=true`).

## OpenAPI and Swagger

- OpenAPI JSON: `GET /api/openapi.json`
- Swagger UI: `GET /api/docs`

## API Contracts (Initial)

Provider registry:
- `GET /api/v1/ai/providers`
- `POST /api/v1/ai/providers`
- `PATCH /api/v1/ai/providers/:id`

Summaries:
- `POST /api/v1/recordings/:id/summaries`
- `GET /api/v1/summaries/:id`

Recordings baseline:
- `POST /api/v1/recordings`
- `GET /api/v1/recordings/:id`
- `POST /api/v1/recordings/:id/transcribe`

## Local Development

```bash
docker compose up -d
```

```bash
cd backend
npm install
npm run dev
```

## Roadmap

1. Docs/contracts baseline.
2. Provider framework + policy controls.
3. Transcription/diarization workers.
4. Search/export/archive/restore.
5. Web/PWA + Android MVP.
6. iOS + extension.

## License

MIT
