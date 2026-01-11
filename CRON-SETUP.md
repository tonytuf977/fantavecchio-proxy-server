# Setup Cron Job su Render.com

## Endpoint creato
✅ `/api/check-finestra-scambi` - Controlla e gestisce apertura/chiusura automatica finestra scambi

## Come configurare il Cron Job su Render

### Opzione 1: Cron Job nativo di Render (CONSIGLIATO)

1. **Vai su Render Dashboard**: https://dashboard.render.com
2. **Click su "New +"** → **"Cron Job"**
3. **Connetti il repository** `fantavecchio-proxy-server`
4. **Configura**:
   - **Name**: `fantavecchio-scambi-checker`
   - **Region**: Frankfurt (più vicino all'Italia)
   - **Branch**: `main`
   - **Command**: 
     ```bash
     curl https://fantavecchio-proxy-server.onrender.com/api/check-finestra-scambi
     ```
   - **Schedule**: Ogni 5 minuti
     ```
     */5 * * * *
     ```
     Oppure ogni 10 minuti (consigliato per piano free):
     ```
     */10 * * * *
     ```

5. **Click su "Create Cron Job"**

### Opzione 2: Servizio esterno (cron-job.org)

Se preferisci un servizio esterno gratuito:

1. Vai su: https://cron-job.org/en/
2. Registrati gratuitamente
3. **Click su "Create Cronjob"**
4. **Configura**:
   - **Title**: Controllo Finestra Scambi FantaVecchio
   - **URL**: `https://fantavecchio-proxy-server.onrender.com/api/check-finestra-scambi`
   - **Schedule**: Ogni 10 minuti
   - **Method**: GET
   - **Request timeout**: 30 seconds

5. **Salva**

## Cosa fa il Cron Job?

Ogni 5-10 minuti il server controlla automaticamente:

1. ✅ Legge le impostazioni da Firebase (`dataApertura`, `oraApertura`, `dataChiusura`, `oraChiusura`)
2. ✅ Confronta con l'ora attuale
3. ✅ Se è ora di aprire → Apre finestra e invia email a tutti
4. ✅ Se è ora di chiudere → Chiude finestra e invia email a tutti
5. ✅ Evita email duplicate (non invia se già inviata negli ultimi 10 minuti)

## Vantaggi

- ⚡ **Automatico**: Non serve che qualcuno apra l'app
- 🎯 **Preciso**: Controlla ogni 5-10 minuti
- 💰 **Gratuito**: Cron Job free su Render
- 📧 **Affidabile**: Email inviate solo quando necessario
- 🚫 **Anti-duplicati**: Logica di prevenzione email duplicate

## Test manuale

Puoi testare manualmente l'endpoint con:

```bash
curl https://fantavecchio-proxy-server.onrender.com/api/check-finestra-scambi
```

Oppure visitando nel browser:
https://fantavecchio-proxy-server.onrender.com/api/check-finestra-scambi

## Logs

Per vedere i logs del Cron Job:
1. Vai su Render Dashboard
2. Seleziona il Cron Job
3. Tab "Logs"
4. Vedrai i log di ogni esecuzione con `🔍 [CRON] Controllo finestra scambi...`
