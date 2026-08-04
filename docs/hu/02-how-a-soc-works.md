# 02 — Hogyan működik egy SOC?

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/02-how-a-soc-works.md)

## Bevezetés

Ebben a fejezetben azt foglalom össze, hogyan működik egy Security Operations Center, vagyis SOC. A témát kezdő nézőpontból közelítem meg, ezért elsősorban az alapvető szerepkörökre, folyamatokra és eszközökre koncentrálok.

A források alapján egy SOC nem csupán technológiai rendszerekből áll. A működéséhez szükség van megfelelő szakemberekre, jól meghatározott folyamatokra és olyan eszközökre, amelyek segítik a biztonsági események és riasztások kezelését.

A Nemzeti Kiberbiztonsági Intézet incidenskezelési platformokról szóló összefoglalója szerint az ilyen rendszerek a SOC-ok, CSIRT-ek és CERT-ek munkáját is támogathatják az események kivizsgálása során. Ez jól mutatja, hogy a technológia elsősorban az elemzői és incidenskezelési folyamatot segíti, nem pedig önállóan helyettesíti azt.

## 1. Emberek, folyamatok és technológia

A SOC működését gyakran három fő területre bontják:

- emberek
- folyamatok
- technológia

### Emberek

A SOC-ban különböző tapasztalati szintű és szakterületű munkatársak dolgozhatnak.

Ilyenek lehetnek:

- Tier 1 elemzők
- Tier 2 incidensvizsgálók
- senior elemzők
- threat hunterek
- detection engineerek
- incidenskezelők
- SOC mérnökök
- SOC menedzserek

Kisebb szervezetekben előfordulhat, hogy egy személy több feladatot is ellát.

### Folyamatok

A folyamatok azt határozzák meg, hogy egy riasztás vagy incidens esetén milyen lépéseket kell követni.

Például:

- hogyan történik a riasztások első ellenőrzése
- mikor kell egy ügyet magasabb szintre továbbítani
- hogyan kell dokumentálni a vizsgálatot
- ki jogosult egy végpont elkülönítésére
- hogyan történik a műszakátadás

A jól leírt folyamatok segítenek abban, hogy a különböző elemzők hasonló módon kezeljék az azonos típusú eseményeket.

A magyar nyelvű *Az információbiztonság alapjai* című egyetemi kiadvány is hangsúlyozza, hogy az információbiztonság nem kizárólag technikai kérdés. Szervezeti szabályokra, felelősségi körökre és tudatos működésre is szükség van.

### Technológia

A SOC többféle biztonsági eszközt használhat.

Gyakori példák:

- SIEM
- EDR vagy XDR
- IDS és IPS
- tűzfal
- e-mail-biztonsági rendszer
- threat intelligence platform
- SOAR
- jegykezelő rendszer

Ezek az eszközök összegyűjtik és rendszerezik az adatokat. A végső értékeléshez azonban továbbra is szükség van emberi elemzésre.

## 2. Milyen adatokkal dolgozik egy SOC?

A SOC többféle naplót és biztonsági adatot használhat.

Például:

- Windows Event Log
- Linux rendszer- és hitelesítési naplók
- tűzfalnaplók
- DNS-naplók
- VPN-naplók
- Active Directory események
- végponti telemetria
- felhőszolgáltatások auditnaplói
- e-mail-biztonsági események
- alkalmazásnaplók

Egyetlen esemény sokszor nem elegendő a döntéshez. Az elemzők ezért több adatforrást is összehasonlíthatnak.

### Egyszerű példa

Egy sikertelen bejelentkezés még nem feltétlenül jelent támadást.

Gyanúsabb lehet a helyzet, ha:

- rövid idő alatt sok sikertelen próbálkozás történik
- ezt sikeres belépés követi
- a forrás IP-cím szokatlan
- a felhasználó nem ismeri fel a tevékenységet

## 3. Hogyan keletkezik egy riasztás?

A rendszerek folyamatosan eseményeket generálnak. Ezek nagy része a normál működéshez tartozik.

Riasztás akkor jöhet létre, ha egy esemény megfelel egy előre meghatározott szabálynak.

Például:

```text
Ha egy felhasználónál 10 percen belül
20 sikertelen bejelentkezés történik,
majd sikeres belépés következik,
hozz létre riasztást.
```

Fontos, hogy egy riasztás önmagában még nem bizonyítja a támadást. Csak azt jelzi, hogy az eseményt érdemes megvizsgálni.

## 4. A riasztás tipikus életútja

Egy leegyszerűsített folyamat így nézhet ki:

```text
Esemény keletkezik
      ↓
A detektálási szabály felismeri
      ↓
Riasztás jön létre
      ↓
Első ellenőrzés
      ↓
További adatok gyűjtése
      ↓
Minősítés
      ↓
Lezárás vagy eszkaláció
```

### Első ellenőrzés

A triázs során az elemző rövid idő alatt megpróbálja eldönteni:

- mennyire sürgős az ügy
- érintett-e fontos rendszer
- valószínű lehet-e valódi fenyegetés
- szükség van-e részletesebb vizsgálatra

### Kontextusgyűjtés

A vizsgálat során további kérdések merülhetnek fel:

- ismert-e a forrás IP-cím
- szokásos-e a felhasználó helye
- milyen folyamat indult el
- volt-e más kapcsolódó riasztás
- érintett-e privilegizált fiók
- történt-e szokatlan fájlletöltés

### Minősítés

