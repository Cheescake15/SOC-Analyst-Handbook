# 02 — Hogyan működik egy SOC?

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/02-how-a-soc-works.md)

## Bevezetés

Egy SOC működését könnyű úgy elképzelni, mint egy helyiséget tele monitorokkal, ahol elemzők folyamatosan támadásokat figyelnek. A valóság ennél összetettebb. Egy jól működő Security Operations Center nem pusztán technológiai eszközök gyűjteménye. Emberek, folyamatok és technológiák összehangolt rendszere.

A SOC célja nem az, hogy minden riasztást incidensnek tekintsen. A feladata az, hogy a nagy mennyiségű biztonsági eseményből gyorsan kiválassza azokat, amelyek valódi kockázatot jelenthetnek, majd megfelelő módon reagáljon rájuk.

## 1. A SOC három alapvető eleme

A legtöbb SOC működése három pillérre épül:

- emberek
- folyamatok
- technológia

Egyik sem működik jól a másik kettő nélkül.

### Emberek

Az elemzők értelmezik a riasztásokat, összekapcsolják a különböző forrásokból származó adatokat, döntéseket hoznak és dokumentálják a vizsgálatot.

A SOC-ban dolgozhatnak:

- Tier 1 elemzők
- Tier 2 incidensvizsgálók
- senior elemzők
- threat hunterek
- detection engineerek
- incidenskezelők
- SOC mérnökök
- SOC menedzserek

Egy kisebb szervezetben ugyanaz a személy több feladatot is elláthat. Egy nagyobb vállalatnál ezek külön szerepkörök lehetnek.

### Folyamatok

A folyamatok határozzák meg, hogy a csapat mit tegyen egy adott helyzetben.

Ide tartozhat:

- a riasztások priorizálása
- az eszkaláció szabályai
- a bizonyítékgyűjtés módja
- a jegykezelés
- a műszakátadás
- a vezetői értesítés
- a containment engedélyezése

Jó folyamatok nélkül két elemző ugyanarra a riasztásra teljesen eltérő módon reagálhat.

### Technológia

A technológia gyűjti, feldolgozza és megjeleníti a biztonsági adatokat.

Gyakori SOC-eszközök:

- SIEM
- EDR vagy XDR
- IDS és IPS
- tűzfal
- e-mail-biztonsági rendszer
- vulnerability management platform
- threat intelligence platform
- SOAR
- jegykezelő rendszer
- felhőalapú biztonsági szolgáltatások

Az eszközök segítik az elemzőt, de nem helyettesítik a szakmai döntést.

## 2. Honnan érkeznek az adatok?

A SOC többféle adatforrást használ. Ezek együttesen adnak képet arról, hogy mi történik a szervezet rendszerében.

Gyakori adatforrások:

- Windows Event Log
- Linux rendszer- és hitelesítési naplók
- tűzfalnaplók
- DNS-naplók
- proxy- és webes naplók
- VPN-naplók
- Active Directory események
- végponti telemetria
- e-mail-biztonsági események
- felhőszolgáltatások auditnaplói
- alkalmazásnaplók
- hálózati forgalmi adatok

### Példa

Egyetlen sikertelen bejelentkezés önmagában nem feltétlenül gyanús. Ha azonban ugyanarról az IP-címről rövid idő alatt több száz sikertelen próbálkozás történik, majd sikeres belépés következik, az már vizsgálatot igényelhet.

A döntéshez az elemző több forrást kapcsolhat össze:

- hitelesítési naplók
- VPN-adatok
- IP-reputáció
- felhasználói előzmények
- végponti aktivitás
- többfaktoros hitelesítési események

## 3. Hogyan lesz egy eseményből riasztás?

A rendszerek folyamatosan eseményeket generálnak. Ezek nagy része normál működéshez kapcsolódik.

Egy detektálási szabály vagy analitikai modell akkor hoz létre riasztást, ha egy esemény vagy eseménysorozat megfelel egy előre meghatározott feltételnek.

```text
Ha egy felhasználónál 10 percen belül
legalább 20 sikertelen bejelentkezés történik,
majd sikeres bejelentkezés következik,
hozz létre magas prioritású riasztást.
```

Ez még nem bizonyítja, hogy támadás történt. A riasztás csak azt jelzi, hogy az esemény további vizsgálatot igényel.

