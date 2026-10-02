# wine.rosenkilde.it — Vin-dagbog

Multi-user wine tasting + purchase journal with bottle photos and AI label reading. Cloudflare Worker
(Hono) + D1 (`wine`) + R2 (`wine-photos`), custom domain **wine.rosenkilde.it**, like the other
subdomain apps (games., news., go. …). See README.md for setup and layout.

## Rules
- UI text is Danish. Plain HTML/CSS/JS in `public/`, no frontend build step.
- Multi-tenant: every API route must check cellar membership (`access` / `wineAccess` / `photoAccess`
  in worker/index.js). Photos are only served through the Worker, never from a public bucket URL.
- Tastings and purchases are per user; only the author or the cellar owner may delete them.
- Auth/cellar code mirrors GamesRegistration (users/sessions/leagues/memberships) — keep them alike.
- Schema changes go in a new `migrations/000N_*.sql`; never edit applied migrations.
- Label reading: worker/label.js, model `claude-opus-5-5`, structured JSON output (no forced tool use),
  `fallbacks: "default"`. Secret `ANTHROPIC_API_KEY`.

## Open tasks
- Create the GitHub repo `K-Rosenkilde/wine.rosenkilde.it` and move this folder there (it was first
  built in `K-Rosenkilde/K-Rosenkilde` under `wine/`).
- Run the one-time Cloudflare setup in README.md (D1, R2, secret, deploy).
- Add a "Vin" card to the rosenkilde.it front page (`rosenkilde-frontpage`) and a row in the portal's
  `apps` table.
