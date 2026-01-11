# Setup Email con Gmail

Per inviare email dal server, devi configurare una **App Password** di Gmail.

## Passaggi:

### 1. Attiva la verifica in 2 passaggi su Gmail
- Vai su: https://myaccount.google.com/security
- Cerca "Verifica in due passaggi"
- Se non è attiva, attivala

### 2. Crea una App Password
- Vai su: https://myaccount.google.com/apppasswords
- Oppure cerca "Password per le app" nelle impostazioni Google
- Seleziona:
  - App: **Mail**
  - Dispositivo: **Altro (nome personalizzato)** → scrivi "FantaVecchio Server"
- Click **Genera**
- Ti verrà mostrata una password di 16 caratteri tipo: `abcd efgh ijkl mnop`

### 3. Inserisci la password in index.mjs

Apri `index.mjs` e sostituisci:

```javascript
pass: 'your-app-password-here'
```

Con:

```javascript
pass: 'abcdefghijklmnop'  // ⬅️ La tua App Password (senza spazi)
```

⚠️ **IMPORTANTE**: Rimuovi gli spazi dalla password!

### 4. Redeploy su Render

Dopo aver salvato:
1. Commit e push su GitHub
2. Redeploy su Render

## Alternative a Gmail

Se preferisci non usare Gmail, puoi configurare:

- **SendGrid**: 100 email/giorno gratis
- **Mailgun**: 5000 email/mese gratis primi 3 mesi
- **Brevo (ex Sendinblue)**: 300 email/giorno gratis

Per usare SendGrid o altri, modifica la configurazione di `transporter` in index.mjs.
