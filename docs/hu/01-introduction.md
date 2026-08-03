# 01 — Bevezetés a biztonsági műveletekbe

[← Vissza a magyar tartalomjegyzékhez](../../README.hu.md) | [English version](../en/01-introduction.md)

## A fejezet célja

Ez a fejezet bemutatja a Security Operations Center (SOC) szerepét, a Blue Team alapvető feladatait, a SOC-elemzők tipikus felelősségi köreit, valamint a különböző elemzői szintek közötti különbségeket.

A fejezet végére az olvasó képes lesz:

- meghatározni, mi a SOC és miért van rá szükség
- megkülönböztetni a Blue Team és a Red Team szerepét
- bemutatni egy SOC-elemző alapvető feladatait
- megkülönböztetni a Tier 1, Tier 2 és Tier 3 szerepköröket
- felismerni a NOC és a SOC közötti különbséget
- áttekinteni egy biztonsági riasztás tipikus életútját

---

## 1. Mi az a Security Operations Center?

A **Security Operations Center**, röviden **SOC**, egy szervezeti funkció vagy szakértői csoport, amely folyamatosan figyeli, elemzi és védi egy szervezet informatikai környezetét.

A NIST terminológiájában a SOC a szervezet biztonsági műveleteinek központi eleme. A gyakorlatban ez azt jelenti, hogy a SOC különböző biztonsági eszközökből és rendszerekből érkező adatokat gyűjt és elemez, majd reagál a gyanús vagy káros eseményekre.

A SOC által figyelt környezet többek között a következőket foglalhatja magában:

- munkaállomások és laptopok
- kiszolgálók
- hálózati eszközök
- felhőszolgáltatások
- felhasználói fiókok
- üzleti alkalmazások
- végpontvédelmi rendszerek
- tűzfalak és behatolásérzékelő rendszerek
- napló- és eseménykezelő platformok

A SOC nem feltétlenül egyetlen fizikai helyiséget jelent. Működhet:

- belső szervezeti egységként
- több telephelyen elosztva
- teljesen távoli csapatként
- kiszervezett szolgáltatásként
- hibrid modellben

A kiszervezett biztonsági megfigyelést gyakran **Managed Security Service Provider** (MSSP) vagy **Managed Detection and Response** (MDR) szolgáltató végzi.

---

## 2. Miért van szükség SOC-ra?

A modern szervezetek nagyszámú eszközt, alkalmazást, felhasználói fiókot és felhőszolgáltatást működtetnek. Ezek folyamatosan naplóbejegyzéseket és biztonsági eseményeket generálnak.

Egyetlen biztonsági eszköz önmagában nem képes teljes képet adni a szervezet állapotáról. A SOC feladata, hogy a különböző forrásokból érkező adatokat összekapcsolja, értelmezze és prioritás szerint kezelje.

A SOC legfontosabb céljai:

1. **Folyamatos megfigyelés**  
   A rendszerekből érkező biztonsági események ellenőrzése.

2. **Fenyegetések észlelése**  
   Gyanús viselkedés, támadási minták és kompromittálódási jelek felismerése.

3. **Riasztások vizsgálata**  
   Annak eldöntése, hogy egy riasztás valódi fenyegetést vagy téves találatot jelent-e.

4. **Incidensek kezelése**  
   A károk korlátozása, a támadói tevékenység megszakítása és a helyreállítás támogatása.

5. **Láthatóság biztosítása**  
   A szervezet biztonsági helyzetének bemutatása a műszaki és vezetői szereplők számára.

6. **Folyamatos fejlesztés**  
   A korábbi eseményekből levont tanulságok felhasználása a védelem javítására.

A NIST Cybersecurity Framework 2.0 hat fő funkciót különböztet meg:

- **Govern** — irányítás
- **Identify** — azonosítás
- **Protect** — védelem
- **Detect** — észlelés
- **Respond** — reagálás
- **Recover** — helyreállítás

