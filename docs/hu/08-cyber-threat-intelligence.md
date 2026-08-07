# 08 — Kiberfenyegetettség-elemzés

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/08-cyber-threat-intelligence.md)

## Bevezetés

A SOC nemcsak azt figyeli, mi történik a saját rendszereiben, fontos az is, hogy tudjuk, milyen támadók, módszerek és rosszindulatú infrastruktúrák jelennek meg a külvilágban.

Ezt segíti a Cyber Threat Intelligence, röviden CTI.

Magyarul leggyakrabban kiberfenyegetettség-elemzésnek vagy kiberfenyegetési hírszerzésnek nevezik.

A Nemzeti Kiberbiztonsági Intézet szerint a CTI különböző forrásokból gyűjtött adatok és információk elemzésével segít felmérni a potenciális veszélyforrásokat, felismerni a támadási mintákat és támogatni a védekezést.

Ebben a fejezetben a CTI alapfogalmait kezdő szinten mutatom be.

## 1. Adat, információ és intelligence

### Adat

Egy önálló tény vagy megfigyelés.

```text
203.0.113.45
```

Ez csak egy IP-cím. Önmagában nem tudjuk, miért érdekes.

### Információ

Az adat már kap valamilyen jelentést.

```text
A 203.0.113.45 IP-címről
rosszindulatú bejelentkezési kísérleteket észleltek.
```

### Intelligence

Az információt elemezték, összefüggésbe helyezték, és döntést segítő következtetés készült belőle.

```text
Az IP-cím egy aktív támadási kampányhoz kapcsolódik,
amely VPN-rendszereket céloz.
A szervezetünk hasonló VPN-megoldást használ,
ezért érdemes ellenőrizni a kapcsolódó naplókat.
```

A CTI tehát nem egyszerű adatgyűjtés. Az értéke abból származik, hogy az adatból használható következtetés készül.

## 2. Mi az a threat actor?

A **threat actor**, magyarul fenyegetési szereplő, olyan személy vagy csoport, amely kibertámadást hajthat végre.

Lehet például:

- kiberbűnözői csoport
- állami hátterű csoport
- hacktivista
- belső elkövető
- alkalmi támadó

A céljaik eltérhetnek:

- pénzszerzés
- adatlopás
- kémkedés
- zsarolás
- szolgáltatás megbénítása
- politikai vagy ideológiai cél

## 3. Mi az az IoC?

Az **IoC** az *Indicator of Compromise* rövidítése.

Egyszerűen olyan technikai nyom, amely ismert vagy feltételezett rosszindulatú tevékenységhez kapcsolódhat.

Példák:

- rosszindulatú IP-cím
- domainnév
- URL
- fájl hash
- e-mail-cím
- fájlnév

Példa:

```text
Domain: malicious-example.com
IP: 203.0.113.45
SHA256: 4a7d1ed414474e4033ac29ccb8653d9b...
```

Egy IoC önmagában nem mindig bizonyít támadást. Egy IP-cím idővel más tulajdonoshoz kerülhet, vagy már nem lehet aktív. Ezért mindig kell kontextus és időbélyeg.

## 4. Mi az a hash?

A **hash** egy fájlból számított, rögzített hosszúságú érték.

Egyszerű hasonlattal olyan, mint egy digitális ujjlenyomat.

Gyakori algoritmus:

```text
SHA-256
```

Ha két fájl hash-e azonos, az erős jel arra, hogy ugyanarról a tartalomról van szó.

A hash hátránya, hogy a fájl apró módosítása után teljesen megváltozik.

## 5. Mi az a TTP?

A **TTP** jelentése:

- Tactics
- Techniques
- Procedures

Magyarul nagyjából taktika, technika és eljárás.

Ez nem egy konkrét IP-címet vagy fájlt ír le, hanem azt, hogyan dolgozik egy támadó.

Például:

```text
A támadó adathalász e-mailt küld.
A dokumentum PowerShellt indít.
A PowerShell további kódot tölt le.
A támadó új ütemezett feladatot hoz létre.
```

A MITRE ATT&CK közös nyelvet biztosít a támadói viselkedések leírására és összehasonlítására.

## 6. IoC és TTP közötti különbség

| IoC | TTP |
|---|---|
| konkrét nyom | viselkedési minta |
| IP-cím | adathalászat |
| domain | PowerShell használata letöltésre |
| fájl hash | jogosultságkiterjesztés |
| gyorsan változhat | gyakran tartósabb |

