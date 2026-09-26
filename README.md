# CyberPath Advisor — Full Project

Two separate folders, two separate servers:

```
cyberpath-backend/     Express API (port 5000) — scoring, career mapping, AI features
cyberpath-frontend/    Next.js + Tailwind app (port 3000) — all 8 screens + mascot
```

## Quick start (two terminals)

**Terminal 1 — backend:**
```bash
cd cyberpath-backend
npm install
cp .env.example .env
# edit .env — add your ANTHROPIC_API_KEY
npm run dev
```
Runs at `http://localhost:5000`. Check `curl http://localhost:5000/api/health`.

**Terminal 2 — frontend:**
```bash
cd cyberpath-frontend
npm install
cp .env.local.example .env.local
npm run dev
```
Runs at `http://localhost:3000`. The `NEXT_PUBLIC_API_URL` in `.env.local`
already points at `http://localhost:5000` — change it if you deploy the
backend somewhere else.

**Backend must be running before you open the frontend** — the assessment
page fetches quiz questions from it on load.

## The 8 screens (all built)

| Screen | Route | What it does |
|---|---|---|
| Landing | `/` | Hero + mascot greeting + "Get started" |
| Registration | `/register` | Name + email, saved locally |
| Interest Selection | `/interests` | Pick a track (or "not sure") |
| Assessment | `/assessment` | Step-through quiz, pulled live from the backend |
| Dashboard | `/dashboard` | Score bars across all 5 tracks |
| Career Recommendation | `/recommendation` | Best-fit role + AI explanation |
| Roadmap | `/roadmap` | Weekly plan + certificate generation |
| Mentor | `/mentor` | Curated free communities |

Data flows through the pages via `localStorage` (see `lib/storage.js`) —
no auth, no database needed, which keeps this buildable in a few hours.

## The mascot

`components/Mascot.js` — "Cy" is a hand-built SVG character (no image
assets to manage) that pops in with a bounce, waves continuously, and
opens a speech bubble with a page-specific message a moment after landing.
Click Cy anytime to reopen the bubble if dismissed.

It's on every page with a message tuned to that screen — encouragement
during the assessment, a personalized greeting on the dashboard once the
student's name is known, etc. This is the one deliberately playful,
high-motion element; everything else in the design stays calm around it
so Cy is what people remember.

## Design system

Rounded, warm, "student-friendly" — not the generic AI-app look:
- **Palette:** soft off-white background, navy for headings/dark panels,
  coral for primary actions, mint/sky/lilac/amber for track-score variety
- **Type:** Fredoka (rounded, friendly) for headings, Inter for body text
- **Shape language:** big radius corners, soft shadows, chip-style buttons

## Known simplifications (call these out if judges ask)

- **Auth:** none — state lives in the browser via `localStorage`. Fine for
  a demo; would need real accounts for production.
- **Resume upload:** the backend has `/api/resume-analysis` ready, but
  it's not wired into a frontend screen yet — parsing PDFs client-side
  was cut for time. Paste-box text input would be the fastest way to add
  it if there's time left.
- **Known skills for gap analysis:** currently passed as an empty list
  (`knownSkills: []`) when building the roadmap, so the AI works from the
  track's full requirement list. A nice next step: derive known skills
  from quiz answers with a strong score in a category.
- **Certificate:** SVG, not PDF — intentional, keeps the build dependency-free.

## Testing the backend independently

```bash
curl http://localhost:5000/api/quiz
curl -X POST http://localhost:5000/api/score \
  -H "Content-Type: application/json" \
  -d '{"answers":[{"questionId":"q1","optionIndex":2}]}'
```
