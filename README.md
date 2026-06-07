# Gaming Shop

A full-stack gaming-store web app — browse games with filtering, sorting, and
search, plus admin CRUD for games, genres, and developers (with image uploads).

**Live:** <https://gameshop.axlothecook.com> — self-hosted on a Raspberry Pi,
exposed via Cloudflare Tunnel.

The project is split across three repositories. Pick the one you want to view:

| Repository | What it is |
| --- | --- |
| [**Front end**](https://github.com/axlothecook/Gaming-shop-frontend) | SvelteKit web UI (adapter-node). The user-facing app. |
| [**Back end**](https://github.com/axlothecook/Gaming-Shop) | Node.js + Express + MongoDB REST API. Image storage on Cloudflare R2. |
| [**Deploy**](https://github.com/axlothecook/gaming-shop-deploy) | Docker Compose orchestration + Cloudflare Tunnel for the Raspberry Pi deploy. |

## How it fits together

```
Browser ─▶ Cloudflare Tunnel ─▶ Frontend (SvelteKit) ─▶ Backend (Express API) ─▶ MongoDB
                                                              │
                                                              └─▶ Cloudflare R2 (images.axlothecook.com)
```

- The **front end** renders the UI and forwards form actions to the back end.
- The **back end** owns all data (games/genres/developers) and uploads images to
  Cloudflare R2, serving them from `images.axlothecook.com`.
- The **deploy** repo ties everything together with Docker Compose and runs the
  whole stack (plus MongoDB and `cloudflared`) on a Raspberry Pi. CI builds the
  images and auto-deploys on push.

## Tech stack at a glance

- **Front end:** SvelteKit, TypeScript, Vite, Sass
- **Back end:** Node.js, Express 5, MongoDB, multer, Cloudflare R2 (S3 SDK)
- **Infra:** Docker / Docker Compose, GitHub Actions (GHCR), Cloudflare Tunnel,
  Raspberry Pi
