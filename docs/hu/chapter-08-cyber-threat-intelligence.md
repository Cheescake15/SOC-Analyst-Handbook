# 08 — Kiberfenyegetettség-elemzés

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/08-cyber-threat-intelligence.md)

## Bevezetés

A SOC nemcsak azt figyeli, mi történik a saját rendszereiben. Fontos az is, hogy tudjuk, milyen támadók, módszerek és rosszindulatú infrastruktúrák jelennek meg a külvilágban.

Ezt segíti a **Cyber Threat Intelligence**, röviden CTI.

Magyarul leggyakrabban kiberfenyegetettség-elemzésnek vagy kiberfenyegetési hírszerzésnek nevezik.

A CTI lényege, hogy különböző forrásokból gyűjtött adatokat értelmez, összefüggésbe helyez, majd olyan információvá alakít, amely segítheti a védekezést.

Ebben a fejezetben a legfontosabb fogalmakat kezdő szinten mutatom be.

## 1. Adat, információ és intelligence

Ezt a három fogalmat érdemes különválasztani.

### Adat

Egy önálló tény vagy megfigyelés.

```text
203.0.113.45
```

Ez csak egy IP-cím. Önmagában nem tudjuk, miért fontos.

### Információ

Az adat már kap valamilyen jelentést.

```text
A 203.0.113.45 IP-címről
több rosszindulatú bejelentkezési
kísérletet észleltek.
```

### Intelligence

Az információt elemezték és olyan következtetés készült belőle, amely döntést segíthet.

```text
Az IP-cím egy aktív kampányhoz kapcsolódik,
amely VPN-rendszereket céloz.
A szervezetünk hasonló rendszert használ,
ezért érdemes ellenőrizni a kapcsolódó naplókat.
```

A CTI tehát nem egyszerű adatgyűjtés.

## 2. Mi az a threat actor?

A **threat actor**, magyarul fenyegetési szereplő, olyan személy vagy csoport, amely kibertámadást hajthat végre.

Lehet például:

- kiberbűnözői csoport
- állami hátterű csoport
- hacktivista
- belső elkövető
- alkalmi támadó

A célja lehet:

- pénzszerzés
- adatlopás
- kémkedés
- zsarolás
- szolgáltatás megbénítása
- politikai vagy ideológiai cél

A különböző támadók különböző módszereket használhatnak.

## 3. Mi az az IoC?

Az **IoC** az *Indicator of Compromise* rövidítése.

Egyszerűen olyan technikai nyom, amely rosszindulatú tevékenységhez kapcsolódhat.

Példák:

- IP-cím
- domainnév
- URL
- fájl hash
- e-mail-cím
- fájlnév

Példa:

```text
Domain: malicious-example.com
IP: 203.0.113.45
```

Fontos, hogy egy IoC önmagában nem mindig bizonyít támadást.

Egy IP-cím idővel más célra is használható, ezért mindig fontos a dátum és a forrás.

## 4. Mi az a hash?

A **hash** egy fájlból számított érték.

Egyszerű hasonlattal olyan, mint egy digitális ujjlenyomat.

Gyakori algoritmus:

```text
SHA-256
```

Ha egy ismert rosszindulatú fájl hash-e rendelkezésre áll, a szervezet megkeresheti, hogy ugyanez a fájl megjelent-e a saját rendszereiben.

A hash hátránya, hogy a fájl kis módosítása után teljesen megváltozik.

## 5. Mi az a TTP?

A **TTP** jelentése:

- Tactics
- Techniques
- Procedures

Magyarul nagyjából:

- taktika
- technika
- eljárás

A TTP nem egy konkrét IP-címet ír le, hanem azt, hogyan viselkedik egy támadó.

Példa:

```text
A támadó phishing e-mailt küld.
A dokumentum PowerShellt indít.
A PowerShell további kódot tölt le.
Egy ütemezett feladat jön létre.
```

A MITRE ATT&CK is támadói viselkedéseket és technikákat rendszerez.

## 6. IoC és TTP közötti különbség

| IoC | TTP |
|---|---|
| konkrét nyom | viselkedési minta |
| IP-cím | phishing |
| domain | PowerShell használata |
| fájl hash | jogosultságkiterjesztés |
| gyorsan változhat | gyakran tartósabb |

Egy támadó könnyen lecserélhet egy IP-címet.

A működési módszereinek megváltoztatása általában nehezebb.

## 7. Honnan származhat CTI?

### Belső források

A saját szervezetből:

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
- gyártói jelentések
- nyílt forrású adatbázisok
- kutatói blogok
- szakmai közösségek
- kereskedelmi CTI feedek

A **feed** folyamatosan frissülő adatforrás.

## 8. Nyílt forrású CTI

Sok CTI-forrás ingyenesen is elérhető.

Példák:

- MITRE ATT&CK
- MISP
- OpenCTI
- CISA közlemények
- CERT-EU jelentések
- NKI figyelmeztetések

Az NKI külön bemutatta az OpenCTI platformot is, amely CTI-információk rendszerezésére és megjelenítésére használható.

Nyílt forrás használatakor érdemes ellenőrizni:

- ki publikálta
- mikor frissítették
- milyen bizonyíték támasztja alá
- más megbízható forrás megerősíti-e

## 9. A CTI életciklusa

A threat intelligence nem egyszeri keresés, hanem ismétlődő folyamat.

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

### Példa kérdés

```text
Milyen támadások érintik jelenleg
az általunk használt VPN-megoldást?
```

A jó CTI mindig valamilyen konkrét kérdésből indul.

## 10. A CTI különböző szintjei

### Stratégiai

