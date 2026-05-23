# The Alchemy Lab Testing

## Commands

Run from:

```powershell
cd C:\Users\yrred\Desktop\Unity\TWB-Alchemy
```

Current commands:

- Install dependencies: `npm install`
- Dev server: `npm run dev`
- Build: `npm run build`
- Preview: `npm run preview`

Current local smoke URL:

```text
http://127.0.0.1:5174/
```

## Reported Checks

- `npm.cmd run build`
- Browser smoke checks at `http://127.0.0.1:5174/`
- Browser cave view checks for console errors after movement/pathing changes
- Manual visual checks from screenshots/user feedback for cave wall traversal, pet release timing, and movement smoothness

## QA Cautions

- Clear or control browser localStorage when testing timing, sleep states, inventory counts, and cave run positions.
- Expect Vite chunk-size warnings from Phaser for now.
- Do not rely on generated `dist\` filenames as stable evidence.

## Sources

- [[short-term/2026-05-12-twb-alchemy-working-window-intake]]
