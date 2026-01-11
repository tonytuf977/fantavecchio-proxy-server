# Fantavecchio Proxy Server

Server Express per gestire l'import automatico dei dati da Fantacalcio.it

## Deploy su Render.com

1. Connetti questo repository su Render.com
2. Seleziona "Web Service"
3. Configura:
   - Build Command: `npm install`
   - Start Command: `node index.mjs`
   - Porta: 3001

## Variabili d'ambiente

Non richieste (i cookie sono hardcodati nel server)

## Endpoints

- `GET /api/giocatori` - Scarica Excel da Fantacalcio.it
