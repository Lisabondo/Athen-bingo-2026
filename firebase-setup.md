# Firebase opsætning — delt Athen Bingo

Samme fremgangsmåde som til dansk-tysk-quiz. Det er en **engangssætning** på ca. 10 minutter. Når det er gjort, synkroniserer alle tre billetter automatisk i realtid — så I kan se hinandens fremskridt live, selv på hver jeres telefon.

---

## Trin 1 — Opret Firebase-projekt

1. Gå til [console.firebase.google.com](https://console.firebase.google.com)
2. Log ind med din Google-konto
3. Klik **"Add project"** (eller **"Tilføj projekt"**)
4. Giv det et navn, f.eks. `athen-bingo`
5. Slå Google Analytics **fra** (ikke nødvendigt) → klik **"Create project"**
6. Vent til projektet er oprettet → klik **"Continue"**

---

## Trin 2 — Aktivér Realtime Database

1. I venstre menu: klik **"Build"** → **"Realtime Database"**
2. Klik **"Create Database"**
3. Vælg region: **"Europe (belgium)"** (nærmest Danmark/Grækenland)
4. Vælg **"Start in test mode"** → klik **"Enable"**

---

## Trin 3 — Hent din config

1. Klik på **tandhjulet** ⚙️ øverst til venstre → **"Project settings"**
2. Scroll ned til **"Your apps"**
3. Klik på **web-ikonet** `</>`
4. Giv appen et navn (f.eks. `bingo`) → klik **"Register app"**
5. Du ser nu en kodeblok der ligner dette:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "athen-bingo.firebaseapp.com",
  databaseURL: "https://athen-bingo-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "athen-bingo",
  storageBucket: "athen-bingo.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

Kopier denne blok (alle 7 linjer inde i `{}`).

---

## Trin 4 — Indsæt config i index.html

1. Åbn `index.html` i en teksteditor (f.eks. TextEdit, VS Code)
2. Find `FIREBASE_CONFIG` nær bunden af filen (i `<script>`-sektionen):

```javascript
const FIREBASE_CONFIG={
  apiKey:"PASTE_YOUR_API_KEY",
  authDomain:"PASTE_YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL:"https://PASTE_YOUR_PROJECT_ID-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:"PASTE_YOUR_PROJECT_ID",
  storageBucket:"PASTE_YOUR_PROJECT_ID.appspot.com",
  messagingSenderId:"PASTE_YOUR_SENDER_ID",
  appId:"PASTE_YOUR_APP_ID"
};
```

3. Erstat de 7 værdier med dine egne fra trin 3
4. Gem filen

Uden dette trin virker siden stadig — men kun lokalt på hver telefon ("🟡 Lokal" i toppen). Med config sat op bliver badgen "🟢 Synk", og alle tre billetter deler data.

---

## Trin 5 — Upload til GitHub Pages

1. Commit og push `index.html` til repoet
2. GitHub Pages opdaterer automatisk inden for ~1 minut

---

## Trin 6 — Første gang på hver telefon

1. Åbn siden på alle tre telefoner
2. Vælg sit eget navn (Lisa / Emilie / Fie) på "Hvem er du?"-skærmen
3. Valget gemmes automatisk til næste gang

✅ Nu synkroniserer alle tre billetter i realtid — når én stempler et felt, ser de andre to det med det samme i deres liste.

---

## Sikkerhed

Firebase er sat op i "test mode" — det betyder at alle, der kender jeres database-URL, kan læse/skrive data. Det er fint til en lille ferie-leg mellem jer tre. Vil du låse det mere ned, kan du opdatere "Rules" i Realtime Database til:

```json
{
  "rules": {
    "athenBingo": {
      ".read": true,
      ".write": true
    }
  }
}
```

---

## Pris

Firebase Realtime Database er **gratis** op til 1 GB lagring og 10 GB/måned datatrafik. Et bingospil mellem tre bruger < 1 MB total. I kommer aldrig i nærheden af grænsen.