A SOC különösen szorosan kapcsolódik a Detect, Respond és Recover funkciókhoz, de hatékony működéséhez az irányítási, azonosítási és védelmi tevékenységekkel is együtt kell működnie.

---

## 3. Mi az a Blue Team?

A **Blue Team** a szervezet védekező biztonsági oldalát jelenti. Feladata az informatikai rendszerek védelme, a támadások felismerése, az incidensek kezelése és a biztonsági képességek fejlesztése.

A Blue Team tevékenységei közé tartozhat:

- biztonsági események megfigyelése
- naplóelemzés
- riasztások vizsgálata
- incidenskezelés
- végpontok és hálózatok védelme
- sebezhetőségek kezelésének támogatása
- threat intelligence felhasználása
- detektálási szabályok fejlesztése
- threat hunting
- biztonsági kontrollok ellenőrzése
- jelentések és dokumentációk készítése

A Blue Team nem feltétlenül azonos a SOC-kal. A SOC jellemzően a Blue Team egyik központi része, de a tágabb védekező csapat további szakembereket is magában foglalhat, például:

- biztonsági mérnököket
- incidenskezelőket
- malware-elemzőket
- digitális forenzikus szakértőket
- threat intelligence elemzőket
- cloud security szakembereket
- sebezhetőségkezelési szakértőket

### Blue Team és Red Team

A **Red Team** támadói módszereket alkalmaz engedélyezett környezetben, hogy tesztelje a szervezet védelmét. A **Blue Team** feladata ezeknek a tevékenységeknek az észlelése, megakadályozása és kezelése.

A két csapat célja végső soron közös: a szervezet biztonságának javítása.

| Blue Team | Red Team |
|---|---|
| Védekezésre összpontosít | Támadói módszereket szimulál |
| Riasztásokat és naplókat elemez | Gyenge pontokat keres és használ ki |
| Incidenseket kezel | A védelmi kontrollokat teszteli |
| Detektálásokat fejleszt | A detektálások megkerülését próbálja ki |
| Folyamatos védelmi feladatokat végez | Általában meghatározott tesztidőszakban dolgozik |

A két oldal együttműködését gyakran **Purple Teamingnek** nevezik.

---

## 4. A SOC-elemző feladatai

A SOC-elemző elsődleges feladata a biztonsági események vizsgálata és a szervezetet fenyegető tevékenységek felismerése.

A napi munka szervezetenként eltérhet, de jellemzően a következő tevékenységeket foglalja magában:

### 4.1 Riasztások triázsa

A **triázs** során az elemző gyorsan felméri

- mi váltotta ki a riasztást
- melyik rendszer vagy felhasználó érintett
- mennyire sürgős az esemény
- valódi fenyegetésről lehet-e szó
- szükséges-e további vizsgálat vagy eszkaláció

### 4.2 Naplók és telemetria elemzése

A SOC-elemző többféle adatforrást vizsgálhat:

- Windows Event Log
- Linux rendszer- és hitelesítési naplók
- tűzfalnaplók
- DNS-naplók
- proxy- és webes naplók
- e-mail-biztonsági események
- EDR-telemetria
- felhőalapú auditnaplók
- IDS- vagy IPS-riasztások
- SIEM-korrelációk

### 4.3 Kontextusgyűjtés

Egy önmagában gyanús esemény nem mindig bizonyít támadást. Az elemző ezért további kontextust gyűjt, például:

- az érintett felhasználó szerepköre
- az eszköz típusa és fontossága
- az IP-cím földrajzi vagy szervezeti háttere
- a folyamat szülő-gyermek kapcsolata
- korábbi hasonló események
- ismert fenyegetettségi információk
- az esemény időpontja és gyakorisága

### 4.4 Riasztások minősítése

A vizsgálat eredménye lehet például:

