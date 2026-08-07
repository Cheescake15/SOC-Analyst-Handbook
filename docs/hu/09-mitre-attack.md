# 09 — MITRE ATT&CK

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/09-mitre-attack.md)

## Bevezetés

Az előző fejezetben megjelent a TTP fogalma, vagyis a támadók taktikái, technikái és eljárásai.

A MITRE ATT&CK egy olyan nyilvános tudásbázis, amely ezeket a támadói viselkedéseket rendszerezi.

Az ATT&CK neve az *Adversarial Tactics, Techniques, and Common Knowledge* kifejezésből származik.

Egyszerűen fogalmazva a MITRE ATT&CK abban segít, hogy közös nyelven tudjunk beszélni arról, hogyan viselkednek a támadók egy kibertámadás során.

## 1. Miért jött létre?

A MITRE az ATT&CK-ot azért kezdték fejleszteni, hogy valós támadásokból megfigyelt viselkedéseket rendszerezzen.

A tudásbázis nem azt írja le, hogyan kell támadást végrehajtani. Azt mutatja be, milyen célokat próbálnak elérni a támadók, és milyen módszereket figyeltek meg a valós életben.

A MITRE hivatalos leírása szerint az ATT&CK valós megfigyelésekre épülő tudásbázis.

## 2. Taktika, technika, altechnika és eljárás

Ez a négy fogalom az ATT&CK alapja.

### Taktika

A taktika azt mutatja meg, **miért** hajt végre valamit a támadó.

Például:

```text
Initial Access
```

Ez azt jelenti, hogy a támadó megpróbál bejutni a célrendszerbe.

Másik példa:

```text
Credential Access
```

Itt a támadó felhasználói azonosítókat vagy jelszavakat próbál megszerezni.

### Technika

A technika azt mutatja meg, **hogyan** próbálja elérni a támadó a célját.

Például az Initial Access taktikán belül egy lehetséges módszer:

```text
Phishing
```

### Altechnika

Az altechnika egy technika pontosabb változata.

Például a phishing történhet:

- rosszindulatú csatolmánnyal
- rosszindulatú linkkel
- szolgáltatáson keresztül

### Eljárás

Az eljárás azt írja le, hogy egy konkrét támadó vagy támadócsoport hogyan alkalmazta az adott technikát a gyakorlatban.

Egyszerűen:

```text
Taktika = Mi a cél?
Technika = Hogyan próbálja elérni?
Altechnika = Pontosan milyen módon?
Eljárás = Egy valódi támadó hogyan csinálta?
```

## 3. Mi az ATT&CK Matrix?

A MITRE ATT&CK legismertebb része a mátrix.

A mátrix oszlopai taktikákat, a hozzájuk tartozó elemek pedig technikákat mutatnak.

Ez első látásra bonyolultnak tűnhet. Nem szükséges mindent megjegyezni.

A mátrix inkább egy térkép.

Segít megkeresni, hogy egy megfigyelt támadói viselkedés milyen célhoz kapcsolódhat.

## 4. ATT&CK területek

A MITRE ATT&CK több technológiai területet kezel.

A legfontosabbak:

- Enterprise
- Mobile
- ICS

### Enterprise

Vállalati informatikai környezeteket és felhőtechnológiákat fed le.

Ez a SOC-elemzők számára általában a legfontosabb rész.

### Mobile

Mobil eszközök elleni támadói viselkedéseket tartalmaz.

### ICS

Az ipari vezérlőrendszerekhez kapcsolódó támadási módszereket rendszerezi.

Az ATT&CK folyamatosan változik, ezért mindig az aktuális online verziót érdemes használni.

## 5. Néhány fontos Enterprise taktika

A teljes listát nem szükséges fejből megtanulni.

Kezdőként inkább a logikát érdemes megérteni.

### Reconnaissance

A támadó információt gyűjt a célpontról.

Például:

- alkalmazottak keresése
- domainek feltérképezése
- nyilvános rendszerek azonosítása

### Initial Access

A támadó megpróbál bejutni.

Például:

- phishing
- sérülékeny internetes szolgáltatás kihasználása
- érvényes fiók használata

### Execution

A támadó kódot vagy parancsot futtat.

Például:

```text
PowerShell
Command Prompt
script
```

### Persistence

A támadó megpróbálja megtartani a hozzáférését.

Például:

- új felhasználói fiók
- ütemezett feladat
- automatikusan induló program

### Privilege Escalation

A támadó magasabb jogosultságot próbál szerezni.

Például normál felhasználóból rendszergazdai hozzáférést.

### Credential Access

Felhasználónevekhez, jelszavakhoz vagy más hitelesítési adatokhoz próbál hozzáférni.

### Discovery

A támadó feltérképezi a rendszert.

Például:

- milyen gépek vannak
- milyen felhasználók léteznek
- milyen programok futnak
- milyen hálózati kapcsolatok vannak

### Lateral Movement

A támadó egyik gépről egy másikra próbál továbbjutni.

### Collection