Vezetői döntéseket támogat.

Példa:

```text
Mely kiberfenyegetések jelentik
a legnagyobb üzleti kockázatot?
```

### Taktikai

A támadók módszereit vizsgálja.

```text
Milyen technikákat használ
egy adott támadócsoport?
```

### Műveleti

Konkrét kampányokkal foglalkozik.

```text
Milyen szervezeteket céloz
egy aktív phishing kampány?
```

### Technikai

Konkrét technikai jeleket ad.

```text
Mely domainek és IP-címek
kapcsolódnak a kampányhoz?
```

## 11. Mit jelent a confidence?

A CTI-ben gyakran jelzik, mennyire biztos az elemző a következtetésben.

Például:

- low confidence
- medium confidence
- high confidence

Fontos különbség:

```text
Tény:
Az IP-cím kapcsolatot létesített a szerverrel.

Értékelés:
Az IP-cím valószínűleg
egy támadási kampány része.
```

A második állítás már elemzői következtetés.

## 12. Mi az a TLP?

A **Traffic Light Protocol**, röviden TLP, azt jelzi, hogyan lehet egy információt továbbadni.

A TLP 2.0 jelölései:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

### TLP:RED

Nagyon szűk körben kezelendő.

### TLP:AMBER

Korlátozottan megosztható azokkal, akiknek szükségük van rá.

### TLP:GREEN

A közösségen belül megosztható, de nyilvánosan nem publikálható.

### TLP:CLEAR

Szabadon megosztható.

A TLP a megosztási határokat jelzi.

## 13. STIX és TAXII röviden

A CTI-adatokat gépek között is lehet továbbítani.

### STIX

A **STIX** egy strukturált formátum CTI-adatok leírására.

Például leírhat:

- indikátorokat
- malware-t
- támadócsoportokat
- technikákat
- kapcsolatokat

### TAXII

A **TAXII** olyan kommunikációs megoldás, amely CTI-adatok cseréjét támogatja rendszerek között.

Egyszerűen:

```text
STIX = az információ formátuma
TAXII = az információ továbbítása
```

Kezdőként ennyit elegendő megjegyezni.

## 14. Hogyan használja a CTI-t egy SOC?

### Riasztás gazdagítása

A SIEM riasztást készít egy IP-cím miatt.

A CTI segíthet megmutatni:

- ismert-e rosszindulatúként
- mely kampányhoz kapcsolódik
- mikor látták utoljára
- milyen tevékenységhez kötődik

### Threat hunting

Új információ alapján visszamenőleg lehet keresni.

```text
Láttuk-e ezt a domaint
az elmúlt 30 napban?
```

### Detektálás fejlesztése

Egy ismert támadói technika alapján új SIEM-szabály készülhet.

### Prioritás meghatározása

Egy riasztás sürgősebb lehet, ha egy aktuális kampányhoz kapcsolódik.

## 15. Egyszerű CTI-példa

Egy megbízható CERT figyelmeztetést tesz közzé:

```text
Új phishing kampány
célozza a pénzügyi szervezeteket.

Kapcsolódó domain:
secure-login-example.com

Módszer:
hamis Microsoft 365 bejelentkezési oldal
```

A SOC ezután:

1. megkeresi a domaint a DNS-naplókban
2. ellenőrzi, érkezett-e ilyen linket tartalmazó e-mail
3. megnézi, kattintott-e valaki a linkre
4. szükség esetén blokkolja a domaint
5. figyelmezteti az érintett felhasználókat
6. új detektálási szabályt készíthet

Így a külső információból konkrét védekezési lépés lesz.

## 16. A CTI korlátai

A threat intelligence nem mindig pontos vagy releváns.

Probléma lehet:

- elavult IoC
- hibás forrás
- téves attribúció
- kontextus nélküli adat
- túl sok használhatatlan indikátor
- más szervezet számára fontos, de nálunk irreleváns információ

A jó CTI:

- releváns
- időszerű
- megbízható
- érthető
- használható

## 17. Mit érdemes kezdőként megjegyezni?

- A CTI elemzett információ, nem puszta adatgyűjtés.
- Az IoC konkrét technikai nyom.
- A TTP a támadó viselkedését írja le.
- A MITRE ATT&CK segít rendszerezni a támadói technikákat.
- A CTI belső és külső forrásból is származhat.
- A forrás megbízhatóságát mindig ellenőrizni kell.
- A confidence a következtetés bizonyosságát jelzi.
- A TLP az információ megoszthatóságát jelöli.
- A STIX a formátum, a TAXII a továbbítás módja.
- A CTI akkor hasznos, ha konkrét döntést támogat.

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
   **Kiberfenyegetettség elemzés**  
   https://nki.gov.hu/intezet/tartalom/magunkrol/

2. Nemzeti Kiberbiztonsági Intézet  
   **Egy ingyenes nyílt forrású CTI platform**  
   https://nki.gov.hu/it-biztonsag/tanacsok/egy-ingyenes-nyilt-forrasu-cti-cyber-threat-intelligence-platform/

3. MITRE ATT&CK  
   **Get Started – Threat Intelligence**  
   https://attack.mitre.org/resources/get-started/threat-intelligence/

4. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

5. CERT-EU  
   **Cyber Threat Intelligence Framework**  
   https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

6. CISA  
   **Information Sharing**  
   https://www.cisa.gov/topic/cybersecurity-information-sharing

7. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

8. MITRE ATT&CK  
   **ATT&CK Data and Tools – STIX**  
   https://attack.mitre.org/resources/attack-data-and-tools/

---

[← Előző fejezet](07-siem-fundamentals.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](09-mitre-attack.md)
