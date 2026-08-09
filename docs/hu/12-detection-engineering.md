# 12 — Detektálási szabályok tervezése

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/12-detection-engineering.md)

## Bevezetés

A korábbi fejezetekben már szó volt naplókról, SIEM-ről, MITRE ATT&CK-ről és incidenskezelésről.

Ezek után felmerül a kérdés:

```text
Hogyan lesz a sok naplóadatból valóban használható biztonsági riasztás?
```

Ezzel foglalkozik a detection engineering.

Magyarul nagyjából detektálási szabályok tervezésének és fejlesztésének nevezhetjük.

A cél olyan szabályok létrehozása, amelyek képesek felismerni a számunkra fontos támadói viselkedéseket, miközben nem generálnak kezelhetetlen mennyiségű téves riasztást.

## 1. Mi az a detektálás?

A detektálás azt jelenti, hogy egy biztonsági rendszer felismer egy előre meghatározott vagy szokatlan mintát.

Egyszerű példa:

```text
Egy felhasználó 5 perc alatt
30 sikertelen bejelentkezést produkál.
```

Ez lehet normális hiba is, de utalhat brute force támadásra.

A detektálási szabály azt mondhatja:

```text
Ha ugyanannál a felhasználónál
5 percen belül legalább 30
sikertelen bejelentkezés történik,
készíts riasztást.
```

## 2. Mi az a detection engineering?

A detection engineering több, mint egy keresőkifejezés megírása.

Általában magában foglalja:

1. a fenyegetés megértését
2. a szükséges naplóforrás kiválasztását
3. a detektálási logika megírását
4. a szabály tesztelését
5. a false positive-ok vizsgálatát
6. a szabály finomhangolását
7. a dokumentálást
8. a későbbi felülvizsgálatot

A jó detektálási szabály nemcsak működik, hanem érthető és karbantartható is.

## 3. Először a kérdést kell megfogalmazni

Egy detektálás készítése előtt érdemes egy egyszerű kérdést feltenni.

Például:

```text
Hogyan tudnánk észrevenni, ha valaki szokatlan módon PowerShellt használ?
```

Ezután lehet tovább bontani:

- milyen PowerShell eseményeket látunk
- mely mezők állnak rendelkezésre
- mi számít normálisnak
- mi számít szokatlannak
- milyen támadói viselkedést keresünk

Ha a kérdés nem világos, a szabály sem lesz igazán jó.

## 4. A megfelelő adatforrás

Detektálni csak azt lehet, amiről adat érkezik.

Például PowerShell-tevékenység vizsgálatához hasznos lehet:

- Windows Event Log
- PowerShell naplózás
- EDR telemetria
- folyamatindítási események
- hálózati naplók

Ha a szükséges napló nincs bekapcsolva, a szabály nem tud működni.

Egyszerűen:

```text
Nincs adat → nincs detektálás
```

Az NKI eseménynaplózási útmutatója is kiemeli, hogy a megfelelő naplóforrások és mezők megléte alapvető a fenyegetések felismeréséhez.

## 5. Milyen mezőkre lehet szükség?

Egy detektálás gyakran ilyen mezőket használ:

- időbélyeg
- felhasználónév
- számítógépnév
- forrás IP-cím
- cél IP-cím
- folyamatnév
- parancssor
- fájlnév
- hash
- eseményazonosító
- szolgáltatás neve

Példa:

```text
ProcessName = powershell.exe
CommandLine contains "-EncodedCommand"
```

Ez már egy egyszerű viselkedési feltétel.

## 6. Egyszerű és összetett szabályok

### Egyszerű szabály

Egyetlen eseményt keres.

```text
Új rendszergazdai fiók jött létre.
```

### Összetett szabály

Több eseményt kapcsol össze.

```text
Sok sikertelen belépés
ÉS
utána sikeres belépés
ÉS
rendszergazdai jogosultság használata
```

Az összetett szabály pontosabb lehet, de nehezebb tesztelni és karbantartani.

