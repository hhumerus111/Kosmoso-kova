# Kaip paversti „Kosmoso Kova" į Android programėlę (nemokamai)

Šiame aplanke yra paruoštas žaidimas kaip **PWA (Progressive Web App)** —
tai pirmas žingsnis link Android programėlės. Failai:

- `index.html` — pats žaidimas (su pridėtomis PWA nuorodomis)
- `manifest.json` — programėlės pavadinimas, spalvos, ikonos
- `service-worker.js` — leidžia žaidimui veikti **be interneto** po pirmo atidarymo
- `icons/icon-192.png`, `icons/icon-512.png` — programėlės ikonos

Yra 3 nemokami keliai, priklausomai kiek "tikros" programėlės norite:

---

## 1 BŪDAS — Greičiausias (5 min): "Pridėti į pradžios ekraną"

Šis būdas duoda programėlės ikoną telefono ekrane, kuri atsidaro per visą
ekraną (be naršyklės adreso juostos) ir veikia offline. **Tai jau yra
programėlė vartotojo požiūriu**, tik neinstaliuojama per Play Store.

1. Įkelkite visą šį aplanką į **nemokamą** statinį hostingą:
   - [GitHub Pages](https://pages.github.com) (nemokama, jei turite GitHub paskyrą)
   - arba [Netlify Drop](https://app.netlify.com/drop) — tiesiog nutempiate aplanką į naršyklę, gaunate nuorodą per kelias sekundes
   - arba [Vercel](https://vercel.com)
2. Atsidarykite gautą nuorodą telefono **Chrome** naršyklėje.
3. Meniu (⋮) → **„Pridėti į pradžios ekraną" / „Įdiegti programėlę"**.
4. Ikona atsiranda pradžios ekrane, žaidimas veikia per visą ekraną, net be interneto.

👉 Jūsų atveju, kadangi jau turite savo Ubuntu serverį, galite tiesiog
patalpinti šį aplanką savo serveryje (pvz. per `nginx` ar `python3 -m http.server`)
ir naudoti tą patį adresą namų tinkle arba per VPN.

---

## 2 BŪDAS — Tikras .apk failas be programavimo: PWABuilder

Jei norite tikro `.apk` failo, kurį galima instaliuoti kaip bet kurią kitą
programėlę (arba net publikuoti Google Play):

1. Atlikite **1 būdo** 1–2 žingsnius (žaidimas turi būti pasiekiamas per `https://` nuorodą).
2. Eikite į [pwabuilder.com](https://www.pwabuilder.com) (Microsoft, nemokama).
3. Įveskite savo žaidimo nuorodą, spauskite „Start".
4. Pasirinkite **Android** paketą → atsisiųskite `.apk`/`.aab` failą.
5. Persiųskite `.apk` į telefoną (per USB, el. paštą, Google Drive) ir atidarykite —
   telefonas paprašys leisti „įdiegti iš nežinomų šaltinių" (tai normalu, patvirtinkite).

- Norint publikuoti į **Google Play** parduotuvę, reikia vienkartinio **25 JAV dolerių**
  Google Play Developer mokesčio — tai vienintelė galima išlaida visame procese.
  Instaliuoti tiesiai į savo/šeimos telefoną — **visiškai nemokama**.

---

## 3 BŪDAS — Pilnai autonominė programėlė (be interneto/serverio): Capacitor

Tinkamiausia, jei norite, kad programėlė veiktų **visiškai savarankiškai**,
be jokio serverio, ir norite patobulinti/versijuoti kaip tikrą Android projektą.
Reikės Node.js ir Android Studio (abu nemokami), įdiegti savo Ubuntu kompiuteryje.

```bash
# 1. Įrankiai (jei dar neturite)
sudo apt install nodejs npm   # arba naujausią Node.js versiją per nvm

# 2. Naujas projektas
mkdir kosmoso-kova-app && cd kosmoso-kova-app
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android

# 3. Inicijuoti Capacitor
npx cap init "Kosmoso Kova" "lt.kosmosokova.app" --web-dir=www

# 4. Įdėti žaidimo failus į www/ aplanką
mkdir www
cp /kelias/iki/index.html www/
cp -r /kelias/iki/icons www/
cp /kelias/iki/manifest.json www/

# 5. Pridėti Android platformą
npx cap add android
npx cap sync

# 6. Atidaryti Android Studio (nemokamas, atsisiųskite iš developer.android.com)
npx cap open android
```

Android Studio viduje: **Build → Build Bundle(s)/APK(s) → Build APK(s)**.
Gautas `.apk` failas bus visiškai savarankiškas — veiks be interneto, be serverio,
naikintuvai/pinigai/lygiai išsaugomi tik atmintyje (kaip dabar žaidime).

---

## Kurį būdą rinktis?

| Noriu... | Būdas |
|---|---|
| Greitai pasidaryti ikoną telefone, testuoti | **1 būdas** |
| Tikro `.apk` failo be programavimo | **2 būdas** |
| Programėlės be interneto/serverio, galimybės tobulinti Android Studio | **3 būdas** |

Visi trys būdai yra **100% nemokami**, išskyrus, jei norėsite publikuoti į
Google Play parduotuvę — tada vienkartinis 25 USD mokestis Google.