- **True Positive:** valódi káros vagy engedély nélküli tevékenység
- **Benign True Positive:** a szabály helyesen észlelt egy eseményt, de az engedélyezett volt
- **False Positive:** a riasztás tévesen jelzett fenyegetést
- **False Negative:** káros tevékenység történt, de a rendszer nem riasztott

### 4.5 Eszkaláció

Az elemző magasabb szintre továbbítja az ügyet, ha:

- az esemény valószínűleg valódi incidens
- kritikus rendszer érintett
- több eszköz vagy felhasználó kompromittálódhatott
- privilegizált fiók érintett
- adatvesztés vagy adatszivárgás gyanúja merül fel
- az eset meghaladja a saját jogosultságát vagy szakértelmét
- azonnali korlátozó intézkedés szükséges

### 4.6 Dokumentáció

A jó SOC-dokumentáció rövid, pontos és ellenőrizhető. Tartalmazza:

- a riasztás vagy esemény időpontját
- az érintett eszközöket és fiókokat
- a releváns indikátorokat
- az elvégzett vizsgálati lépéseket
- a megállapításokat
- a bizonyítékokat
- a kockázati besorolást
- a végrehajtott vagy javasolt intézkedéseket

A CISA Cyber Defense Analyst szerepleírása szerint a védelmi elemző különböző eszközökből (például IDS-riasztásokból, tűzfalakból és hálózati naplókból) származó adatokat elemez a fenyegetések mérséklése érdekében.

---

## 5. Tier 1, Tier 2 és Tier 3 szerepkörök

A legtöbb SOC többszintű működési modellt alkalmaz. A pontos elnevezések és feladatok szervezetenként eltérhetnek, ezért a Tier-modell nem tekinthető mindenhol azonos, kötelező szabványnak.

### Tier 1 — Első szintű elemző

A Tier 1 elemző rendszerint a riasztások első vizsgálója.

Tipikus feladatai:

- riasztások fogadása és priorizálása
- alapvető triázs
- előre meghatározott playbookok követése
- alapadatok és bizonyítékok összegyűjtése
- false positive események lezárása
- gyanús ügyek eszkalálása
- jegyek és vizsgálati megjegyzések dokumentálása

A Tier 1 szerepkörben különösen fontos:

- a részletekre való odafigyelés
- az eljárások pontos követése
- a világos dokumentáció
- az alapvető hálózati és operációs rendszer ismeret
- a megfelelő időben történő eszkaláció

### Tier 2 — Incidensvizsgáló

A Tier 2 elemző összetettebb vizsgálatokat végez.

Tipikus feladatai:

- eszkalált riasztások mélyebb elemzése
- több adatforrás korrelálása
- támadási idővonal összeállítása
- érintett eszközök és fiókok azonosítása
- incidens súlyosságának meghatározása
- threat intelligence és MITRE ATT&CK alkalmazása
- Tier 1 elemzők támogatása

### Tier 3 — Senior elemző vagy threat hunter

A Tier 3 szerepkör a legösszetettebb technikai vizsgálatokat foglalhatja magában.

Tipikus feladatai:

- fejlett incidensek vizsgálata
- proaktív threat hunting
- malware- és forenzikus elemzés támogatása
- új detektálások fejlesztése
- támadói technikák modellezése
- észlelési hiányosságok feltárása
- automatizálási és fejlesztési javaslatok kidolgozása
- szakmai mentorálás

### További SOC-szerepkörök

Egy érettebb SOC-ban további szerepkörök is megjelenhetnek:

- SOC Manager
- SOC Engineer
- Detection Engineer
- Incident Responder
- Threat Intelligence Analyst
- Threat Hunter
- Digital Forensics Analyst
- Malware Analyst
- Security Automation Engineer

---

## 6. NOC és SOC közötti különbség

A **Network Operations Center** (NOC) és a **Security Operations Center** (SOC) egyaránt folyamatos megfigyelési feladatokat végezhet, de eltérő célokkal.