Kezdőként érdemes egyszerű szabályokkal kezdeni.

## 7. Küszöbértékek

Sok szabály valamilyen küszöbértéket használ.

Példa:

```text
10 sikertelen belépés 5 perc alatt
```

Itt:

```text
10 = küszöbérték
5 perc = időablak
```

Ha a küszöb túl alacsony, túl sok riasztás keletkezhet.

Ha túl magas, valódi támadás maradhat észrevétlen.

Ezért a szabályt tesztelni és hangolni kell.

## 8. Baseline

A baseline azt mutatja meg, mi számít normális működésnek.

Például:

- egy rendszergazda naponta használ PowerShellt
- egy pénzügyi felhasználó szinte soha
- egy szerver éjjel is rendszeresen kommunikál
- egy munkaállomás csak munkaidőben aktív

A normális viselkedés ismerete segít eldönteni, mi számít valóban szokatlannak.

## 9. False positive

A false positive olyan riasztás, amely gyanúsnak tűnik, de valójában normális tevékenység.

Példa:

```text
A szabály riaszt, mert
PowerShell futott.

Valójában az IT-csapat
jóváhagyott karbantartást végzett.
```

A túl sok false positive riasztási fáradtsághoz vezethet.

## 10. False negative

A **false negative** azt jelenti, hogy valódi rosszindulatú tevékenység történt, de a szabály nem riasztott.

Például:

```text
A szabály csak powershell.exe
fájlnévre keres.

A támadó más módon
indítja a PowerShellt.
```

A false negative gyakran nehezebben észlelhető, mint a false positive.

## 11. Tuning

A **tuning** a detektálás finomhangolását jelenti.

Példa:

Az első szabály:

```text
Riasztás minden PowerShell-indításra.
```

Ez valószínűleg túl sok találatot ad.

Finomított szabály:

```text
Riasztás akkor,
ha a PowerShell kódolt parancsot használ,
vagy Office-programból indul,
vagy internetes letöltést végez.
```

A tuning célja a zaj csökkentése úgy, hogy közben a fontos tevékenységek továbbra is láthatóak maradjanak.

## 12. Mit jelent a rule lifecycle?

A detektálási szabály nem egyszer készül el örökre.

Egy egyszerű életciklus:

```text
Ötlet
  ↓
Fejlesztés
  ↓
Teszt
  ↓
Élesítés
  ↓
Megfigyelés
  ↓
Tuning
  ↓
Felülvizsgálat
  ↓
Módosítás vagy kivezetés
```

A támadói módszerek és a vállalati rendszerek változnak, ezért a szabályokat is frissíteni kell.

## 13. Tesztelés

Egy új szabály élesítése előtt érdemes tesztelni.

Ellenőrizni kell:

- valóban megtalálja-e a keresett eseményt
- milyen gyakran fut
- mennyi adatot vizsgál
- hány találatot ad
- milyen false positive-ok jelennek meg
- elérhető-e minden szükséges mező

A tesztelés célja nem az, hogy a szabály minden körülmények között tökéletes legyen.

A cél az, hogy megértsük a működését és a korlátait.

## 14. Dokumentálás

Egy jó szabályhoz tartozik dokumentáció.

Érdemes leírni:

- a szabály neve
- mit keres
- miért fontos
- milyen adatforrást használ
- milyen mezőkre épül
- milyen ATT&CK technikához kapcsolódik
- milyen false positive-ok várhatók
- milyen súlyosságú
- mit vizsgáljon az elemző riasztás esetén

A Microsoft Sentinel szabályleírásai is külön kezelik például a szabály nevét, leírását, súlyosságát, ATT&CK-kapcsolatát és lekérdezési logikáját.

## 15. MITRE ATT&CK és detection engineering

A MITRE ATT&CK segíthet abban, hogy a detektálást ne véletlenszerűen építsük.

Például kiválasztunk egy technikát:

