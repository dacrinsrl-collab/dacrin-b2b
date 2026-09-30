# Dacrin B2B

Aplicație internă pentru documentarea lucrărilor de fibră optică.

## Funcționalități

- Management proiecte și conturi cu autentificare username/parolă.
- Documentație client, trasee FO, suduri FO și operațiuni site.
- Hărți OpenStreetMap cu registrul Optix.
- Fotografii, rapoarte și sincronizare Google Drive.
- Acces separat pentru administratori, coordonatori și tehnicieni.

## Publicare în Cloudflare

1. Creează baza D1 `dacrin-b2b-db`.
2. Creează bucket-ul R2 `dacrin-b2b-files`.
3. Înlocuiește `YOUR_D1_DATABASE_ID` din `wrangler.jsonc` cu identificatorul bazei.
4. Configurează secretele `DACRIN_ADMIN_PASSWORD`, `DACRIN_TECHNICIAN_PASSWORD` și `DACRIN_DRIVE_ENCRYPTION_KEY` exclusiv în Cloudflare.
5. Conectează repository-ul prin Cloudflare Workers & Pages → Create application → Import a repository.
6. Comanda de build: `npm run build`.
7. Comanda de deploy: `npx wrangler d1 migrations apply dacrin-b2b-db --remote && npx wrangler deploy --config wrangler.jsonc`.
8. Adaugă noul URL în Google Cloud OAuth și reconectează Google Drive.

Nu adăuga parole, tokenuri, fotografii ale clienților sau exporturi ale bazei de date în repository.

## Configurarea clonei Dacrin

- Configurează o bază D1 și un bucket R2 dedicate acestei aplicații. ID-ul bazei trebuie completat în `wrangler.jsonc`.
- Domeniile Dacrin din `CNAME`, `wrangler.jsonc`, `app/layout.tsx` și documentația OAuth sunt valori propuse; înlocuiește-le cu domeniul real înainte de publicare.
- Configurează secretele `DACRIN_ADMIN_PASSWORD`, `DACRIN_TECHNICIAN_PASSWORD`, `DACRIN_DRIVE_ENCRYPTION_KEY` și variabila `DACRIN_APP_URL`, plus setările Microsoft descrise în `docs/ONEDRIVE_SETUP.md`.
- Reconectează Google Drive și OneDrive pentru noua aplicație.
- Pentru Android TWA, configurează numele pachetului și amprenta certificatului propriu în `public/.well-known/assetlinks.json`.
- Pe Windows poți rula direct `npx vite` pentru dezvoltare și `npx vinext build` pentru build; scripturile npm originale necesită Bash.
