# 07 — SIEM-alapismeretek

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/07-siem-fundamentals.md)

## Bevezetés

Az előző fejezetben azt néztük meg, hogyan lehet naplóbejegyzéseket értelmezni. Egy nagyobb szervezetben azonban rengeteg rendszer készít naplókat. Ezeket kézzel, egyenként átnézni szinte lehetetlen.

Ebben segít a SIEM.

A SIEM a *Security Information and Event Management* rövidítése. Magyarul nagyjából biztonsági információ- és eseménykezelő rendszernek fordítható.

Egyszerűen fogalmazva a SIEM összegyűjti a különböző rendszerek biztonsági adatait, kereshetővé teszi őket, és riasztást hozhat létre, ha gyanús mintát észlel.

## 1. Egyszerű hasonlat

A SIEM-et elképzelhetjük egy központi biztonsági irányítóasztalként.

Egy nagy épületben külön rendszer figyelheti:

- a bejárati kártyákat
- a kamerákat
- a tűzjelzőket
- a lifteket
- a riasztókat

Ha ezek mind külön működnek, nehéz észrevenni az összefüggéseket.

Ha azonban minden adat egy központi helyre érkezik, könnyebb felismerni például ezt a történetet:

1. valaki éjjel belépett az épületbe
2. olyan emeletre ment, ahol nem dolgozik
3. röviddel később kinyílt egy vészkijárat

A SIEM hasonló módon kapcsol össze informatikai eseményeket.

## 2. Milyen adatokat gyűjthet egy SIEM?

Egy SIEM sokféle forrásból fogadhat adatokat.

Például:

- Windows-naplók
- Linux-naplók
- tűzfalnaplók
- VPN-események
- DNS-lekérdezések
- felhőszolgáltatások naplói
- vírusvédelmi riasztások
- EDR-adatok
- e-mail-biztonsági események
- alkalmazásnaplók
- hitelesítési adatok

Nem minden szervezet gyűjt be minden adatot. A forrásokat a kockázatok, a költségek és a vizsgálati igények alapján választják ki.

## 3. Hogyan jut el az adat a SIEM-be?

A folyamat leegyszerűsítve így néz ki:

```text
Rendszer eseményt készít
        ↓
A napló továbbításra kerül
        ↓
A SIEM fogadja az adatot
        ↓
A mezőket feldolgozza
        ↓
Az adat kereshetővé válik
        ↓
Szabály vagy lekérdezés vizsgálhatja
```

Az adat többféle módon érkezhet:

- telepített ügynök segítségével
- hálózati továbbítással
- API-kapcsolaton keresztül
- felhőalapú csatlakozóval
- fájl importálásával

Az ügynök, angolul agent, egy kis program, amely adatokat gyűjt és továbbít a végpontról vagy szerverről.

## 4. Adatgyűjtés és feldolgozás

A különböző rendszerek eltérő formátumban készítik a naplókat.

A SIEM ezért gyakran:

1. fogadja az adatot
2. felismeri a formátumot
3. mezőkre bontja
4. egységesíti a mezőneveket
5. eltárolja az adatot

Például a következő mezők ugyanazt jelenthetik:

```text
src_ip
source_ip
client_ip
```

A SIEM ezeket egységesen kezelheti például `source_ip` néven.

Ezt normalizálásnak nevezzük.

## 5. Keresés a SIEM-ben

A SIEM egyik legfontosabb funkciója a keresés.

Egy elemző például ezt szeretné megtudni:

```text
Mely felhasználóknál történt
több mint 10 sikertelen bejelentkezés
az elmúlt egy órában?
```

Vagy:

```text
Mely számítógépek kapcsolódtak
a 203.0.113.50 IP-címhez?
```

A pontos lekérdezési nyelv SIEM-termékenként eltérhet.

Példák:

- Microsoft Sentinel KQL-t használ
- Splunk gyakran SPL-t használ
- Elastic környezetben KQL vagy EQL is előfordulhat

Kezdőként nem a lekérdezési nyelv teljes megtanulása a legfontosabb. Először azt kell világosan megfogalmazni, milyen kérdésre keresünk választ.

## 6. Mi az a detektálási szabály?

A detektálási szabály olyan feltétel, amely meghatározza, mikor hozzon létre a SIEM riasztást.

Egyszerű példa:

```text
Ha ugyanannál a felhasználónál
10 percen belül 20 sikertelen bejelentkezés történik,
hozz létre riasztást.
```

