# GEMINI.md - Project Context

## Project Overview

**SAMRA** is a SaaS Website Builder specialized in creating stunning 3D animated landing pages without code. It features real-time collaboration (Google Docs-style) and targets non-technical users.

*   **Tagline:** "3D Landing Pages, No Code Required"
*   **Core Innovation:** Hides Three.js complexity behind visual presets, converts photos to 3D effects, and supports real-time multiplayer editing.

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Runtime/PM** | [Bun](https://bun.sh/) | Fast JavaScript runtime & package manager |
| **Framework** | [TanStack Start](https://tanstack.com/start/latest) | Type-safe full-stack React framework |
| **3D Engine** | Three.js + React Three Fiber | WebGL rendering, 3D graphics |
| **Styling** | Tailwind CSS v4 | Utility-first styling |
| **Components** | shadcn/ui | Accessible UI primitives |
| **Auth** | Clerk | User authentication |
| **Multi-tenancy** | Better Auth | Organizations, teams, roles |
| **Backend** | Convex | Real-time database, auto-sync |
| **Animations** | Framer Motion + GSAP | Smooth transitions |
| **Linting** | [Biome](https://biomejs.dev/) | Fast linting + formatting |
| **Deployment** | Nitro (Vercel) | Agnostic deployment adapter |

## Project Structure

The project follows a standard TanStack Start structure (using `src/` instead of `app/`).

```
samra/
├── .cta.json           # TanStack configuration
├── biome.json          # Biome configuration
├── bun.lock            # Bun lockfile
├── package.json        # Dependencies
├── vite.config.ts      # Vite config
├── convex/             # (Planned) Backend & Database Schema
│   ├── schema.ts
│   └── ...
├── public/             # Static assets
└── src/
    ├── components/     # React components
    │   ├── ui/         # (Planned) shadcn/ui components
    │   ├── editor/     # (Planned) Builder components
    │   └── landing/    # (Planned) Marketing site components
    ├── data/           # Static data
    ├── lib/            # (Planned) Utilities
    │   ├── three/      # Three.js utils
    │   ├── convex.ts   # Convex client
    │   └── utils.ts    # General utils
    ├── routes/         # File-based routes
    │   ├── __root.tsx  # Root layout
    │   └── index.tsx   # Homepage
    ├── routeTree.gen.ts # Auto-generated route definitions
    └── styles.css      # Global styles
```

## Building and Running

### Development
```bash
bun run dev
```
*Runs on `http://localhost:3000`*

### Production
```bash
bun run build
bun run serve
```

### Code Quality
```bash
bun run check   # Lint & Format check
bun run format  # Fix formatting
bun run test    # Run tests
```

## Development Phases

### Phase 1: Foundation & Landing Page (Current)
**Goal:** Working marketing website with 3D hero section.
1.  Setup project structure (Done).
2.  Create marketing landing page (Hero, Features, Pricing, Footer).
3.  Implement Three.js animation in Hero.
4.  Responsive design & Deploy.

### Phase 2: Authentication & Dashboard
**Goal:** User sign-up, workspaces, and project management (Clerk + Better Auth + Convex).

### Phase 3: Template System
**Goal:** 5 pre-built animated 3D templates and a selection gallery.

### Phase 4: Visual Builder - Core
**Goal:** Simple block-based editor with 3-panel layout (Layers, Preview, Properties).

### Phase 5: Three.js Integration
**Goal:** Image-to-3D features (background removal, depth maps).

### Phase 6: Real-Time Collaboration
**Goal:** Multi-user editing, cursors, and conflict resolution.

### Phase 7: Publishing System
**Goal:** Export pipeline and subdomain hosting.

### Phase 8: Polish & Launch
**Goal:** Onboarding, payments (Stripe), and documentation.

## Critical Requirements

*   **Non-Technical Focus:** No technical jargon ("metalness", "XYZ"). Use visual presets and simple language.
*   **Performance:** Mobile-first. Lighthouse > 70. Initial load < 3s. Lazy load 3D assets.
*   **Security:** Input sanitization, file validation, CSRF protection.
*   **Documentation:** Essential. Document purpose, props, and usage for every component.

## Development Conventions

*   **TypeScript:** Strict mode, no `any`, Zod schemas.
*   **React:** Functional components, custom hooks.
*   **Styling:** Tailwind CSS utility classes (v4). No inline styles.
*   **Naming:** `PascalCase` for Components, `camelCase` for utilities.
*   **Commits:** Conventional Commits (e.g., `feat: add template gallery`, `fix: mobile rendering`).
*   **Code Style:** Adhere to **Biome** rules (Tabs, Double Quotes).

## Current Status (Nov 30, 2025)

*   **Status:** Project setup complete.
*   **Active Task:** **Phase 1 - Landing Page**.
*   **Next Action:** Install Three.js dependencies and build the 3D Hero section.