| Szempont | NOC | SOC |
|---|---|---|
| Elsődleges cél | Rendelkezésre állás és teljesítmény | Biztonság és fenyegetések kezelése |
| Fő kérdés | Működik-e megfelelően a rendszer? | Biztonságos-e a rendszer? |
| Tipikus esemény | Szolgáltatáskiesés, magas terhelés | Gyanús bejelentkezés, malware, adatlopás |
| Fő adatforrás | Teljesítmény- és rendelkezésreállási adatok | Biztonsági naplók és riasztások |
| Tipikus válasz | Hibaelhárítás és szolgáltatás-helyreállítás | Vizsgálat, korlátozás és incidenskezelés |
| Kiemelt mérőszám | Uptime, késleltetés, kapacitás | Észlelési és reagálási idő, incidensek |

A két központ gyakran együttműködik. Egy szolgáltatáskiesés mögött lehet műszaki hiba, de akár kibertámadás is. A megfelelő besoroláshoz mindkét csapat információira szükség lehet.

---

## 7. Egy biztonsági riasztás tipikus életútja

Egy riasztás kezelése általában a következő lépésekből áll:

```text
Adatforrás
    ↓
Detektálási szabály
    ↓
Riasztás
    ↓
Triázs
    ↓
Kontextusgyűjtés és vizsgálat
    ↓
Minősítés
    ↓
Lezárás vagy eszkaláció
    ↓
Incidenskezelés
    ↓
Tanulságok és fejlesztés
```

### 7.1 Adat keletkezése

Egy végpont, szerver, tűzfal, felhőszolgáltatás vagy más rendszer eseményt naplóz.

### 7.2 Detektálás

Egy biztonsági szabály, analitikai modell vagy eszköz felismeri a gyanús mintát.

### 7.3 Riasztás létrehozása

A SIEM, EDR vagy más platform riasztást generál.

### 7.4 Triázs

A Tier 1 elemző ellenőrzi a riasztás alapadatait és prioritását.

### 7.5 Vizsgálat

Az elemző további naplókat, felhasználói adatokat, folyamatokat, hálózati kapcsolatokat és threat intelligence információkat vizsgál.

### 7.6 Döntés

Az eseményt lezárják, további megfigyelésre jelölik vagy magasabb szintre eszkalálják.

### 7.7 Reagálás

Valódi incidens esetén a szervezet korlátozza a károkat, megszünteti a támadói hozzáférést és helyreállítja a működést.

### 7.8 Fejlesztés

A csapat értékeli, hogy:

- megfelelően működött-e a detektálás;
- elegendő adat állt-e rendelkezésre;
- javítani kell-e a szabályokon;
- szükséges-e új playbook vagy kontroll;
- milyen tanulságokat kell megosztani.

---

## 8. A jó SOC-elemző készségei

### Technikai készségek

- hálózati alapismeretek
- Windows- és Linux-ismeretek
- naplóelemzés
- SIEM-használat
- végpontbiztonsági alapok
- hitelesítési folyamatok ismeretek
- alapvető scripting
- MITRE ATT&CK használata
- incidenskezelési alapok

### Nem technikai készségek

- elemző gondolkodás
- kíváncsiság
- pontos dokumentáció
- világos kommunikáció
- időgazdálkodás
- prioritások kezelése
- csapatmunka
- nyomás alatti döntéshozatal
- folyamatos tanulási hajlandóság

Egy jó elemző nem pusztán eszközöket kezel. Kérdéseket tesz fel, összefüggéseket keres, ellenőrzi a feltételezéseit, és bizonyítékokra alapozza a döntéseit.

---

## 9. Példa: gyanús bejelentkezési riasztás

Tegyük fel, hogy a SIEM rövid időn belül sok sikertelen, majd egy sikeres bejelentkezést jelez ugyanahhoz a felhasználóhoz.

Az elemző a következő kérdéseket teheti fel:

