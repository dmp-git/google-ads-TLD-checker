# 🌐 Google Ads Script — TLD Placement Exclusion (Display)

Questo script Google Ads automatizza l’esclusione di domini di basso valore (ad esempio `.xyz`, `.buzz`, `.ru`, ecc.) dalle campagne Display sulla base dell’estensione (TLD). È utile per proteggere i budget pubblicitari da siti spam, bot o traffico poco qualificato.

---

## ✨ Funzionalità principali

- ❌ **Esclude automaticamente domini** che corrispondono a specifici TLD sospetti.
- 🔎 **Filtra solo i placement con almeno 1 clic** negli ultimi 30 giorni.
- 📂 **Utilizza o crea una lista condivisa di esclusione placement** nel tuo account Google Ads.
- ♻️ **Evita duplicati** controllando se il dominio è già stato escluso.
- ⏱️ **Batch e throttling** gestiti per evitare superamento delle quote.

---

## ⚙️ Configurazione

Modifica i seguenti parametri nella sezione `currentSetting` dello script:

```javascript
stringsToExclude: [
  ".one", ".buzz", ".xyz", ".ee", ".cloud", ".ru", ".ro",
  ".space", ".in", ".news", ".today", ".fun", ".mr",
  ".me", ".gratis", ".link", ".es", ".al", ".ua", ".id", ".app",
  ".top", ".group", ".jp", ".click", ".shop", ".pl", ".su",
  ".art", ".gr", ".am", ".camera", ".recipes"
],
dateRange: "LAST_30_DAYS",
batchSize: 10000,
yieldTime: 1000
```

---

## 🧠 Logica di funzionamento

1. Esegue un **report sui placement automatici** negli ultimi 30 giorni.
2. Se il nome del dominio del placement contiene uno dei TLD specificati, viene marcato.
3. Se il dominio non è già nella lista di esclusione, viene aggiunto.
4. Evita l'esclusione di domini YouTube (`youtube.com`).

---

## 🧾 Lista esclusioni

Il nome della lista di esclusione è definito in:

```javascript
var EXCLUSION_LIST_NAME = 'esclusione placement';
```

Se non esiste, lo script la crea automaticamente.

---

## 🛠️ Come usarlo

1. Apri l’account Google Ads e vai su **Strumenti > Script**.
2. Crea un nuovo script e incolla il codice.
3. Salva ed esegui con autorizzazioni appropriate.
4. (Opzionale) Imposta una **schedulazione periodica** per mantenerla aggiornata.

---

## 🔐 Requisiti

- Accesso al tuo account Google Ads.
- Permessi per creare e modificare liste di esclusione placement.
- Il dominio deve essere diverso da `youtube.com`.

---

## 📌 Note aggiuntive

- Lo script utilizza `AUTOMATIC_PLACEMENTS_PERFORMANCE_REPORT`, deprecato in alcuni account. In alternativa, puoi convertirlo a GAQL con `search()`.
- Non si basa sul traffico totale ma solo sui **click ricevuti**, per evitare esclusioni inutili.
- Sospende l'elaborazione temporaneamente ogni 10.000 righe o 50 esclusioni per evitare limiti quota.

---

## 🛠️ Contribuire

Hai idee o miglioramenti? Sentiti libero di inviare una Pull Request o aprire un'Issue!

---

## 📄 Licenza

MIT License. Vedi [LICENSE](./LICENSE) per i dettagli.