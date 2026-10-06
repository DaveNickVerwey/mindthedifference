# Google Sheets aanmeldingen — setup

## Stap 1: Maak een Google Sheet

1. Ga naar [sheets.new](https://sheets.new)
2. Noem 'm bijvoorbeeld "Mind The Difference aanmeldingen"
3. Zet in **rij 1** deze kolomkoppen:
   ```
   Tijdstip | Voornaam | Achternaam | Leeftijd | E-mail | Studie/functie | Challenge | Taal
   ```

## Stap 2: Apps Script koppelen

1. In het sheet: menu **Extensies → Apps Script**
2. Verwijder alle bestaande code
3. Plak dit erin:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data = JSON.parse(e.postData.contents);

  sheet.appendRow([
    new Date(data.tijdstip),
    data.voornaam,
    data.achternaam,
    data.leeftijd,
    data.email,
    data.studie,
    data.challenge,
    data.taal
  ]);

  return ContentService
    .createTextOutput(JSON.stringify({ ok: true }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Klik op het **schijfje** om op te slaan (naam mag "Aanmeldingen webhook" zijn)

## Stap 3: Deploy als webhook

1. Rechtsboven **Implementeren → Nieuwe implementatie**
2. Bij "Type kiezen" (het tandwieltje) → **Web-app**
3. Vul in:
   - Beschrijving: `MTD aanmeld webhook`
   - Uitvoeren als: **ik**
   - Wie heeft toegang: **iedereen**
4. Klik **Implementeren**
5. Bij de eerste keer moet je toestemming geven — klik door de waarschuwing (Google waarschuwt bij zelfgemaakte scripts, dat is normaal)
6. **Kopieer de web-app URL** die je krijgt (ziet eruit als `https://script.google.com/macros/s/AKfy.../exec`)

## Stap 4: URL in de site zetten

Open `index.html` en zoek deze regel:

```javascript
const WEBHOOK_URL = 'JOUW_APPS_SCRIPT_URL_HIER';
```

Vervang `JOUW_APPS_SCRIPT_URL_HIER` door de URL die je hebt gekopieerd.

## Stap 5: Testen

Deploy de site en vul een keer het formulier in. Kijk in het sheet of de rij verschijnt.

## Aanmeldingen bijhouden

Rijen komen automatisch onderaan het sheet. Je kunt:
- Een filter op de kolom "Challenge" zetten om te zien wie meedoet aan de challenge
- E-mailmeldingen instellen: **Extra → Meldingsregels** → melding bij elke wijziging

## Als je updates doet aan de site en het formulier

Werkt gewoon door, geen nieuwe deploy van de Apps Script nodig.

## Als je updates doet aan het Apps Script

**Elke keer** wanneer je het script wijzigt, moet je opnieuw deployen:
- **Implementeren → Implementaties beheren** → potlood-icoon → **Nieuwe versie** → **Implementeren**
- De URL blijft hetzelfde.