1. Melyik felhasználói fiók érintett?
2. Honnan érkeztek a bejelentkezési kísérletek?
3. Ugyanaz az IP-cím szerepel minden eseménynél?
4. Szokásos helyről és időpontban történt a sikeres belépés?
5. Használtak többfaktoros hitelesítést?
6. Történt-e jelszóváltoztatás?
7. Követte-e a bejelentkezést szokatlan tevékenység?
8. Érintett-e privilegizált fiók?
9. Vannak-e hasonló események más felhasználóknál?
10. Szükséges-e a fiók ideiglenes letiltása vagy további eszkaláció?

Ez a példa mutatja, hogy egyetlen riasztás önmagában ritkán elegendő. A SOC-elemző feladata a megfelelő kontextus összegyűjtése.

---

## 10. Összefoglalás

A SOC egy szervezet biztonsági megfigyelési, elemzési és reagálási képességeinek központi eleme. A SOC-elemzők különböző adatforrásokból származó eseményeket vizsgálnak, riasztásokat minősítenek, incidenseket eszkalálnak és dokumentálnak.

A Tier 1, Tier 2 és Tier 3 modell segíthet a feladatok elosztásában, de a tényleges szerepkörök szervezetenként eltérnek. A hatékony SOC nem kizárólag technológiai eszközökre épül, hanem megfelelő emberekre, folyamatokra, együttműködésre és folyamatos fejlesztésre is.

---

## 11. Ellenőrző kérdések

1. Mit jelent a SOC rövidítés?
2. Mi a SOC három alapvető feladata?
3. Mi a különbség a SOC és a tágabb Blue Team között?
4. Mi a különbség a Blue Team és a Red Team között?
5. Mit jelent a riasztások triázsa?
6. Mi a false positive?
7. Mikor kell egy riasztást eszkalálni?
8. Mi a Tier 1 elemző tipikus feladata?
9. Miben különbözik a Tier 2 szerepkör a Tier 1-től?
10. Milyen feladatokat végezhet egy Tier 3 elemző?
11. Mi a legfontosabb különbség a NOC és a SOC között?
12. Miért fontos a pontos dokumentáció?
13. Milyen adatforrásokat használhat egy SOC-elemző?
14. Mi történik egy riasztás lezárása vagy eszkalációja után?
15. Mely technikai és nem technikai készségek fontosak egy SOC-elemző számára?

---

## 12. Rövid gyakorlófeladat

Egy felhasználó munkaidőn kívül egy korábban nem látott országból jelentkezik be a vállalati felhőszolgáltatásba. A belépést több sikertelen próbálkozás előzte meg.

Készíts rövid triázsjegyzetet az alábbi szerkezetben:

```text
Riasztás:
Érintett felhasználó:
Érintett rendszer:
Időpont:
Forrás IP-cím:
Első megállapítás:
További ellenőrzések:
Kockázati szint:
Javasolt intézkedés:
Eszkaláció szükséges: igen / nem
Indoklás:
```

A feladat célja nem a végleges incidensminősítés, hanem a strukturált elemzői gondolkodás gyakorlása.

---

## Források

1. National Institute of Standards and Technology: **Security Operations Center — CSRC Glossary**  
   https://csrc.nist.gov/glossary/term/Security_Operations_Center

2. National Institute of Standards and Technology: **The NIST Cybersecurity Framework (CSF) 2.0**  
   https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20

3. National Institute of Standards and Technology: **SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

4. Cybersecurity and Infrastructure Security Agency: **Cyber Defense Analyst**  
   https://www.cisa.gov/careers/work-rolescyber-defense-analyst

5. MITRE ATT&CK: **Get Started with ATT&CK**  
   https://attack.mitre.org/resources/

---

[← Vissza a magyar tartalomjegyzékhez](../../README.hu.md) | [Következő fejezet →](02-how-a-soc-works.md)
