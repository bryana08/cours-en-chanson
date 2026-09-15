# Cours en Chanson 🎵📚

Application qui transforme des cours manuscrits en chansons pour faciliter la mémorisation.

## Pipeline

1. **OCR** — Photo du cours manuscrit → texte (Google Cloud Vision API)
2. **Extraction** — Texte brut → concepts-clés (définitions, formules, dates)
3. **Génération de paroles** — Concepts-clés → paroles structurées (couplets/refrain)
4. **Génération audio** — Paroles → chanson (audio simple, extensible vers une API musicale)

Pipeline asynchrone via RabbitMQ : chaque étape publie un événement, évite de bloquer l'utilisateur sur une requête HTTP longue.

## Architecture — Microservices

| Service | Rôle | Stack suggérée |
|---|---|---|
| `services/api-gateway` | Point d'entrée unique, routage, auth | NestJS |
| `services/ocr` | Photo → texte (Google Vision API) | Python (FastAPI) |
| `services/extraction-paroles` | Texte → concepts-clés → paroles (LLM) | Python (FastAPI) ou NestJS |
| `services/audio` | Paroles → chanson | Python (FastAPI) |
| `services/utilisateur` | Auth, comptes, historique | NestJS |

**Infrastructure partagée** (`infra/docker-compose.yml`) :
- PostgreSQL — utilisateurs, métadonnées des chansons
- RabbitMQ — pipeline asynchrone
- MinIO — stockage photos et fichiers audio

## Structure du dépôt

```
cours-en-chanson/
├── services/
│   ├── api-gateway/
│   ├── ocr/
│   ├── extraction-paroles/
│   ├── audio/
│   └── utilisateur/
├── web/         # Application web (Next.js)
├── mobile/      # Application mobile (Flutter)
├── infra/       # Docker Compose, config infrastructure
└── docs/        # Documentation, schémas d'architecture
```

## Équipe

Projet réalisé à 4, dans le cadre d'une soutenance académique.

## Répartition suggérée

| Membre | Périmètre |
|---|---|
| 1 | `services/ocr` — upload, appel API Vision, gestion des erreurs |
| 2 | `services/extraction-paroles` + `services/audio` |
| 3 | `web/` (Next.js) |
| 4 | `mobile/` (Flutter) |

*(`api-gateway` et `utilisateur` peuvent être répartis selon l'avancement de chacun)*

## Démarrer l'infrastructure locale

```bash
cd infra
docker compose up -d
```

## Statut

🚧 En cours de développement — MVP en préparation pour soutenance.