## 4. A riasztás életútja

```text
Adat keletkezik
      ↓
A rendszer felismer egy mintát
      ↓
Riasztás jön létre
      ↓
Tier 1 triázs
      ↓
Kontextusgyűjtés
      ↓
Minősítés
      ↓
Lezárás vagy eszkaláció
      ↓
Incidenskezelés
      ↓
Utólagos értékelés
```

### Triázs

A triázs célja annak gyors eldöntése, hogy:

- van-e valódi biztonsági kockázat
- mennyire sürgős az ügy
- szükséges-e mélyebb vizsgálat
- kell-e azonnali intézkedés
- tovább kell-e adni más elemzőnek

A triázs nem teljes incidensvizsgálat. Inkább gyors és strukturált első értékelés.

### Kontextusgyűjtés

Az elemző további adatokat keres.

Például:

- ismert-e az IP-cím
- megszokott-e a felhasználó helye
- milyen folyamat indult el
- mi volt a szülőfolyamat
- történt-e fájlletöltés
- volt-e más kapcsolódó riasztás
- érintett-e privilegizált fiók
- van-e hasonló aktivitás más eszközökön

### Minősítés

A vizsgálat végén a riasztás lehet:

- true positive
- benign true positive
- false positive
- információs esemény
- további vizsgálatot igénylő ügy

## 5. Prioritás és súlyosság

Nem minden riasztás egyformán fontos.

A prioritás meghatározásakor több szempontot kell figyelembe venni:

- milyen eszköz érintett
- mennyire kritikus az üzleti folyamat
- milyen jogosultsággal rendelkezik a felhasználó
- mekkora lehet a hatás
- mennyire megbízható a detektálás
- aktív-e még a fenyegetés
- érintett-e érzékeny adat
- hány rendszerre terjed ki az esemény

### Példa

Egy sikertelen bejelentkezés egy tesztfióknál alacsony prioritású lehet.

Ugyanez a tevékenység egy rendszergazdai fióknál, külföldi IP-címről, munkaidőn kívül már jóval magasabb prioritást kaphat.

## 6. Playbookok és runbookok

A SOC gyakran előre meghatározott eljárásokat használ.

### Playbook

A playbook egy adott eseménytípus kezelésének magasabb szintű menete.

Egy phishing playbook tartalmazhatja:

1. az e-mail fejlécének ellenőrzését
2. a hivatkozások és mellékletek vizsgálatát
3. a címzettek azonosítását
4. a kattintások ellenőrzését
5. az üzenet eltávolítását
6. az érintett fiókok vizsgálatát
7. a dokumentáció elkészítését

### Runbook

A runbook részletesebb technikai végrehajtási utasítás.

Leírhatja:

- melyik SIEM-lekérdezést kell futtatni
- melyik EDR-funkcióval lehet elkülöníteni a gépet
- milyen mezőket kell kitölteni a jegyben
- melyik csapatot kell értesíteni

A lényeg az, hogy az elemző követhető és ismételhető eljárás alapján dolgozzon.

## 7. Eszkaláció

Az eszkaláció nem azt jelenti, hogy az elemző nem tudta megoldani a feladatot. A jó elemző felismeri, mikor kell más szakembert vagy döntéshozót bevonni.

### Technikai eszkaláció

Például:

- malware-elemző
- incidenskezelő
- digitális forenzikus szakértő
- cloud security szakember
- identity specialist

### Vezetői eszkaláció

Vezetői bevonásra lehet szükség, ha:

- jelentős üzleti hatás várható
- szabályozási kötelezettség merül fel
- személyes adat érintett
- kommunikációs döntés szükséges
- külső hatóság vagy partner értesítése válhat szükségessé

## 8. Együttműködés más csapatokkal

A SOC nem működhet elszigetelten.

Gyakori együttműködő partnerek:

- IT üzemeltetés
- Identity and Access Management
- jogi osztály
- adatvédelmi csapat
- HR
- kommunikáció
- üzleti területek
- vezetőség

A SOC feladata, hogy világosan összefoglalja:

- mi történt
- mi érintett
- mekkora a kockázat
- milyen intézkedés történt
- milyen döntés szükséges

## 9. Műszakátadás

A folyamatosan működő SOC-ban az egyik műszak átadja a nyitott ügyeket a következőnek.

