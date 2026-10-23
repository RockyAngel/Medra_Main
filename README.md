# Medra

Multi-role healthcare and delivery marketplace **frontend prototype**. This repository continues the supplied React source, fixes a staff sign-in crash, and preserves the original source and downloadable HTML under `archive/`.

## Open it immediately

No package installation is needed to open `previews/index.html` in your browser. It contains the combined preview with all seven apps. Alternatively, with Node.js installed:

```sh
npm start
```

Open **http://localhost:5173**. `npm start` serves the included, corrected snapshots; editing JSX does not update those snapshots.

## Develop in VS Code

Install Node.js 24 LTS, open this folder in VS Code, and run in its terminal:

```sh
npm ci
npm run dev
```

Open **http://localhost:5173**. Edit `src/apps/*.jsx`, save, then reload the browser. This uses esbuild's watch mode; React Fast Refresh is not configured. The development server listens on localhost. In Codespaces, forward port 5173 from the Ports panel.

| Experience | Editable source | Preview route |
| --- | --- | --- |
| All apps together | `src/apps/medra-combined.jsx` | `/` or `/combined.html` |
| Customer | `src/apps/medra.jsx` | `/customer.html` |
| Seller | `src/apps/medra-seller.jsx` | `/seller.html` |
| Rider | `src/apps/medra-rider.jsx` | `/rider.html` |
| Admin | `src/apps/medra-admin.jsx` | `/admin.html` |
| Support | `src/apps/medra-support.jsx` | `/support.html` |
| Super Admin | `src/apps/medra-superadmin.jsx` | `/super-admin.html` |
| Landing | `src/apps/medra-landing.jsx` | `/landing.html` |

Use the prefilled demo sign-in values. Staff sign-in has a second, simulated code step prefilled with `123456`. These forms do not authenticate against a server.

## Build and verify

```sh
npm run build
npx playwright install chromium
npm test
npm run preview
```

The build regenerates eight self-contained HTML files in `dist/`, plus `index.html` as a copy of the combined preview. Preview it at **http://localhost:4173**. Bundled scripts work from `file://`; remote fonts/images can still require internet. `dist/` is generated and ignored by Git. Run `npm run snapshots` to rebuild and update the checked-in `previews/` files too. `archive/` remains the original recovery baseline.

The browser smoke test checks all eight source-built entry points, demo sign-in, authenticated dashboard rendering, combined-shell role switching, and basic mobile rendering. It is not a full feature or security audit.

## What works today, and what does not

- React interfaces for all seven experiences, with Lucide icons and Recharts dashboards.
- Mock data and in-memory interactions. Reloading resets state.
- The combined shell shares demo sign-in and orders in the same browser session. Other app-specific state can reset when switching roles. Standalone files do not share sessions or orders.
- No Supabase client, backend API, persistent authentication, real 2FA, production payment processing, or durable data storage is included.
- Admin and Support have separate interfaces. Separate HTML files do **not** enforce backend permissions. See `docs/permission-matrix.md` for the intended permission design.
- Metrics, forecasts, medical providers, emergency directory entries, and staff identities are prototype content; their presence does not establish a live service or verified credentials.

No backend keys are required to run this version. The historical notes under `docs/legacy/` describe several different builds, including an older Supabase implementation and a separate Nexo telehealth project. They are context, not evidence of this version's capabilities. See `docs/CURRENT-STATE.md`.

## Put this on GitHub

See [GITHUB-SETUP.md](GITHUB-SETUP.md) for a browser upload or VS Code instructions. Keep the repository private while reviewing the inherited demo content. Do not commit credentials, `.env`, real patient data, or `node_modules/`.

No application license is assigned by this import; the project owner can choose one. Bundled third-party license notices remain in the supplied HTML and generated builds.
