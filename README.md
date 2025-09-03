
# Emergence Movie Exhibit

This is the official web exhibit for the documentary film **Emergence: South Asian Canadian Stories**. The project showcases the film, its cast, awards, and related content, built with SvelteKit and Tailwind CSS.

## About the Project

**Emergence** is a documentary exploring the stories of South Asian Canadians, their cultural heritage, and contributions. This web exhibit provides:

- Film details and synopsis
- Cast and crew profiles
- Awards and recognitions
- Trailer and media assets
- Interactive navigation and accessible design

## Tech Stack

- SvelteKit (Svelte 5 runes syntax)
- Tailwind CSS (v4, with design tokens)
- TypeScript
- Custom SVG icons (no external icon libraries)
- Figma design tokens integration

## Getting Started

Install dependencies (use `pnpm`):

```bash
pnpm install
```

Start the development server:

```bash
pnpm run dev
```

Build for production:

```bash
pnpm run build
```

Preview production build:

```bash
pnpm run preview
```

> **Note:** Always use `pnpm` for package management.

## Project Structure

- `src/routes/` — SvelteKit file-based routing (pages: awards, cast, etc.)
- `src/lib/components/` — Custom and UI components
- `src/lib/assets/` — Images, video, and media
- `src/content/films/emergence.json` — Film metadata
- `static/` — Public assets (hero poster, etc.)

## Contributing

Please follow code style and architecture guidelines in `.github/copilot-instructions.md` and `src/app.css` for theming. Use Svelte 5 runes syntax and Tailwind CSS utilities. All icons must be inline SVG from Figma assets.

## License

See LICENSE file for details.

...existing code...