Egy jó műszakátadás tartalmazza:

- a nyitott riasztásokat
- az aktív incidenseket
- az eddig elvégzett lépéseket
- a még szükséges feladatokat
- a fontos határidőket
- az érintett kapcsolattartókat
- az ismert technikai problémákat
- az ideiglenesen módosított szabályokat

### Rossz átadás

```text
Nézzetek rá a gyanús PowerShell-riasztásra.
```

### Jobb átadás

```text
A WS-104 végponton gyanús, kódolt PowerShell-parancs futott 22:14-kor.
A felhasználó szerint nem végzett adminisztrációs feladatot.
Az EDR-vizsgálat elindult.
A végpont még nincs elkülönítve.
Következő lépés: process tree és hálózati kapcsolatok ellenőrzése.
Jegy: INC-2481.
```

## 10. Automatizálás a SOC-ban

A SOAR és más automatizálási eszközök ismétlődő feladatokat hajthatnak végre.

Például:

- IP-cím reputációjának lekérdezése
- fájlhash ellenőrzése
- felhasználói adatok összegyűjtése
- jegy automatikus létrehozása
- e-mail karanténba helyezése
- végpont elkülönítése
- értesítés küldése

Az automatizálás előnyei:

- gyorsabb válaszadás
- következetes végrehajtás
- kevesebb manuális munka
- kisebb hibalehetőség

A nagy hatású műveleteknél gyakran szükséges emberi jóváhagyás.

## 11. Hogyan mérhető a SOC teljesítménye?

Gyakori mutatók:

- Mean Time to Detect
- Mean Time to Acknowledge
- Mean Time to Respond
- Mean Time to Contain
- False Positive Rate
- Escalation Rate
- Alert Volume

Ezeket a számokat óvatosan kell értelmezni. A gyors lezárás önmagában nem jelent jó minőségű vizsgálatot.

## 12. Gyakorlati példa

Egy pénzügyi osztályon dolgozó felhasználó fiókja rövid idő alatt több országból jelentkezik be.

Az elemző megvizsgálja:

- az IP-címeket
- a bejelentkezések időpontját
- az eszközazonosítókat
- a többfaktoros hitelesítési eseményeket
- a felhasználó korábbi viselkedését
- a bejelentkezés utáni aktivitást

Lehetséges magyarázatok:

- VPN használata
- utazás
- megosztott fiók
- hibás helymeghatározás
- ellopott hitelesítő adatok
- session token eltulajdonítása

Ha a felhasználó nem ismeri fel a tevékenységet, és a bejelentkezést szokatlan fájlletöltés vagy postafiókszabály létrehozása követi, az ügyet eszkalálni kell.

## 13. Összefoglalás

A SOC működésének alapja az emberek, folyamatok és technológiák összehangolása.

A riasztások kezelése nem merül ki abban, hogy az elemző megnyom egy lezárás gombot. Meg kell értenie az esemény kontextusát, értékelnie kell a kockázatot, dokumentálnia kell a vizsgálatot, és szükség esetén eszkalálnia kell az ügyet.

## 14. Ellenőrző kérdések

1. Mi a SOC három alapvető pillére?
2. Miért nem elegendő önmagában egy SIEM-rendszer?
3. Mi a különbség egy esemény és egy riasztás között?
4. Mit jelent a triázs?
5. Milyen tényezők befolyásolják egy riasztás prioritását?
6. Mi a különbség a playbook és a runbook között?
7. Mikor szükséges technikai eszkaláció?
8. Milyen szervezeti egységekkel működhet együtt a SOC?
9. Mit kell tartalmaznia egy jó műszakátadásnak?
10. Milyen előnyei és kockázatai vannak az automatizálásnak?

## Források

1. NIST SP 800-61 Rev. 3  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. NIST Cybersecurity Framework 2.0  
   https://www.nist.gov/cyberframework

3. CISA Cybersecurity Incident and Vulnerability Response Playbooks  
   https://www.cisa.gov/news-events/news/cisa-releases-updated-cybersecurity-incident-and-vulnerability-response-playbooks

4. MITRE ATT&CK Data Sources  
   https://attack.mitre.org/datasources/

---

[← Előző fejezet](01-introduction.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](03-network-fundamentals.md)
