# WKPB Werklijst Generator

## Start hier

Gebruik het dashboard:

https://cultureelerfgoed.github.io/wkpb/

---

## Wat doet dit systeem?

Het systeem vergelijkt twee Excelbestanden (BRK-export) en genereert automatisch een WKPB-werklijst.

De verwerking draait via GitHub Actions. Er hoeft niets lokaal geïnstalleerd te worden.

---

## Basisproces

1. Open het dashboard
2. Klik op **START WKPB VERWERKING**
3. Gebruik als tag de datum van vandaag (YYYYMMDD)
4. Upload precies 2 Excelbestanden
5. Klik **Publish release**
6. Wacht tot het dashboard groen wordt
7. Download het resultaat

---

## Belangrijk

- Gebruik altijd een **nieuwe datum**
- Gebruik geen bestaande tag
- Krijgt u de melding “tag already exists”?  
  Voeg dan `-1`, `-2`, etc. toe aan de datum

Voorbeeld:

20260220  
20260220-1  
20260220-2  

---

## Output

Het resultaatbestand heet:

wkpb_werklijst_YYYYMMDD.xlsx

Dit bestand bevat:

- WKPB Lijst
- Samenvatting
- Audit verschil

---

Voor gebruikersinstructie zie: GEBRUIKERSHANDLEIDING.md