Egy támadó könnyen lecserélhet egy IP-címet vagy fájlt. A működési módszereinek megváltoztatása gyakran nehezebb.

## 7. CTI-források

### Belső források

A saját szervezet adatai:

- SIEM-riasztások
- tűzfalnaplók
- EDR-adatok
- incidensjelentések
- phishing bejelentések
- malware-elemzések

### Külső források

Például:

- CERT és CSIRT figyelmeztetések
- NKI riasztások
- gyártói biztonsági jelentések
- nyílt forrású adatbázisok
- kutatói blogok
- szakmai közösségek
- kereskedelmi CTI feedek

A **feed** folyamatosan frissülő adatforrást jelent.

## 8. Nyílt forrású CTI

Számos nyílt forrású adat és platform érhető el.

Például:

- MITRE ATT&CK
- MISP
- OpenCTI
- CISA közlemények
- CERT-EU jelentések
- NKI figyelmeztetések

Az NKI külön bemutatta az OpenCTI platformot is. Ez technikai és nem technikai CTI-információk tárolására, rendszerezésére és megjelenítésére használható.

Nyílt forrás esetén érdemes ellenőrizni:

- ki publikálta
- mikor frissítették
- milyen bizonyíték támasztja alá
- más megbízható forrás megerősíti-e

## 9. A CTI életciklusa

Egy egyszerűsített modell:

```text
1. Igény meghatározása
        ↓
2. Adatgyűjtés
        ↓
3. Feldolgozás
        ↓
4. Elemzés
        ↓
5. Megosztás
        ↓
6. Visszajelzés
        ↺
```

### Igény meghatározása

Először kérdést kell megfogalmazni.

```text
Milyen támadások érintik jelenleg
az általunk használt VPN-megoldást?
```

### Adatgyűjtés

Releváns források keresése.

### Feldolgozás

Az adatok rendezése és egységesítése.

### Elemzés

Annak értékelése, mit jelentenek az adatok a saját szervezet számára.

### Megosztás

Az eredmény eljuttatása annak, akinek szüksége van rá.

### Visszajelzés

Annak ellenőrzése, hogy az információ hasznos volt-e.

## 10. Stratégiai, taktikai, műveleti és technikai CTI

### Stratégiai

Vezetői döntéseket támogat.

```text
Mely kiberfenyegetések jelentik
a legnagyobb üzleti kockázatot?
```

### Taktikai

A támadók módszereit vizsgálja.

```text
Milyen MITRE ATT&CK technikákat
használ egy adott támadócsoport?
```

### Műveleti

Konkrét kampányokkal foglalkozik.

```text
Milyen szervezeteket céloz
a jelenlegi phishing kampány?
```

### Technikai

Konkrét technikai jeleket ad.

```text
Mely IP-címek és domainek
kapcsolódnak a kampányhoz?
```

A kategóriák elnevezése és határa forrásonként eltérhet.

## 11. Mi az a confidence?

A CTI-elemzésben gyakran meg kell adni, mennyire biztos az elemző a következtetésben.

Példák:

- low confidence
- medium confidence
- high confidence

A CERT-EU 2026-os CTI keretrendszere külön foglalkozik a bizonytalanság és a confidence kezelésével.

Fontos különbség:

```text
Tény: az IP-cím kapcsolatot létesített a szerverrel.

Értékelés: az IP-cím valószínűleg
egy ismert támadási kampány része.
```

## 12. Mi az a TLP?

A **Traffic Light Protocol**, röviden TLP, azt jelzi, hogyan lehet egy információt továbbadni.

A TLP 2.0 jelölései:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

Egyszerűen:

- **RED** nagyon szűk körben kezelendő
- **AMBER** korlátozottan megosztható
- **GREEN** közösségen belül megosztható
- **CLEAR** szabadon megosztható

A TLP a megosztási határokat jelzi.

## 13. STIX és TAXII röviden

### STIX

A **STIX** egy strukturált formátum CTI-adatok leírására.

Leírhat például:

- indikátorokat
- malware-t
- támadócsoportokat
- kapcsolatokat
- technikákat

### TAXII

A **TAXII** olyan kommunikációs mechanizmus, amelyen keresztül CTI-adatokat lehet megosztani rendszerek között.

Egyszerű hasonlattal:

```text
STIX = az információ formátuma
TAXII = a szállítás módja
```

## 14. CTI használata egy SOC-ban

### Riasztás gazdagítása