```text
T1059.001 — PowerShell
```

Majd megkérdezzük:

- milyen adatforrás látja
- milyen viselkedés lenne gyanús
- van-e már rá szabályunk
- milyen vakfoltjaink vannak

Az ATT&CK tehát segíthet a detektálási lefedettség átgondolásában.

## 16. Detection coverage

A **detection coverage** azt mutatja meg, milyen támadói viselkedésekre van használható detektálásunk.

Fontos azonban:

```text
Van szabály ≠ biztos detektálás
```

Egy szabály lehet:

- rosszul konfigurált
- nem megfelelő adatforrásra épülő
- túl szűk
- túl zajos
- elavult

Ezért a lefedettséget rendszeresen ellenőrizni kell.

## 17. Mi az a Sigma?

A **Sigma** egy nyílt formátum detektálási szabályok leírására.

Egyszerűen úgy lehet elképzelni, mint egy közös nyelvet a naplóalapú detektálásokhoz.

A Sigma-szabályok YAML formátumú szövegfájlok.

Egyetlen Sigma-szabály különböző SIEM-rendszerek lekérdezési nyelvére alakítható.

Például:

- Microsoft Sentinel
- Splunk
- Elasticsearch
- Grafana Loki

Ez azért hasznos, mert a detektálási ötlet kevésbé kötődik egyetlen gyártóhoz.

## 18. Egy egyszerű Sigma-példa

Nagyon leegyszerűsített példa:

```yaml
title: Multiple Failed Windows Logons

logsource:
  product: windows
  service: security

detection:
  selection:
    EventID: 4625
  condition: selection

level: medium
```

Ez a szabály a Windows 4625-ös eseményt keresi, amely sikertelen bejelentkezést jelez.

Ez még nem feltétlenül jó kész detektálás.

Egyetlen sikertelen belépés általában nem támadás.

Ezért egy valós szabály gyakran időablakot, darabszámot vagy más feltételt is használ.

## 19. A Sigma fő részei

Egy Sigma-szabályban gyakran szerepel:

### title

A szabály neve.

### logsource

Milyen naplót vizsgál.

### detection

Mit keres a szabály.

### condition

Mikor teljesül a feltétel.

### falsepositives

Milyen normális tevékenység válthatja ki.

### level

A feltételezett súlyosság.

### tags

Például MITRE ATT&CK technika.

A Sigma hivatalos dokumentációja szerint a legfontosabb részek a detection, logsource és a metaadatok.

## 20. Vendor-neutral gondolkodás

A detection engineeringben hasznos először a viselkedést megfogalmazni, és csak utána a konkrét lekérdezési nyelvet.

Nem így:

```text
Milyen KQL-lekérdezést írjak?
```

Hanem inkább:

```text
Milyen támadói viselkedést szeretnék felismerni?
Milyen adat bizonyítja ezt?
```

Ezután lehet KQL, SPL, Sigma vagy más formátumban megvalósítani.

## 21. Egyszerű detection engineering példa

### Cél

Gyanús PowerShell-használat felismerése.

### Feltételezés

Kódolt PowerShell-parancs ritka a normál felhasználóknál.

### Szükséges adat

```text
ProcessName
CommandLine
User
Computer
Timestamp
ParentProcess
```

### Első detektálási logika

```text
ProcessName = powershell.exe
ÉS
CommandLine tartalmazza: EncodedCommand
```

### Teszt

Megnézzük az elmúlt 30 napot.

### Eredmény

Találunk 250 eseményt.

Kiderül, hogy 230-at egy vállalati adminisztrációs eszköz generált.

### Tuning

A jóváhagyott adminisztrációs folyamatot pontos feltétellel kivesszük.

### Új eredmény

20 esemény marad.

Ezeket már reálisabb kézzel megvizsgálni.

## 22. Mit vizsgáljon az elemző riasztás után?

Egy szabály csak kiindulópont.

Például gyanús PowerShell-riasztásnál az elemző megnézheti:

