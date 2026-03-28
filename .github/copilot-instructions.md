# Copilot Instructions — Mona Mayhem

## Project Overview

**Mona Mayhem** is a VS Code & GitHub Copilot workshop project — a retro arcade-themed Astro website that compares GitHub contribution graphs of two users. The project is intentionally scaffolded for learning, with most functionality unimplemented via TODOs for workshop participants to build using Copilot.

**Important:** This is a workshop *starter template*, not a production app. Code should prioritize clarity and educational value over optimization.

## Technology Stack

- **Framework**: Astro v5.14.4 with SSR enabled (`@astrojs/node` adapter in standalone mode)
- **Language**: TypeScript (strict mode)
- **Styling**: CSS (no UI frameworks; retro/arcade theme via Press Start 2P font)
- **Runtime**: Node.js (required for server-side rendering)
- **API**: GitHub's contribution graph API (via `https://github.com/{username}.contribs`)

## Build Commands

```bash
npm run dev       # Start dev server (default: http://localhost:3000)
npm run build     # Build for production
npm run preview   # Preview production build locally
npm astro         # Run Astro CLI directly
```

## Project Structure

```
src/
├── pages/
│   ├── index.astro                    # Landing page
│   └── api/
│       └── contributions/
│           └── [username].ts          # GitHub contribution fetcher (dynamic route)
astro.config.mjs                        # Astro config with Node.js adapter
tsconfig.json                           # TypeScript strict config
workshop/                               # 7-part markdown learning guides (00-06)
docs/                                   # Documentation assets (static HTML/CSS)
```

## Key Files & Patterns

### Pages (File-based Routing)

- **Location**: `src/pages/` — each `.astro` file auto-creates a route
- **Current**: `index.astro` (home page)
- **Create new pages**: Add `.astro` files to `src/pages/`; nested folders create nested routes

### API Routes (Dynamic Routes)

- **Location**: `src/pages/api/` — TypeScript/JavaScript files that handle HTTP requests
- **Naming**: `[username].ts` creates a dynamic route matching `/api/contributions/{username}`
- **Pattern**: Export default async function with `(context)` parameter containing `params`, `request`, `url`
- **Return**: `Response` object with status code and body
- **Current**: `/api/contributions/[username].ts` is unimplemented (returns 501)

### Styling

- **Approach**: Scoped stylesheet per component (standard Astro pattern using `<style>` in `.astro` files)
- **Global theme**: `Press Start 2P` font (retro arcade aesthetic)
- **Theme toggle**: See `docs/theme-toggle.js` for light/dark mode example

### TypeScript

- **Config**: `tsconfig.json` extends Astro's strict preset
- **API endpoints**: Must be TypeScript files (`.ts`) for type safety
- **Components**: `.astro` files support TypeScript in the frontmatter

## Common Development Tasks

### Create a New Page

1. Create file: `src/pages/[name].astro`
2. Add Astro component with HTML + optional `<style>` block
3. Access via route: `/[name]`

### Create an API Endpoint

1. Create file: `src/pages/api/[endpoint].ts`
2. Export default async function:
   ```typescript
   export default async (context) => {
     const { params } = context;
     // Logic here
     return new Response(JSON.stringify(data), { status: 200 });
   };
   ```
3. Access via: `/api/[endpoint]`

### Fetch GitHub Contribution Data

- **Endpoint**: `/api/contributions/{username}`
- **Data source**: `https://github.com/{username}.contribs` (HTML table format)
- **Current status**: Returns 501 Not Implemented — workshop participants build this
- **Expected output**: Parse HTML table into JSON contribution data

### Add Styling

- **Scoped (component-level)**: Add `<style>` block in `.astro` file
- **Global (site-wide)**: Import CSS file in `src/pages/index.astro` using Astro's CSS imports
- **Theme colors**: Reference arcade/retro palette (define CSS variables for reusability)

## Workshop Structure

The [workshop/](workshop/) directory contains 7 sequential markdown guides for learners:

| Part | Focus |
|------|-------|
| [00-overview.md](workshop/00-overview.md) | Track selection and learning objectives |
| [01-setup.md](workshop/01-setup.md) | Workspace instructions and context engineering |
| [02-plan-and-scaffold.md](workshop/02-plan-and-scaffold.md) | API and page architecture planning |
| [03-agent-mode.md](workshop/03-agent-mode.md) | Building the game with Copilot in agent mode |
| [04-design-vibes.md](workshop/04-design-vibes.md) | Visual design and theming |
| [05-polish.md](workshop/05-polish.md) | Parallelism, reviews, and quality passes |
| [06-bonus.md](workshop/06-bonus.md) | Open-ended extensions and experiments |

**When implementing features**: Reference the relevant workshop section to understand the learning context and track (VS Code vs CLI).

## Development Conventions

### TypeScript & Type Safety

- Always use TypeScript (`.ts` for API routes, TypeScript in Astro frontmatter)
- Do not use `any` types — prefer specific types or generics
- API response types should be clearly defined

### Error Handling

- API endpoints should return appropriate HTTP status codes (200, 400, 404, 500, etc.)
- Use `Response` objects with meaningful error messages
- Document expected response formats in comments

### Code Comments

- Add comments explaining business logic (e.g., why fetching from a specific URL)
- Mark incomplete features with `TODO:` comments for workshop participants
- Reference workshop sections when TODOs relate to learning goals

### Testing & Linting

- No test framework currently configured (participants may add in bonus section)
- No linter/formatter configured (maintain readable code)
- Before major changes, consider if tests or linting would be beneficial

## Common Pitfalls

- **Astro routes are file-based**: File path = route structure; moving/renaming files changes routes
- **SSR required**: This project uses Node.js adapter; some browser-only APIs need `client:only` directive
- **GitHub API rate limits**: Bare requests to GitHub may hit rate limits; consider caching in production
- **TypeScript strict mode**: All code must pass strict type checking (no `any`, proper return types)

## Helpful Links

- [Astro Documentation](https://astro.build/docs/)
- [Astro Routing Guide](https://docs.astro.build/en/basics/routing/)
- [GitHub Personal Contributions API](https://docs.github.com/en/rest/users/users?apiVersion=2022-11-28)
- [Workshop Overview](workshop/00-overview.md)
