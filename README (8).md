# Dicteermachine

Een zelfstandige web-app die je gesproken woord omzet naar tekst — volledig in je eigen browser, in het Nederlands of Engels. Je kunt het transcript naar een andere taal vertalen en beide versies downloaden als Word-bestand.

De app is één HTML-bestand zonder server of back-end. Je opent `dicteermachine.html` in een moderne browser, of je host het op een statische plek zoals GitHub Pages.

---

## Voor de gebruiker

### Zo werkt het

1. **Kies je instellingen** rechts: dicteertaal (Nederlands of Engels), je steekwoorden, de maximale dicteertijd en de nauwkeurigheid van het model.
2. **Klik op “Start dicteren.”** De eerste keer wordt het AI-model eenmalig gedownload; dat kan even duren. Daarna staat het lokaal in je browser en gaat starten sneller.
3. **Spreek rustig in.** Je tekst verschijnt live in het transcriptveld. Je kunt op elk moment zelf in het veld typen en corrigeren.
4. **Pauzeer met je steekwoord** (zie hieronder) of met de knop “Pauzeer.”
5. **Vertaal** het hele transcript naar een andere taal en **download** het transcript en/of de vertaling als Word-bestand.

Zolang het dicteren loopt, draait het gele rondje linksboven als animatie. Dat is je teken dat de app actief luistert. Bij pauze draait het rondje langzamer.

### Steekwoorden (zelf te kiezen commando's)

Je bepaalt zelf met welk woord je het dicteren pauzeert en met welk woord je weer verdergaat. Standaard staan er **“pauze”** en **“verder,”** maar je kunt die vervangen door elk woord dat je wilt — bijvoorbeeld “stop” en “doorgaan.”

- Zeg je **pauzeer-commando** en de app stopt met opschrijven. De tekst tot aan het commando blijft staan; het commando zelf komt niet in het transcript.
- Tijdens de pauze blijft de app luisteren naar je **doorgaan-commando**. Zodra je dat zegt, gaat het dicteren verder.

**Tip:** kies commando's die je zelden in gewone zinnen gebruikt, zodat je niet per ongeluk pauzeert.

### Vertalen en downloaden

- **Download als Word** onder het transcript levert je gedicteerde tekst als `.docx`.
- In het blok **Vertaling** kies je een doeltaal (Engels, Nederlands, Duits, Frans of Spaans), klik je op **Vertaal transcript** en download je die vertaling apart als Word-bestand met **Download vertaling als Word.** Het originele transcript blijft ongewijzigd staan.

Vertalen naar Duits, Frans of Spaans loopt automatisch via het Engels als tussenstap. Dat kan de kwaliteit iets beïnvloeden; controleer de vertaling altijd voordat je hem gebruikt.

### Maximale dicteertijd

Omdat alles lokaal in je browser draait en de audio in het werkgeheugen staat, geldt er een maximum. Standaard is dat **15 minuten,** instelbaar tot **30 minuten.** De klok telt af en de balk kleurt oranje en daarna rood naarmate je de grens nadert. Bij 0 stopt het dicteren automatisch; je transcript blijft staan.

### Wat je nodig hebt

- Een recente browser: Chrome, Edge of Firefox (Safari 14+ werkt meestal ook).
- Toestemming voor de microfoon.
- Voor de eerste keer: een internetverbinding om de modellen eenmalig te downloaden. Daarna werkt de app ook offline.

---

## Privacyvoorwaarden en verwerking

### Korte samenvatting

De app verwerkt je spraak en tekst **uitsluitend lokaal in je eigen browser.** Er wordt geen audio, tekst of persoonsgegeven naar een server van de universiteit of van derden gestuurd. Er worden geen gegevens opgeslagen buiten je eigen apparaat.

### Welke gegevens worden verwerkt

- **Audio van je microfoon**, alleen tijdens het actieve dicteren. De audio wordt in kleine fragmenten in het werkgeheugen omgezet naar tekst en daarna direct weggegooid. Er wordt geen geluidsopname bewaard.
- **De tekst** die je dicteert, typt of laat vertalen. Die staat alleen in het geheugen van de pagina en verdwijnt zodra je de pagina sluit of ververst, tenzij je hem zelf als Word-bestand hebt gedownload.

### Waar de verwerking plaatsvindt

Alle spraakherkenning en vertaling draaien met open-source AI-modellen die in je browser worden uitgevoerd (via de bibliotheek Transformers.js van Hugging Face, met ONNX Runtime Web op WebAssembly of WebGPU). Er is geen cloud-API die je woorden ontvangt.

### Modelbestanden en caching

De AI-modellen worden bij het eerste gebruik gedownload vanaf de Hugging Face-modelhub en daarna door je browser lokaal bewaard (in IndexedDB / de browsercache), zodat ze niet elke keer opnieuw hoeven te worden opgehaald. Bij dat downloaden ziet Hugging Face — net als bij elk gewoon bezoek aan een website — technische verbindingsgegevens zoals je IP-adres. Je gedicteerde audio of tekst gaat hier nooit naartoe; alleen de modelbestanden komen binnen.

### Gebruik van AI

- **Spraak naar tekst:** OpenAI **Whisper** (multilingual), open source.
- **Vertaling:** Helsinki-NLP **OPUS-MT**, open source, per taalpaar.

Deze modellen genereren automatisch tekst en kunnen fouten maken: verkeerd verstane woorden, ontbrekende interpunctie of vertaalfouten. De uitvoer is een hulpmiddel, geen bron van waarheid. Controleer en corrigeer het resultaat altijd zelf voordat je het gebruikt of deelt, zeker bij gevoelige of formele inhoud.

### Jouw verantwoordelijkheid

Je bepaalt zelf wat je inspreekt. Wees terughoudend met bijzondere persoonsgegevens en met vertrouwelijke informatie van anderen. Gedownloade Word-bestanden bewaar je op een plek die past bij de gevoeligheid van de inhoud.

### AVG / GDPR

Doordat er geen persoonsgegevens naar een centrale server of derde partij worden verzonden en niets buiten je apparaat wordt opgeslagen, is er in de kern geen externe verwerking van jouw dicteerinhoud. Voor gebruik binnen de universiteit geldt aanvullend het vigerende privacy- en AI-beleid van de instelling.

---

## Technisch (voor beheerders)

- **Bestand:** één zelfstandig `dicteermachine.html`. Geen build-stap, geen back-end.
- **Afhankelijkheden:** Transformers.js wordt op de client geladen via een CDN. De Word-export gebruikt een eigen, in de app ingebouwde ZIP-schrijver, zonder externe bibliotheek.
- **Hosting:** werkt op elke statische host over HTTPS (bijvoorbeeld GitHub Pages). HTTPS is vereist voor microfoontoegang en modelcaching.
- **Modellen:** `Xenova/whisper-tiny | base | small` voor spraakherkenning; `Xenova/opus-mt-*` voor vertaling.
- **Aanpassen:** doeltalen, standaard-steekwoorden en de maximale dicteertijd zijn direct in de HTML terug te vinden en te wijzigen.

---

*Gemaakt voor het Programma AI in het Onderwijs, Universiteit Utrecht.*