Egy szabály több feltételt is összekapcsolhat.

```text
Sok sikertelen bejelentkezés
ÉS
utána sikeres bejelentkezés
ÉS
ismeretlen külső IP-cím
```

Minél több feltételt használunk, annál pontosabb lehet a riasztás. Túl szigorú szabály esetén viszont valódi támadás maradhat észrevétlen.

## 7. Korreláció

A korreláció azt jelenti, hogy a SIEM több, különböző esemény között keres kapcsolatot.

Példa:

```text
VPN: sikeres külső bejelentkezés
Windows: PowerShell elindult
Tűzfal: kapcsolat ismeretlen szerverhez
Active Directory: új adminisztrátori fiók
```

Ezek külön rendszerek eseményei.

A SIEM egy közös idővonalon összekapcsolhatja őket.

A korreláció segít abban, hogy az elemző ne csak elszigetelt eseményeket lásson, hanem egy lehetséges támadási folyamatot is.

## 8. Esemény, riasztás és incidens

Ezt a három fogalmat könnyű összekeverni.

### Esemény

Valami történt egy rendszerben.

```text
Egy felhasználó bejelentkezett.
```

### Riasztás

Egy szabály vagy biztonsági eszköz az eseményt gyanúsnak találta.

```text
A felhasználó szokatlan országból jelentkezett be.
```

### Incidens

Egy vagy több riasztást a vizsgálat során valódi vagy valószínű biztonsági problémához kapcsoltak.

```text
A felhasználói fiókot valószínűleg megszerezték.
```

Nem minden eseményből lesz riasztás, és nem minden riasztásból lesz incidens.

## 9. Prioritás és súlyosság

A SIEM a riasztásokhoz gyakran súlyossági szintet rendel.

Például:

- Low
- Medium
- High
- Critical

A súlyosságot befolyásolhatja:

- az érintett rendszer fontossága
- a felhasználó jogosultsága
- az adat érzékenysége
- a detektálás megbízhatósága
- a kapcsolódó események száma
- a lehetséges üzleti hatás

Egy magas súlyosságú riasztás sem bizonyít automatikusan támadást. A címke abban segít, hogy az elemzők eldöntsék, mely ügyeket vizsgálják meg először.

## 10. Dashboardok

A dashboard egy áttekintő képernyő, amely grafikonokon és táblázatokban mutatja az adatokat.

Egy SOC-dashboard megjelenítheti:

- a riasztások számát
- a leggyakoribb riasztástípusokat
- a legtöbb hibás bejelentkezést
- a legaktívabb forrás IP-címeket
- a nyitott incidenseket
- a riasztások súlyosságát
- az adatforrások állapotát

A dashboard segít gyors képet kapni, de önmagában nem helyettesíti a részletes vizsgálatot.

## 11. Riasztási fáradtság

Ha egy SIEM túl sok riasztást készít, az elemzők nehezen tudják mindet megfelelően átnézni.

Ezt alert fatigue-nak, magyarul riasztási fáradtságnak nevezik.

Okai lehetnek:

- túl érzékeny szabályok
- sok false positive
- rosszul beállított adatforrás
- ismétlődő, azonos riasztások
- hiányzó üzleti kontextus
- elavult szabályok

A megoldás része lehet:

- szabályhangolás
- kivételek óvatos használata
- duplikált riasztások összevonása
- kockázatalapú priorizálás
- rendszeres felülvizsgálat

A cél nem az, hogy minél több riasztás készüljön. A cél az, hogy a riasztások használhatóak legyenek.

## 12. Mi az a tuning?

A tuning a szabályok finomhangolását jelenti.

Példa:

Egy szabály minden PowerShell-indításra riaszt.

Ez túl sok riasztást okozhat, mert a rendszergazdák is rendszeresen használják a PowerShellt.

A szabály pontosítható:

```text
Riasztás akkor,
ha a PowerShell kódolt parancsot futtat,
internetről tölt le fájlt,
vagy Office-programból indul.
```

A tuning során figyelni kell arra, hogy a kivételek ne rejtsenek el valódi támadást.

## 13. SIEM és SOAR

A SIEM és a SOAR nem ugyanaz.

### SIEM

Főként:

- adatokat gyűjt
- keresést biztosít
- eseményeket kapcsol össze
- riasztásokat készít
- vizsgálatot támogat

### SOAR

A SOAR a *Security Orchestration, Automation and Response* rövidítése.