A CTI plusz információt adhat egy IP-címről, domainről vagy fájlról.

### Threat hunting

Új információ alapján visszamenőleg kereshetünk.

```text
Láttuk-e ezt a domaint
az elmúlt 30 napban?
```

### Detektálás fejlesztése

Egy ismert TTP alapján új SIEM-szabály készíthető.

### Prioritás meghatározása

Egy riasztás fontosabb lehet, ha éppen aktív kampányhoz kapcsolódik.

## 15. Egyszerű CTI-példa

Egy megbízható CERT figyelmeztetést ad ki:

```text
Új phishing kampány
célozza a pénzügyi szervezeteket.

Kapcsolódó domain:
secure-login-example.com

Jellemző módszer:
hamis Microsoft 365 bejelentkezési oldal
```

A SOC ezután:

1. ellenőrzi, megjelent-e a domain a DNS-naplókban
2. megkeresi, érkezett-e ilyen linket tartalmazó e-mail
3. ellenőrzi, kattintott-e felhasználó a linkre
4. szükség esetén blokkolja a domaint
5. figyelmezteti az érintett felhasználókat
6. új detektálási szabályt készíthet

Így a külső információból konkrét védekezési lépés lesz.

## 16. A CTI korlátai

Probléma lehet:

- elavult IoC
- hibás forrás
- téves attribúció
- kontextus nélküli adat
- túl sok használhatatlan indikátor
- más szervezet számára releváns információ

A jó CTI:

- releváns
- időszerű
- megbízható
- érthető
- használható

## 17. Mit érdemes kezdőként megjegyezni?

- A CTI nem egyszerű adatgyűjtés, hanem elemzett információ.
- Az IoC konkrét technikai nyom.
- A TTP azt írja le, hogyan dolgozik egy támadó.
- A MITRE ATT&CK közös nyelvet ad a támadói viselkedéshez.
- A CTI belső és külső forrásból is származhat.
- Nem minden feed releváns minden szervezet számára.
- A bizonytalanságot és a megbízhatóságot jelezni kell.
- A TLP az információ megoszthatóságát jelzi.
- A STIX strukturálja, a TAXII továbbíthatja a CTI-adatokat.
- A CTI akkor igazán hasznos, ha konkrét védekezési döntést támogat.

## 18. Ellenőrző kérdések

1. Mit jelent a CTI rövidítés?
2. Mi a különbség adat, információ és intelligence között?
3. Mi az a threat actor?
4. Mi az az IoC?
5. Mi az a hash?
6. Mit jelent a TTP?
7. Mi a különbség IoC és TTP között?
8. Milyen belső CTI-források létezhetnek?
9. Milyen külső források használhatók?
10. Melyek a CTI életciklus fő lépései?
11. Mi a stratégiai CTI?
12. Mit jelent a confidence level?
13. Mire szolgál a TLP?
14. Mi a különbség a STIX és TAXII között?
15. Hogyan használhatja a CTI-t egy SOC?

## Források

1. Nemzeti Kiberbiztonsági Intézet  
   **Magunkról – Kiberfenyegetettség elemzés**  
   https://nki.gov.hu/intezet/tartalom/magunkrol/

2. Nemzeti Kiberbiztonsági Intézet  
   **Egy ingyenes nyílt forrású CTI platform**  
   https://nki.gov.hu/it-biztonsag/tanacsok/egy-ingyenes-nyilt-forrasu-cti-cyber-threat-intelligence-platform/

3. Nemzeti Közszolgálati Egyetem  
   **Kiberfenyegetettség elemzés – képzési program**  
   https://kti.uni-nke.hu/document/vtkk-uni-nke-hu/Elektronikus%20inform%C3%A1ci%C3%B3biztons%C3%A1gi%20vezet%C5%91%20-%20K%C3%A9pz%C3%A9si%20program%202025.pdf

4. MITRE ATT&CK  
   **Get Started – Threat Intelligence**  
   https://attack.mitre.org/resources/get-started/threat-intelligence/

5. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

6. CERT-EU  
   **Cyber Threat Intelligence Framework**  
   https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

7. CISA  
   **Information Sharing**  
   https://www.cisa.gov/topic/cybersecurity-information-sharing

8. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

9. MITRE ATT&CK  
   **ATT&CK Data and Tools – STIX**  
   https://attack.mitre.org/resources/attack-data-and-tools/

---

[← Előző fejezet](07-siem-fundamentals.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](09-mitre-attack.md)