A riasztás minősítése lehet:

- true positive
- benign true positive
- false positive
- információs esemény
- további vizsgálatot igénylő ügy

## 5. Prioritás és súlyosság

A források alapján a prioritást nem csak a riasztás típusa határozza meg.

Fontos lehet:

- az érintett eszköz szerepe
- a felhasználó jogosultsági szintje
- az esetleges üzleti hatás
- az érintett adatok érzékenysége
- a fenyegetés aktivitása
- az érintett rendszerek száma

Egy tesztfiók sikertelen bejelentkezése például kevésbé súlyos lehet, mint ugyanez egy rendszergazdai fióknál.

## 6. Playbook és runbook

A SOC-ok gyakran előre elkészített eljárásokat használnak.

### Playbook

A playbook egy eseménytípus kezelésének fő lépéseit írja le.

Egy phishing playbook például tartalmazhatja:

1. az e-mail fejlécének ellenőrzését
2. a hivatkozások vizsgálatát
3. a címzettek azonosítását
4. az érintett fiókok ellenőrzését
5. az eredmények dokumentálását

### Runbook

A runbook részletesebb technikai utasításokat adhat.

Például:

- melyik SIEM-lekérdezést kell futtatni
- hogyan kell egy végpontot elkülöníteni
- milyen mezőket kell kitölteni a jegyben

A két kifejezést a szervezetek nem mindig ugyanúgy használják.

## 7. Eszkaláció

Az eszkaláció azt jelenti, hogy az ügyet egy tapasztaltabb vagy más szakterületen dolgozó szakemberhez továbbítják.

Erre szükség lehet, ha:

- kritikus rendszer érintett
- privilegizált fiók érintett
- több rendszer kompromittálódhatott
- adatvesztés gyanúja merül fel
- az eset meghaladja az elemző jogosultságát
- azonnali beavatkozás szükséges

## 8. Együttműködés más csapatokkal

A SOC gyakran együttműködik más szervezeti egységekkel.

Ilyenek lehetnek:

- IT üzemeltetés
- Identity and Access Management
- jogi osztály
- adatvédelmi csapat
- HR
- kommunikáció
- vezetőség

A SOC-nak nemcsak technikai adatokat kell továbbítania. Fontos, hogy érthetően összefoglalja, mi történt és milyen intézkedés szükséges.

## 9. Műszakátadás

A folyamatosan működő SOC-ban fontos a nyitott ügyek átadása.

Egy jó műszakátadás tartalmazhatja:

- a nyitott riasztásokat
- az aktív incidenseket
- az elvégzett lépéseket
- a következő feladatokat
- a kapcsolódó jegyszámot
- a fontos határidőket

### Rövid példa

```text
A WS-104 végponton gyanús PowerShell-parancs futott 22:14-kor.
Az EDR-vizsgálat elindult.
A végpont még nincs elkülönítve.
Következő lépés: process tree és hálózati kapcsolatok ellenőrzése.
Jegy: INC-2481.
```

## 10. Automatizálás

A SOAR és más automatizálási megoldások ismétlődő feladatokat végezhetnek el.

Például:

- IP-cím reputációjának ellenőrzése
- fájlhash vizsgálata
- jegy létrehozása
- értesítés küldése
- e-mail karanténba helyezése

Az automatizálás gyorsíthatja a munkát, de hibás beállítás esetén problémát is okozhat. Nagy hatású műveleteknél ezért emberi jóváhagyásra lehet szükség.

## 11. Teljesítménymérés

A SOC működését többféle mutatóval mérhetik.

Például:

- Mean Time to Detect
- Mean Time to Acknowledge
- Mean Time to Respond
- Mean Time to Contain
- False Positive Rate
- Alert Volume

Ezek a mutatók segíthetnek a folyamatok értékelésében, de önmagukban nem adnak teljes képet.

## 12. Összefoglalás

A források alapján egy SOC hatékony működéséhez emberekre, folyamatokra és technológiára egyaránt szükség van.

A riasztások kezelése során az elemző:

- ellenőrzi az eseményt
- további adatokat gyűjt
- értékeli a kockázatot
- dokumentálja a vizsgálatot
- szükség esetén eszkalál

## Ellenőrző kérdések

1. Mi a SOC három fő eleme?
2. Milyen adatforrásokat használhat egy SOC?
3. Mi a különbség egy esemény és egy riasztás között?
4. Mit jelent a triázs?
5. Milyen tényezők befolyásolhatják a prioritást?
6. Mi a playbook célja?
7. Mikor lehet szükség eszkalációra?
8. Miért fontos a műszakátadás?
9. Milyen feladatokat automatizálhat egy SOAR?
10. Miért nem elegendő csak a riasztások számát mérni?

## Források

1. NIST SP 800-61 Rev. 3  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. NIST Cybersecurity Framework 2.0  
   https://www.nist.gov/cyberframework

3. CISA Cybersecurity Incident and Vulnerability Response Playbooks  
   https://www.cisa.gov/news-events/news/cisa-releases-updated-cybersecurity-incident-and-vulnerability-response-playbooks

4. MITRE ATT&CK Data Sources  
   https://attack.mitre.org/datasources/

5. Nemzeti Kiberbiztonsági Intézet  
   **Incidenskezelési platformok**  
   https://nki.gov.hu/it-biztonsag/tanacsok/incidenskezelesi-platformok/

6. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](01-introduction.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](03-network-fundamentals.md)