Főként:

- automatizálható lépéseket hajt végre
- playbookokat futtat
- más biztonsági eszközöket kapcsol össze
- válaszlépéseket gyorsít

Például a SIEM riasztást készít egy rosszindulatú IP-cím miatt, a SOAR pedig automatikusan lekérheti az IP reputációját és jegyet nyithat.

## 14. A SIEM korlátai

A SIEM hasznos, de nem old meg mindent.

Nem működik jól, ha:

- fontos naplók nem érkeznek be
- rossz az időszinkronizálás
- hibás a mezők feldolgozása
- túl rövid a megőrzési idő
- rosszul vannak beállítva a szabályok
- senki nem vizsgálja a riasztásokat
- nincs elegendő szakmai kontextus

Egyszerűen fogalmazva:

```text
A SIEM csak abból tud dolgozni,
amit valóban megkap.
```

## 15. Adatminőség

Nemcsak az adatok mennyisége fontos, hanem a minőségük is.

Probléma lehet, ha:

- hiányzik a felhasználónév
- hibás az időbélyeg
- nem látható a forrás IP-cím
- egy adatforrás napok óta nem küld eseményt
- a mezők rosszul vannak felismerve
- ugyanaz az esemény többször érkezik be

A SOC-nak ezért azt is figyelnie kell, hogy a naplóforrások megfelelően működnek-e.

## 16. Egyszerű SIEM-példa

Tegyük fel, hogy a SIEM a következő eseményeket látja:

```text
10:01 — 25 sikertelen bejelentkezés
10:04 — sikeres bejelentkezés
10:06 — PowerShell elindult
10:07 — kapcsolat rossz hírű IP-címhez
10:09 — új ütemezett feladat
```

A SIEM szabálya ezek alapján magas prioritású riasztást készít.

Az elemző ezután megvizsgálhatja:

1. melyik fiók érintett
2. honnan érkezett a kapcsolat
3. milyen PowerShell-parancs futott
4. melyik program kapcsolódott a külső címhez
5. mit indít az ütemezett feladat
6. van-e hasonló esemény másik gépen
7. felismeri-e a felhasználó a tevékenységet

A SIEM segít összegyűjteni az adatokat. A végső értékelést az elemző végzi.

## 17. Mit érdemes kezdőként megjegyezni?

- A SIEM több rendszer biztonsági adatait gyűjti központi helyre.
- Az adatokat kereshetővé és összehasonlíthatóvá teszi.
- A detektálási szabályok riasztásokat hozhatnak létre.
- A korreláció több esemény kapcsolatát vizsgálja.
- Nem minden riasztás jelent támadást.
- A túl sok riasztás riasztási fáradtságot okozhat.
- A tuning segít a szabályok javításában.
- A SIEM és a SOAR eltérő feladatot lát el.
- A SIEM csak a megfelelően begyűjtött adatokból tud dolgozni.
- Az emberi értékelés továbbra is szükséges.

## 18. Ellenőrző kérdések

1. Mit jelent a SIEM rövidítés?
2. Mi a SIEM alapvető feladata?
3. Milyen adatforrásokat gyűjthet?
4. Mi az az agent?
5. Mit jelent a normalizálás?
6. Mire használható egy SIEM-lekérdezés?
7. Mi az a detektálási szabály?
8. Mit jelent a korreláció?
9. Mi a különbség az esemény, a riasztás és az incidens között?
10. Mire szolgál a dashboard?
11. Mit jelent az alert fatigue?
12. Mi az a tuning?
13. Mi a különbség a SIEM és a SOAR között?
14. Miért fontos az adatminőség?
15. Miért nem helyettesíti a SIEM az elemzőt?

## Források

1. Microsoft Learn  
   **What is Microsoft Sentinel SIEM?**  
   https://learn.microsoft.com/en-us/azure/sentinel/overview

2. Microsoft Learn  
   **Design solutions for security operations**  
   https://learn.microsoft.com/en-us/training/modules/design-solutions-security-operations/

3. Cybersecurity and Infrastructure Security Agency  
   **Use Logging on Business Systems**  
   https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

4. Cybersecurity and Infrastructure Security Agency  
   **Enhanced Visibility and Hardening Guidance for Communications Infrastructure**  
   https://www.cisa.gov/resources-tools/resources/enhanced-visibility-and-hardening-guidance-communications-infrastructure

5. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](06-log-analysis.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](08-cyber-threat-intelligence.md)
