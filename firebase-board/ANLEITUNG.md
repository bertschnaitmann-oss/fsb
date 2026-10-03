# Team-Board auf Firebase veröffentlichen

Ergebnis: Eine Adresse wie `https://euer-board.web.app`. Dein Team öffnet sie ohne Konto und kann lesen und schreiben. Zugang nur mit Team-Code.

## 1. Projekt anlegen (im Browser, ca. 5 Min.)

1. https://console.firebase.google.com öffnen, mit deinem Google-Konto anmelden.
2. **Projekt hinzufügen**, Namen vergeben (z. B. `euer-board`). Google Analytics kannst du ausschalten.
3. Links **Build → Firestore Database → Datenbank erstellen**.
   - Standort: `europe-west6` (Zürich) oder `eur3` (Europa).
   - Modus: **Produktionsmodus** (die richtigen Regeln laden wir in Schritt 4 hoch).
4. Oben links beim Zahnrad **Projekteinstellungen → Allgemein → Meine Apps → Web-Symbol (`</>`)**.
   - Namen eingeben, **Hosting NICHT** ankreuzen, **App registrieren**.
   - Es erscheint ein Block `firebaseConfig = { apiKey: ..., ... }`. Diesen brauchst du gleich.

## 2. Zugangswerte eintragen

Öffne `public/index.html` in einem Texteditor. Suche `firebaseConfig` und ersetze jedes `HIER_EINFUEGEN` durch den passenden Wert aus Schritt 1.4. Die Werte sind keine Passwörter. Der Schutz kommt von den Regeln und dem Team-Code.

## 3. Werkzeug installieren (einmalig, am Computer)

1. Node.js installieren: https://nodejs.org (LTS-Version).
2. Terminal (Mac) bzw. Eingabeaufforderung (Windows) öffnen:

```
npm install -g firebase-tools
firebase login
```

## 4. Hochladen

Im Terminal in den Ordner `firebase-board` wechseln (z. B. `cd Pfad/zu/firebase-board`), dann:

```
firebase deploy --only hosting,firestore --project DEINE-PROJEKT-ID
```

Die Projekt-ID steht in den Projekteinstellungen (z. B. `euer-board`). Am Ende zeigt der Befehl die **Hosting URL** an.

## 5. Team einladen

- Denke dir einen Team-Code aus, mindestens 8 Zeichen, nicht erratbar (z. B. `blauer-Tisch-2026`).
- Schicke dem Team den Link mit Code, dann müssen sie nichts eintippen:
  `https://euer-board.web.app/?code=blauer-Tisch-2026`
- Der Code wird auf dem Handy gespeichert. Danach reicht der normale Link.
- Tipp auf dem Handy: Seite über das Teilen-Menü zum Home-Bildschirm hinzufügen.

## Wichtig

- Der Team-Code ist die Zugangssperre. Wer ihn kennt, sieht und ändert alles. Gib ihn nur im Team weiter. Für vertrauliche Inhalte ist das nicht stark genug.
- Neuer Code = neues, leeres Board. Die alten Einträge bleiben unter dem alten Code erhalten.
- Kosten: Der kostenlose Tarif (Spark) reicht für ein kleines Team. Prüfe die aktuellen Limits auf der Firebase-Preisseite.
- Seite später ändern: Datei anpassen und den Befehl aus Schritt 4 erneut ausführen.
