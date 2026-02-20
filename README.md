# WKPB Diff via GitHub

## TL;DR

Wilt u een WKPB-werklijst genereren?

1. Ga naar **Releases**
2. Klik op **Draft a new release**
3. Upload precies 2 Excelbestanden (.xlsx)
4. Klik op **Publish release**
5. Wacht ± 1 minuut
6. Download `wkpb_werklijst_YYYYMMDD.xlsx`

Bij fouten wordt de release automatisch gemarkeerd als **MISLUKT** met uitleg.

U hoeft niets te installeren.

---

# Doel

Deze repository genereert automatisch een WKPB-werklijst door twee Kadaster-exportbestanden met elkaar te vergelijken.

De verwerking draait volledig via GitHub Actions.

- Geen installatie
- Geen Python lokaal nodig
- Geen macro’s
- Geen handmatige diff

---

# Wat doet het systeem?

Het systeem:

1. Downloadt de twee geüploade Excelbestanden
2. Sorteert ze op naam (datum/tijd vooraan)
3. Bepaalt automatisch:
   - oudste bestand → oud.xlsx
   - nieuwste bestand → nieuw.xlsx
4. Telt per identificatie het aantal actieve BRK-objecten
5. Selecteert identificaties waarvoor geldt:
   - oud_actief = 0
   - nieuw_actief > 0
6. Genereert een Excelbestand met drie tabbladen

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
2. Vul een tag in (bijvoorbeeld: v2026-02-20)
3. Titel mag leeg blijven (wordt automatisch aangepast)

---

## Stap 3 – Upload precies 2 Excelbestanden

Upload:

- het oude bestand
- het nieuwe bestand

Voorbeeld bestandsnaam:

20260202 0907 BRK-PB De Staat (Onderwijs, Cultuur en Wetenschap).xlsx

Belangrijk:

- Upload exact 2 .xlsx bestanden
- Geen extra bestanden
- Bestandsnamen mogen blijven zoals ze zijn

Het systeem bepaalt zelf welk bestand oud en nieuw is op basis van de naam.

---

## Stap 4 – Klik op Publish release

De verwerking start automatisch.

---

## Stap 5 – Controleer de status

Ga naar het tabblad **Actions** om de voortgang te bekijken.

Na succesvolle verwerking:

- De releasetitel wordt automatisch aangepast naar:

  WKPB werklijst YYYYMMDD

- Alleen het resultaatbestand blijft zichtbaar bij Assets.

---

# Resultaatbestand

Het Excelbestand bevat drie tabbladen:

## 1. WKPB Lijst
De geselecteerde identificaties.

Kolommen:

- identificatie
- monumentnummer
- register
- kenmerk
- kadastraleGemeenteBRK
- sectieBRK
- perceelnummerBRK
- Wijzigingstype

## 2. Samenvatting
Aantal gewijzigde objecten.

## 3. Audit verschil
Per identificatie:

- oud_actief
- nieuw_actief
- reden: nieuw actief BRK-object

---

# Wanneer komt een object in de werklijst?

Een identificatie wordt opgenomen wanneer:

- In het oude bestand geen actief BRK-object aanwezig is
- In het nieuwe bestand één of meer actieve BRK-objecten aanwezig zijn

Actief betekent dat de kolom:

indicatieObjectVervallenBRK

de waarde bevat:

- WAAR
- TRUE
- 1

Hoofdlettergebruik maakt niet uit.

---

# Validatie en foutafhandeling

## Fout: niet precies 2 Excelbestanden

Als er minder of meer dan 2 bestanden zijn:

- De workflow stopt
- De releasetitel wordt aangepast naar:

  WKPB MISLUKT YYYYMMDD

- De release krijgt een foutmelding met uitleg

Maak daarna een nieuwe release met precies 2 bestanden.

---

## Fout: ontbrekende kolommen of ongeldig bestand

Als vereiste kolommen ontbreken of het bestand ongeldig is:

- De workflow stopt
- De releasetitel wordt aangepast naar:

  WKPB MISLUKT YYYYMMDD

- De release bevat uitleg

Controleer de bestandsstructuur en maak daarna een nieuwe release.

---

# Wat gebeurt er met de geüploade bestanden?

Na succesvolle verwerking:

- De twee oorspronkelijke Excelbestanden worden automatisch uit de release verwijderd
- Alleen het resultaatbestand blijft zichtbaar

Er blijven geen inputbestanden permanent in de repository staan.

---

# Vereiste kolommen in beide Excelbestanden

Beide bestanden moeten minimaal deze kolommen bevatten:

- identificatie
- indicatieObjectVervallenBRK
- monumentnummer
- register
- kenmerk
- kadastraleGemeenteBRK
- sectieBRK
- perceelnummerBRK

Ontbreekt een kolom, dan stopt de verwerking.

---

# Voor beheerders

Belangrijke bestanden in deze repository:

.github/workflows/run_wkpb.yml  
wkpb_core.py  
requirements.txt  

De workflow:

1. Downloadt release-assets
2. Valideert aantal bestanden
3. Sorteert en hernoemt
4. Draait het Python-script
5. Uploadt resultaat
6. Verwijdert inputbestanden
7. Past releasetitel automatisch aan

---

## TL;DR (nogmaals)

Draft release → Upload 2 Excelbestanden → Publish → Download resultaat.

Klaar.