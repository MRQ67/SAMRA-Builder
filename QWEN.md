# Qwen Code Analysis - SAMRA Project

## Project Overview

SAMRA is a SaaS Website Builder focused on creating stunning 3D animated landing pages using Three.js, without requiring users to write code. It features Google Docs-style real-time collaboration and targets non-technical users (marketers, agencies, indie hackers).

**Tagline:** "3D Landing Pages, No Code Required"

### Core Innovation:
- **Hides Three.js complexity** behind simple visual presets
- **Converts regular photos to 3D effects** (users don't need GLTF models)
- **Real-time collaboration** (multiple users editing simultaneously)
- **Template-first approach** (20+ pre-built animated templates)

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Framework** | TanStack Start | Type-safe full-stack React framework |
| **3D Engine** | Three.js + React Three Fiber | WebGL rendering, 3D graphics |
| **Styling** | Tailwind CSS v4 | Utility-first styling |
| **Components** | shadcn/ui | Accessible UI primitives |
| **Auth** | Clerk | User authentication |
| **Multi-tenancy** | Better Auth | Organizations, teams, roles |
| **Backend** | Convex | Real-time database, auto-sync |
| **Animations** | Framer Motion + GSAP | Smooth transitions |
| **Linting** | Biome | Fast linting + formatting |
| **Package Manager** | Bun | Fast JavaScript runtime |
| **Deployment** | Nitro (Vercel initially) | Agnostic deployment adapter |

## Project Structure

```
samra/
├── app/
│   ├── routes/              # File-based routing
│   │   ├── __root.tsx      # Root layout
│   │   ├── index.tsx       # Landing page
│   │   ├── dashboard.tsx   # User dashboard
│   │   └── editor.$projectId.tsx  # Builder interface
│   │
│   ├── components/
│   │   ├── ui/             # shadcn/ui components
│   │   ├── editor/         # Builder components
│   │   │   ├── Canvas3D.tsx
│   │   │   ├── PropertyPanel.tsx
│   │   │   ├── BlockLibrary.tsx
│   │   │   └── TemplateGallery.tsx
│   │   ├── landing/        # Marketing site components
│   │   └── layout/         # Layout components
│   │
│   ├── lib/
│   │   ├── three/          # Three.js utilities
│   │   │   ├── loaders.ts
│   │   │   ├── animations.ts
│   │   │   └── image-to-3d.ts
│   │   ├── convex.ts       # Convex client
│   │   ├── clerk.ts        # Clerk config
│   │   └── utils.ts        # General utilities
│   │
│   └── styles/
│       └── globals.css
│
├── convex/
│   ├── schema.ts           # Database schema
│   ├── users.ts           # User operations
│   ├── projects.ts        # Project CRUD
│   ├── organizations.ts   # Multi-tenancy
│   └── assets.ts          # File management
│
├── public/
│   ├── templates/         # Template previews
│   └── models/            # Sample 3D models
│
└── docs/
    ├── ARCHITECTURE.md
    ├── API.md
    └── DEVELOPMENT.md
```

## Development Phases

### Phase 1: Foundation & Landing Page (Week 1-2)
**Goal:** Working marketing website with 3D hero section

**Tasks:**
1. Setup project structure (✅ DONE)
2. Create marketing landing page
   - Hero section with Three.js animation
   - Features section
   - Pricing section
   - Footer
3. Basic routing with TanStack Router
4. Responsive design with Tailwind CSS
5. Deploy to Vercel

**Deliverables:**
- Marketing site live at samra.vercel.app
- Interactive 3D hero animation
- Mobile-responsive

### Phase 2: Authentication & Dashboard (Week 3)
**Goal:** User sign-up and project management

**Tasks:**
1. Integrate Clerk authentication
   - Sign up / Sign in flows
   - OAuth providers (Google, GitHub)
   - User profile
2. Integrate Better Auth for organizations
   - Create workspace on signup
   - Multi-tenant isolation
3. Build dashboard UI
   - Project cards grid
   - Create new project button
   - Template gallery modal
4. Convex schema and queries
   - Users table
   - Organizations table
   - Projects table
5. Project CRUD operations

**Deliverables:**
- Users can sign up
- Users can create workspaces
- Users can create projects from templates
- Dashboard showing user's projects

### Phase 3: Template System (Week 4)
**Goal:** 5 pre-built animated templates

**Tasks:**
1. Design template data structure
2. Create 5 templates:
   - Floating Product Showcase
   - Particle Galaxy
   - Spinning Product Display
   - Wave Animation Background
   - 3D Text Hero
3. Template preview system
4. Template selection flow
5. Store templates in Convex

**Deliverables:**
- 5 working templates with Three.js animations
- Visual template gallery
- One-click template instantiation

### Phase 4: Visual Builder - Core (Week 5-6)
**Goal:** Simple block-based editor

**Tasks:**
1. Builder layout (3-panel)
   - Section list (left)
   - Live preview (center)
   - Properties panel (right)
2. Block library system
   - Hero blocks
   - Content blocks
   - CTA blocks
3. Property editor
   - Text editing
   - Color picker
   - Image upload
4. Simple animations picker
5. Real-time preview updates

**Deliverables:**
- Working visual editor
- Users can edit text/colors
- Users can add/remove sections
- Live preview of changes

### Phase 5: Three.js Integration (Week 7)
**Goal:** Image-to-3D magic feature

**Tasks:**
1. Image upload system
2. Background removal integration (remove.bg API)
3. Depth map generation (AI)
4. Layered 3D effect renderer
5. Animation presets for 3D elements
6. Performance optimization

**Deliverables:**
- Users upload regular photos
- Photos converted to 3D-like effects
- 6 animation presets working
- Mobile-optimized performance

### Phase 6: Real-Time Collaboration (Week 8)
**Goal:** Multiple users editing simultaneously

**Tasks:**
1. Convex subscriptions for real-time sync
2. User presence system
   - Show active users
   - Cursor tracking
3. Conflict resolution
   - Layer locking
   - Last-write-wins
4. Version history
5. Collaboration UI indicators

**Deliverables:**
- Multiple users can edit same project
- See each other's cursors
- Changes sync in real-time
- No data loss on conflicts

### Phase 7: Publishing System (Week 9)
**Goal:** One-click publish to live URL

**Tasks:**
1. Export/optimization pipeline
   - Compress 3D assets
   - Minify code
   - Generate static HTML
2. Subdomain hosting (projectname.samra.app)
3. Custom domain support
4. SEO meta tags generation
5. Analytics injection

**Deliverables:**
- One-click publish button
- Live pages at custom URLs
- SEO-optimized output
- Basic analytics tracking

### Phase 8: Polish & Launch (Week 10)
**Goal:** Production-ready MVP

**Tasks:**
1. Onboarding flow
2. Error handling
3. Loading states
4. Documentation
5. Stripe integration (payments)
6. Performance optimization
7. Bug fixes
8. Launch prep

**Deliverables:**
- Stable, production-ready app
- Payment system working
- Full documentation
- Ready for beta users

## Critical Requirements

### For Non-Technical Users
- ❌ NO technical jargon (no "metalness", "roughness", "position XYZ")
- ✅ Visual presets (click to apply)
- ✅ Template-first approach (never blank canvas)
- ✅ Simple language ("Change background color" not "Configure scene background")
- ✅ Drag-and-drop where possible
- ✅ Instant preview of changes

### Performance
- Mobile-first (60% of users will be on mobile)
- Lighthouse score > 70
- Initial load < 3 seconds
- 3D assets < 5MB per project
- Lazy loading for everything

### Security
- Input sanitization (prevent XSS)
- File upload validation
- CSRF protection
- Rate limiting
- User data isolation (multi-tenant)

### Documentation
**CRITICAL:** Document everything as you build!

For each component/feature, create:
1. **Purpose**: What does it do?
2. **Props/API**: Input/output interfaces
3. **Usage Example**: Code snippet
4. **Edge Cases**: Known limitations
5. **Performance Notes**: Optimization tips

Save documentation in:
- Component files (JSDoc comments)
- `/docs` folder (markdown files)
- README.md (high-level overview)

## Code Standards

### TypeScript
- Strict mode enabled
- Explicit return types for functions
- No `any` types (use `unknown` if needed)
- Zod schemas for validation

### React
- Functional components only
- Custom hooks for logic
- Proper dependency arrays
- Memoization where beneficial

### Styling
- Tailwind CSS utility classes
- No inline styles
- Responsive design (mobile-first)
- Dark mode support

### File Naming
- Components: PascalCase (e.g., `Canvas3D.tsx`)
- Utilities: camelCase (e.g., `imageLoader.ts`)
- Types: PascalCase (e.g., `ProjectSchema.ts`)

### Git Commits
- Conventional commits format
- Examples:
  - `feat: add template gallery`
  - `fix: resolve mobile canvas rendering`
  - `docs: update API documentation`
  - `perf: optimize 3D model loading`

## Building and Running

### Prerequisites
- Bun (recommended) or Node.js with npm

### Installation
```bash
bun install
```

### Development
```bash
# Start development server on port 3000
bun --bun run dev
# or
bun --bun run start
```

### Production Build
```bash
# Build for production
bun --bun run build

# Preview production build locally
bun --bun run serve
```

### Testing
```bash
# Run tests once
bun --bun run test

# Run tests in watch mode
bun --bun run test --watch
```

### Code Quality
```bash
# Lint code
bun --bun run lint

# Format code
bun --bun run format

# Run comprehensive code check
bun --bun run check
```

## Development Conventions

### Routing
- Routes are file-based and located in `app/routes/`
- Root route is in `app/routes/__root.tsx` and serves as the layout component
- Index route is in `app/routes/index.tsx`
- Additional routes automatically create navigation endpoints
- Use the `Link` component from `@tanstack/react-router` for SPA navigation

### Styling
- Tailwind CSS is used for styling with the new v4 engine
- Global styles are defined in `app/styles/globals.css`
- Utility classes are preferred over custom CSS

### Data Fetching
- Convex is used for real-time database operations
- TanStack Router includes built-in `loader` functionality for data loading
- Server functions are available for server-side operations

### Authentication
- Clerk is used for user authentication
- Better Auth for multi-tenancy (organizations, teams, roles)

### Code Quality
- Biome is configured for linting, formatting, and code analysis
- All code should pass linting and formatting checks
- Type safety is enforced with strict TypeScript settings
- Import aliasing with `@/*` pointing to `./src/*`

## Important Files

- `app/routes/__root.tsx`: Root layout component that appears across all routes
- `app/routes/index.tsx`: Landing page component with 3D hero section
- `app/router.tsx`: Router configuration
- `convex/schema.ts`: Database schema definition
- `convex/users.ts`: User operations in Convex
- `vite.config.ts`: Vite build configuration with TanStack Start integration
- `biome.json`: Code quality configuration

## Current Status

**Setup Completed:**
- ✅ Bun installed
- ✅ TanStack Start initialized
- ✅ Biome configured (linting)
- ✅ Tailwind CSS setup
- ✅ Convex initialized
- ✅ Project structure created
- ✅ Dev server running

**Next Task:**
Phase 1 - Building the marketing landing page with 3D hero section

## Deployment

The application is built with TanStack Start and can be deployed to Vercel using the Nitro adapter. For full SSR support, serverless functions are used.