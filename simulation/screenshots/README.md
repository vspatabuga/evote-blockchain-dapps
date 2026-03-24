# Simulation Screenshots

This directory contains auto-generated screenshots for the Kalpataru simulation.

## Screenshot Naming Convention

```
{project}-{page}-{description}.png

Examples:
├── kalpataru-01-login.png        - Login/landing page
├── kalpataru-02-dashboard.png    - Main dashboard
├── kalpataru-03-waste-catalog.png - Waste catalog view
├── kalpataru-04-transactions.png  - Transaction history
└── kalpataru-05-admin.png        - Admin panel
```

## Generation

Screenshots are generated automatically via GitHub Actions on every push to `main`.

See `.github/workflows/screenshot.yml` for the generation pipeline.

## Manual Generation

```bash
# Start the simulation
npm run simulate

# Generate screenshots (requires Playwright)
npx playwright screenshot http://localhost:3001 ./simulation/screenshots/
```

## Requirements

- Docker and Docker Compose running
- Playwright installed (`npx playwright install chromium`)