A támadó összegyűjti azokat az adatokat, amelyeket később fel akar használni vagy el akar lopni.

### Command and Control

A kompromittált gép kapcsolatot tart a támadó infrastruktúrájával.

Ezt gyakran C2-nek vagy C&C-nek rövidítik.

### Exfiltration

A támadó adatokat visz ki a szervezetből.

### Impact

A támadó működési zavart vagy kárt próbál okozni.

Például:

- fájlok titkosítása
- adatok törlése
- szolgáltatás leállítása

## 6. Fontos, hogy ez nem mindig egyenes sorrend

Az ATT&CK mátrixot nem szabad úgy elképzelni, mint egy kötelező lépéssort.

A támadó:

- kihagyhat bizonyos taktikákat
- visszatérhet korábbi lépésekhez
- egyszerre több célt is követhet
- ugyanazt a technikát több célra használhatja

Ezért az ATT&CK nem egyszerű folyamatábra.

## 7. Technikák és azonosítók

Minden ATT&CK technikához tartozik egy azonosító.

Például:

```text
T1059
```

Ez a Command and Scripting Interpreter technika azonosítója.

Egy altechnika például így nézhet ki:

```text
T1059.001
```

Ez a PowerShellhez kapcsolódó altechnika.

Az azonosítók azért hasznosak, mert egyértelműen lehet velük hivatkozni egy technikára akkor is, ha a dokumentumok különböző nyelveken készülnek.

## 8. Egyszerű ATT&CK-példa

Tegyük fel, hogy egy vizsgálat során ezt látjuk:

```text
1. A felhasználó rosszindulatú e-mailt kap.
2. Megnyitja a benne lévő linket.
3. Egy program PowerShellt indít.
4. A támadó új ütemezett feladatot hoz létre.
5. A gép külső szerverhez kapcsolódik.
```

Ezt egyszerűsítve így lehet ATT&CK-höz kötni:

| Megfigyelés | Lehetséges ATT&CK-kategória |
|---|---|
| rosszindulatú e-mail | Initial Access |
| PowerShell futtatása | Execution |
| ütemezett feladat | Persistence |
| külső vezérlőszerver | Command and Control |

Ez nem teljes elemzés, de segít rendszerezni a történteket.

## 9. ATT&CK és Cyber Threat Intelligence

A CTI-jelentések gyakran ATT&CK technikákkal írják le egy támadócsoport viselkedését.

Például egy jelentés azt mondhatja, hogy egy csoport gyakran használ:

- phishinget
- PowerShellt
- hitelesítőadat-lopást
- távoli szolgáltatásokat
- ütemezett feladatokat

Ezek ATT&CK technikákhoz rendelhetők.

Így különböző jelentések könnyebben összehasonlíthatók.

## 10. ATT&CK és a SOC

Egy SOC többféleképpen használhatja az ATT&CK-öt.

### Riasztások címkézése

Egy SIEM-riasztáshoz hozzárendelhető a kapcsolódó ATT&CK technika.

### Detektálási hiányosságok keresése

Meg lehet vizsgálni, hogy mely fontos támadói technikákra van már detektálás, és melyekre nincs.

### Threat hunting

Egy ismert támadócsoport technikái alapján célzott keresés indítható.

### Incidens dokumentálása

Egy incidens lépéseit ATT&CK technikákkal lehet egységesen leírni.

### CTI feldolgozása

Egy külső jelentésben szereplő támadói viselkedés ATT&CK technikákhoz kapcsolható.

## 11. Mit jelent a detection coverage?

A **detection coverage** azt mutatja meg, hogy a szervezet milyen ATT&CK technikákhoz rendelkezik valamilyen észlelési képességgel.

Például:

```text
Phishing → van e-mail detektálás
PowerShell → van naplózás és szabály
Scheduled Task → részleges detektálás
Credential Dumping → nincs megfelelő adatforrás
```

Fontos, hogy egy zöldre jelölt technika nem jelenti azt, hogy minden lehetséges változatát biztosan észleljük.

A MITRE külön figyelmeztet arra, hogy az ATT&CK-öt nem szabad egyszerű kipipálandó ellenőrzőlistaként használni.

## 12. ATT&CK Navigator

Az **ATT&CK Navigator** egy webes eszköz a mátrix vizuális megjelenítésére.

Segítségével technikákat lehet például:

- kijelölni
- színezni
- pontozni
- megjegyzésekkel ellátni
- rétegekbe rendezni

Egy SOC például készíthet egy réteget:

```text
Mely technikákra van detektálásunk?
```

Egy másikat:

```text
Mely technikákat használja
a számunkra fontos támadócsoport?
```

A két réteg összevetése segíthet prioritásokat meghatározni.

## 13. ATT&CK Groupok és szoftverek

A MITRE ATT&CK nemcsak technikákat tartalmaz.

Találhatók benne:

- ismert támadócsoportok
- malware-ek
- támadói eszközök
- kampányok

Egy támadócsoport oldalán meg lehet nézni, hogy a nyilvános források alapján milyen technikákat használt.