1. melyik felhasználó futtatta
2. melyik gépen
3. milyen parancs futott
4. mi volt a parent process
5. történt-e külső kapcsolat
6. jött-e létre új fájl
7. van-e hasonló esemény más gépen
8. kapcsolódik-e ismert CTI-adathoz

A szabály értékét az is növeli, ha egyértelmű vizsgálati lépések tartoznak hozzá.

## 23. Detektálás karbantartása

Egy szabályt érdemes felülvizsgálni, ha:

- túl sok riasztást ad
- hónapok óta soha nem jelez
- megváltozott az adatforrás
- új szoftvert vezettek be
- támadói módszer változott
- új ATT&CK technika vált fontossá
- az elemzők rendszeresen figyelmen kívül hagyják

A Microsoft is azt javasolja, hogy az elavult vagy hosszú ideje nem hasznos szabályokat ne kezeljük automatikusan értékesnek.

## 24. Mit ne csináljunk?

Nem jó gyakorlat:

- minden eseményre riasztást készíteni
- forrás nélkül szabályt írni
- ismeretlen adatmezőre építeni
- false positive-okat korlátlanul kizárni
- tesztelés nélkül élesíteni
- soha nem felülvizsgálni
- ATT&CK technikákat csak díszítésként hozzárendelni

A cél nem a szabályok számának növelése.

A cél a használható detektálási képesség.

## 25. Mit érdemes kezdőként megjegyezni?

- A detection engineering használható biztonsági detektálások tervezése és fejlesztése.
- Először a támadói viselkedést kell megérteni.
- Csak azt lehet detektálni, amiről megfelelő adat áll rendelkezésre.
- A küszöbérték és az időablak sok szabály fontos része.
- A baseline segít megérteni a normális működést.
- A false positive téves riasztás.
- A false negative kihagyott valódi rosszindulatú esemény.
- A tuning a szabály finomhangolása.
- Egy detektálási szabályt tesztelni és dokumentálni kell.
- A MITRE ATT&CK segíthet a lefedettség rendszerezésében.
- A Sigma egy nyílt, gyártófüggetlen detektálási formátum.
- A detektálás nem egyszeri feladat, hanem folyamatos fejlesztés.

## 26. Ellenőrző kérdések

1. Mit jelent a detection engineering?
2. Mi az a detektálási szabály?
3. Miért kell először a kérdést megfogalmazni?
4. Miért fontos a megfelelő adatforrás?
5. Mi az a küszöbérték?
6. Mi az időablak?
7. Mit jelent a baseline?
8. Mi a false positive?
9. Mi a false negative?
10. Mit jelent a tuning?
11. Mi a rule lifecycle?
12. Miért fontos a tesztelés?
13. Mit érdemes dokumentálni egy szabályról?
14. Hogyan segíthet a MITRE ATT&CK?
15. Mit jelent a detection coverage?
16. Mi az a Sigma?
17. Miért gyártófüggetlen a Sigma?
18. Mi a logsource szerepe?
19. Miért fontos a riasztás utáni vizsgálati útmutató?
20. Miért kell rendszeresen felülvizsgálni a szabályokat?

## Források

1. Microsoft Learn  
   **Create and publish analytics rules for Microsoft Sentinel solutions**  
   https://learn.microsoft.com/en-us/azure/sentinel/isv/sentinel-analytic-rules-creation

2. Microsoft Learn  
   **Scheduled analytics rules in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/scheduled-rules-overview

3. Microsoft Learn  
   **Create scheduled analytics rules in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/create-analytics-rules

4. MITRE ATT&CK  
   **Data Sources**  
   https://attack.mitre.org/datasources/

5. Sigma Detection Format  
   **Getting Started**  
   https://sigmahq.io/docs/

6. Sigma Detection Format  
   **Sigma Rules**  
   https://sigmahq.io/docs/basics/rules.html

7. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

8. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](11-malware-basics.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](13-practical-examples.md)
