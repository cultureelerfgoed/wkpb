# WKPB Diff via GitHub

## TL;DR

Wilt u een WKPB-werklijst genereren?

1. Ga naar **Releases**
2. Klik op **Draft a new release**
3. Upload precies 2 Excelbestanden (oude en nieuwe export)
4. Klik op **Publish release**
5. Wacht ±1 minuut
6. Download `wkpb_werklijst_YYYYMMDD.xlsx`

De twee geüploade bestanden worden automatisch verwijderd.
Er blijft alleen het resultaatbestand over.

Geen installatie. Geen macro’s. Geen handmatige diff.

---

# Doel

Deze repository berekent automatisch een WKPB-werklijst door twee Kadaster-exportbestanden met elkaar te vergelijken.

Alles draait via GitHub Actions.
U hoeft niets te installeren.

---

# Wat doet het systeem?

Het systeem:

1. Leest het oude Excelbestand
2. Leest het nieuwe Excelbestand
3. Telt per identificatie het aantal actieve BRK-objecten
4. Selecteert identificaties waarvoor geldt:
   - oud_actief = 0
   - nieuw_actief > 0
5. Neemt het eerste record uit het nieuwe bestand
6. Schrijft een Excelbestand met drie tabbladen

De output heet:

wkpb_werklijst_YYYYMMDD.xlsx

---

# Stappen voor de gebruiker

## Stap 1 – Ga naar Releases

1. Open de repository
2. Klik op **Releases**

---

## Stap 2 – Maak een nieuwe Release

1. Klik op **Draft a new release**
2. Vul een tag in, bijvoorbeeld:
   v2026-02-20
3. Titel mag hetzelfde zijn als de tag

---

## Stap 3 – Upload precies 2 Excelbestanden

Upload:

- het oude bestand
- het nieuwe bestand

Voorbeeld bestandsnaam:

20260202 0907 BRK-PB De Staat (Onderwijs, Cultuur en Wetenschap).xlsx

Belangrijk:

- De naam mag blijven zoals hij is
- Het systeem bepaalt automatisch welk bestand oud en nieuw is
- Dit gebeurt op basis van de datum/tijd aan het begin van de bestandsnaam
- Upload precies 2 .xlsx bestanden

Als dit niet klopt, stopt de verwerking.

---

## Stap 4 – Publiceer de Release

Klik op **Publish release**.

De verwerking start automatisch.

---

## Stap 5 – Wacht tot de verwerking klaar is

1. Ga naar tab **Actions**
2. Open de meest recente workflow
3. Wacht tot alles groen is

Dit duurt meestal minder dan 1 minuut.

---

## Stap 6 – Download het resultaat

Ga terug naar **Releases**.

Download:

wkpb_werklijst_YYYYMMDD.xlsx

De twee oorspronkelijke Excelbestanden zijn automatisch verwijderd.

---

# Inhoud van het resultaatbestand

Het Excelbestand bevat drie tabbladen:

1. WKPB Lijst
2. Samenvatting
3. Audit verschil

---

# Vereiste kolommen in beide Excelbestanden

De volgende kolommen moeten aanwezig zijn:

- identificatie
- indicatieObjectVervallenBRK
- monumentnummer
- register
- kenmerk
- kadastraleGemeenteBRK
- sectieBRK
- perceelnummerBRK

Ontbreekt een kolom, dan stopt de workflow.

---

# Wanneer is een object actief?

Een record geldt als actief wanneer:

indicatieObjectVervallenBRK

de waarde heeft:

- WAAR
- TRUE
- 1

Hoofdletters maken niet uit.

---

# Wat gebeurt er met de geüploade bestanden?

Na verwerking:

- Worden de twee inputbestanden automatisch verwijderd uit de Release
- Blijft alleen het resultaatbestand zichtbaar

De bestanden blijven niet permanent in de repository staan.

---

# Wat als er iets misgaat?

Ga naar:

Actions → laatste run

Bekijk de foutmelding in de log.

Veelvoorkomende oorzaken:

- Niet precies 2 Excelbestanden geüpload
- Onjuiste kolomnamen
- Bestand is geen geldig .xlsx bestand

Maak daarna een nieuwe Release en probeer opnieuw.

---

# Voor beheerders

Belangrijke bestanden:

wkpb_core.py  
.github/workflows/run_wkpb.yml  
requirements.txt  

Trigger:

release → published

De workflow:

1. Downloadt beide Excelbestanden
2. Sorteert ze op naam
3. Hernoemt naar oud.xlsx en nieuw.xlsx
4. Draait het Python-script
5. Uploadt de output
6. Verwijdert de oorspronkelijke inputbestanden

---

## TL;DR (kort)

Draft release → Upload 2 bestanden → Publish → Download resultaat.