Ezeket azonban nem szabad abszolút igazságként kezelni. A tudásbázis a nyilvánosan megfigyelt és dokumentált viselkedésekre épül.

## 14. Mi az a mapping?

A **mapping** azt jelenti, hogy egy megfigyelt tevékenységet ATT&CK technikához rendelünk.

Példa:

```text
A támadó PowerShellt futtatott.
```

Ezt a PowerShell altechnikához lehet kapcsolni.

A jó mappinghez nem elég egy kulcsszó.

Meg kell érteni:

- mit csinált a támadó
- mi volt a cél
- hogyan hajtotta végre
- van-e elég bizonyíték a besoroláshoz

## 15. Gyakori kezdő hiba

Kezdőként könnyű túl gyorsan ATT&CK technikát választani.

Példa:

```text
powershell.exe elindult
```

Ez önmagában csak azt mutatja, hogy PowerShell futott.

Nem tudjuk még:

- ki indította
- milyen paranccsal
- normális adminisztráció volt-e
- kapcsolódott-e támadáshoz

Az ATT&CK-mapping nem helyettesíti a vizsgálatot.

## 16. Az ATT&CK korlátai

A MITRE ATT&CK nagyon hasznos, de vannak korlátai.

### Nem tartalmaz minden létező támadói viselkedést

Csak dokumentált, megfigyelt technikákat tud tartalmazni.

Az NKI is beszámolt már olyan Linux malware-ről, amely olyan perzisztencia-módszert használt, amely akkor még nem szerepelt az ATT&CK-ben.

### Folyamatosan változik

Új technikák jelenhetnek meg, más elemek módosulhatnak.

### Nem kockázati pontszám

Az ATT&CK nem mondja meg automatikusan, hogy egy technika mennyire veszélyes a saját szervezet számára.

### Nem ellenőrzőlista

Nem az a cél, hogy minden mezőt zöldre színezzünk.

A szervezet számára releváns fenyegetésekre érdemes koncentrálni.

## 17. Mit érdemes kezdőként megjegyezni?

- A MITRE ATT&CK valós támadói viselkedéseket rendszerező tudásbázis.
- A taktika azt mutatja, mi a támadó célja.
- A technika azt mutatja, hogyan próbálja elérni.
- Az altechnika pontosabb viselkedést ír le.
- A technikáknak egyedi azonosítójuk van.
- A mátrix nem egy kötelező támadási sorrend.
- Az ATT&CK segíthet CTI-ben, detektálásban és threat huntingban.
- Az ATT&CK Navigator vizuálisan segít a technikák rendszerezésében.
- Egy technika lefedettsége nem jelent automatikusan teljes védelmet.
- Az ATT&CK nem helyettesíti az elemzői gondolkodást.

## 18. Ellenőrző kérdések

1. Mi a MITRE ATT&CK?
2. Mit jelent az ATT&CK rövidítés?
3. Mit jelent a taktika?
4. Mit jelent a technika?
5. Mi az altechnika?
6. Mi az eljárás?
7. Mire szolgál az ATT&CK Matrix?
8. Milyen fő technológiai területei vannak?
9. Mit jelent az Initial Access?
10. Mit jelent a Persistence?
11. Mit jelent a Lateral Movement?
12. Mire szolgálnak a technikaazonosítók?
13. Hogyan használhatja az ATT&CK-öt egy SOC?
14. Mire használható az ATT&CK Navigator?
15. Miért nem szabad az ATT&CK-öt egyszerű ellenőrzőlistaként használni?

## Források

1. MITRE ATT&CK  
   **Get Started**  
   https://attack.mitre.org/resources/

2. MITRE ATT&CK  
   **Enterprise Tactics**  
   https://attack.mitre.org/tactics/

3. MITRE ATT&CK  
   **Frequently Asked Questions**  
   https://attack.mitre.org/resources/faq/

4. MITRE ATT&CK  
   **ATT&CK Data & Tools**  
   https://attack.mitre.org/resources/attack-data-and-tools/

5. MITRE ATT&CK  
   **CTI Training**  
   https://attack.mitre.org/resources/training/cti/

6. Nemzeti Kiberbiztonsági Intézet  
   **Éves kiberbiztonsági jelentés**  
   https://nki.gov.hu/wp-content/uploads/2024/07/Eves-kiberbiztonsagi-jelentes.pdf

7. Nemzeti Kiberbiztonsági Intézet  
   **Androidos felhasználók után kémkedett egy applikáció**  
   https://nki.gov.hu/it-biztonsag/hirek/androidos-felhasznalok-utan-kemkedett-egy-applikacio/

8. Nemzeti Kiberbiztonsági Intézet  
   **A sedexp Linux malware éveken át észrevétlen maradt**  
   https://nki.gov.hu/it-biztonsag/hirek/a-sedexp-linux-malware-eveken-at-eszrevetlen-maradt/

---

[← Előző fejezet](08-cyber-threat-intelligence.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](10-incident-response.md)
