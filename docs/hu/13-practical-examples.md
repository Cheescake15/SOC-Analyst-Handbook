# 13 — Gyakorlati példák

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/13-practical-examples.md)

## Bevezetés

Az előző fejezetek külön-külön mutatták be a SOC működését, a hálózatokat, a Windows és Linux alapokat, a naplóelemzést, a SIEM-et, a CTI-t, a MITRE ATT&CK-öt, az incidenskezelést, a malware-eket és a detektálási szabályokat.

Ebben a fejezetben ezeket egyszerű gyakorlati példákon keresztül kapcsolom össze.

A példák célja nem az, hogy valódi támadást hajtsunk végre.

A cél az elemzői gondolkodás gyakorlása:

```text
Mit látok?
Mit jelenthet?
Milyen adat hiányzik?
Mit ellenőrizzek következőként?
Mikor kell eszkalálni?
```

## 1. Egy egyszerű SOC-vizsgálat logikája

Egy kezdő számára hasznos lehet ugyanazt a gondolkodási sorrendet követni minden riasztásnál.

### 1. Mi történt?

Olvasd el a riasztás címét és leírását.

### 2. Mikor történt?

Határozd meg az időpontot és az időzónát.

### 3. Ki vagy mi érintett?

Például:

- felhasználó
- számítógép
- IP-cím
- fájl
- e-mail
- folyamat

### 4. Mi történt előtte és utána?

Készíts rövid idővonalat.

### 5. Normális lehet?

Keress egyszerű üzleti vagy technikai magyarázatot.

### 6. Mi teszi gyanússá?

Kapcsold össze a szokatlan részleteket.

### 7. Mi hiányzik?

Ne találgass. Írd le, mit kell még ellenőrizni.

### 8. Mi legyen a következő lépés?

Lehet:

- további keresés
- felhasználó megkeresése
- eszkaláció
- incidens megnyitása
- riasztás lezárása

## 2. Példa 1 — Több sikertelen bejelentkezés

A SIEM riasztása:

```text
User: anna
Failed logons: 18
Time window: 5 minutes
Source IP: 10.10.5.24
```

### Első benyomás

Sok sikertelen belépés rövid idő alatt gyanús lehet.

Lehetséges magyarázat:

- elfelejtett jelszó
- régi jelszót használó alkalmazás
- brute force próbálkozás

### Mit ellenőrizzünk?

1. Volt-e utána sikeres bejelentkezés?
2. Ismert-e a forrás IP?
3. Ugyanerről az IP-ről más fiókokat is próbáltak?
4. A felhasználó valóban próbált belépni?
5. Ugyanez rendszeresen előfordul-e?

### Idővonal

```text
09:01 — sikertelen belépés
09:02 — sikertelen belépés
09:03 — további próbálkozások
09:05 — sikeres belépés
```

A sikeres belépés miatt a riasztás érdekesebbé válik.

### Lehetséges következtetés

```text
További vizsgálat szükséges.
```

Nem helyes azonnal azt mondani, hogy a fiókot feltörték.

## 3. Példa 2 — Phishing e-mail

Egy felhasználó jelenti:

```text
Subject: Urgent password expiration
Sender: support@example-security-mail.com
Link: login-example-secure.com
```

Az e-mail azt állítja, hogy a jelszó hamarosan lejár.

### Mit vizsgáljunk?

- valódi-e a küldő domainje
- hová mutat a link
- más felhasználó is kapta-e
- kattintott-e valaki
- adott-e meg valaki jelszót
- van-e hozzá kapcsolódó CTI-információ

### Egyszerű vizsgálati logika

```text
Gyanús küldő
+
sürgető üzenet
+
bejelentkezési link
=
phishing lehetősége
```

Ez még nem bizonyíték, de jó ok a további vizsgálatra.

### Ha a felhasználó kattintott

Ellenőrizhető:

- böngésző vagy proxy napló
- DNS-napló
- bejelentkezési események
- EDR-adatok
- e-mail gateway naplók

### MITRE ATT&CK

A phishing az Initial Access taktikához kapcsolódhat.

## 4. Példa 3 — Gyanús PowerShell

Az EDR riasztása:

```text
Process: powershell.exe
Parent process: winword.exe
User: bela
```

### Miért érdekes?

PowerShell önmagában normális.

Az viszont szokatlanabb lehet, ha a Microsoft Word indítja el.

### Mit ellenőrizzünk?

1. Milyen dokumentumot nyitott meg a felhasználó?
2. Honnan származott?
3. Mi volt a PowerShell parancssora?
4. Volt-e kódolt parancs?
5. Történt-e külső hálózati kapcsolat?
6. Jött-e létre új fájl?
7. Jelzett-e a vírusvédelem?

### Lehetséges idővonal

```text
11:03 — Word dokumentum megnyílt
11:04 — winword.exe → powershell.exe
11:04 — PowerShell külső domainhez kapcsolódott
11:05 — új fájl jelent meg a Temp mappában
```

A több összefüggő esemény miatt az eset magasabb prioritást kaphat.

### MITRE ATT&CK

Lehetséges technika:

```text
T1059.001 — PowerShell
```

## 5. Példa 4 — Malware-riasztás

A vírusvédelem jelzi:

```text
Threat detected: Trojan
File: C:\Users\user\AppData\Local\Temp\update.exe
```

### Első kérdések

- futott-e a fájl
- honnan került a gépre
- mi a hash-e
- izolálta-e a vírusvédelem
- van-e másik érintett gép

### Hash használata

A fájl SHA-256 értéke például kereshető:

- belső EDR-ben
- SIEM-ben
- engedélyezett CTI-forrásban

A kérdés:

```text
Megjelent-e ugyanez a fájl
másik gépen is?
```

### Fontos

A kezdő ne futtassa a fájlt saját gépen.

## 6. Példa 5 — Új adminisztrátori fiók

Windows-esemény:

```text
Event ID: 4720
New account: backup_admin
Time: 02:17
```

Később:

```text
Az új fiók
adminisztrátori csoporttagságot kapott.
```

### Miért érdekes?

Új fiók létrehozása lehet normális adminisztráció.

Hajnali időpont és gyors jogosultságnövelés azonban további vizsgálatot indokolhat.

### Mit ellenőrizzünk?

- ki hozta létre a fiókot
- volt-e jóváhagyott változtatás
- honnan történt a művelet
- belépett-e később az új fiók
- milyen rendszereket ért el

## 7. Példa 6 — Gyanús SSH Linuxon

Linux napló:

```text
Failed password for admin from 198.51.100.24
Failed password for admin from 198.51.100.24
Failed password for admin from 198.51.100.24
Accepted password for admin from 198.51.100.24
```

### Miért érdekes?

A sok sikertelen próbálkozást sikeres belépés követi.

### Mit vizsgáljunk?

- ismert-e az IP
- engedélyezett-e a külső SSH
- valóban az admin jelentkezett-e be
- mi történt a belépés után
- használtak-e sudo parancsot
- jött-e létre cronfeladat
- történt-e külső kapcsolat

### Egyszerű idővonal

```text
01:10 — sikertelen SSH
01:11 — sikertelen SSH
01:13 — sikeres SSH
01:15 — sudo
01:17 — új cronfeladat
```

Ez már erősebb gyanút ad, mint az első esemény önmagában.

## 8. Példa 7 — CTI-találat

Egy CTI-forrás szerint:

```text
malicious-example.com
```

egy aktív phishing kampányhoz kapcsolódik.

### SOC-kérdés

```text
Láttuk-e ezt a domaint
a saját környezetünkben?
```

### Hol kereshetünk?

- DNS-naplók
- proxy
- tűzfal
- e-mail gateway
- EDR
- SIEM

### Eredmény

```text
3 munkaállomás
kapcsolódott a domainhez
az elmúlt 7 napban.
```

Ezután gépenként meg kell vizsgálni:

- melyik felhasználó
- milyen folyamat
- mikor
- mi történt utána

A CTI így válik használható belső vizsgálattá.

## 9. Példa 8 — Ransomware-gyanú

A helpdesk több bejelentést kap:

```text
Nem nyílnak meg a dokumentumok.
A fájlok neve megváltozott.
```

Az EDR több gépen tömeges fájlmódosítást lát.

### Első prioritás

Ez már potenciálisan súlyos incidens.

Kezdő elemzőként fontos:

```text
gyors eszkaláció
```

### Lehetséges kérdések

- hány gép érintett
- ugyanaz a folyamat módosítja-e a fájlokat
- van-e közös felhasználói fiók
- megjelent-e zsaroló üzenet
- érintett-e fájlszerver
- rendelkezésre állnak-e mentések

A containment döntéseket a szervezet incidenskezelési eljárása szerint kell meghozni.

## 10. Példa 9 — Ismeretlen külső kapcsolat

A tűzfal riaszt:

```text
Source: workstation-24
Destination: 203.0.113.90
Port: 443
Connection every 60 seconds
```

### Első fontos felismerés

A 443-as port általában HTTPS.

Ez önmagában normális.

A pontosan ismétlődő kapcsolat viszont érdekes lehet.

### Mit vizsgáljunk?

- melyik folyamat hozza létre
- ismert-e a domain vagy IP
- milyen gyakran történik
- más gépek is kapcsolódnak-e
- mikor kezdődött
- kapcsolódik-e malware-riasztáshoz

A rendszeres rövid kapcsolatot néha beaconingnak nevezik.

Ez lehet C2-jellegű tevékenység, de normális alkalmazás is.

## 11. Példa 10 — False positive

A SIEM riasztása:

```text
Impossible travel detected
Budapest → London
20 minutes
```

Elsőre ez lehetetlennek tűnik.

### Vizsgálat

Kiderül:

- a felhasználó Budapesten van
- vállalati VPN-t használ
- a VPN kilépési pontja Londonban van

### Következtetés

```text
False positive
```

Ez jó példa arra, miért fontos a kontextus.

## 12. Példa 11 — Benign true positive

Riasztás:

```text
Multiple vulnerability scan attempts detected
```

A forrás IP a vállalat saját biztonsági tesztszervere.

A security team megerősíti, hogy jóváhagyott vizsgálat futott.

### Következtetés

A szabály helyesen felismerte a mintát.

A tevékenység azonban engedélyezett volt.

Ez lehet **benign true positive**.

## 13. Példa 12 — Adatforrás-hiba

A SOC dashboardján:

```text
Windows Security logs
Last event received: 9 hours ago
```

Nincs biztonsági riasztás.

Mégis probléma lehet.

### Miért?

Ha nincs napló, a SIEM nem látja a Windows-eseményeket.

Ez detektálási vakfoltot okoz.

### Mit ellenőrizzünk?

- működik-e a log forwarder
- van-e hálózati hiba
- megtelt-e a tárhely
- változott-e konfiguráció
- más rendszerek küldenek-e adatot

A SOC-nak nemcsak a támadásokat, hanem saját adatforrásainak állapotát is figyelnie kell.

## 14. Egyszerű incident note példa

Egy rövid elemzői jegyzet lehet:

```text
Alert:
Multiple failed logons followed by successful logon

User:
anna

Source IP:
198.51.100.24

Timeline:
09:01–09:04 — 18 failed logons
09:05 — successful logon

Checks performed:
Source IP reviewed
No similar attempts against other users
User confirmation pending

Assessment:
Suspicious activity, not yet confirmed malicious

Next step:
Contact user and review post-logon activity
```

A jó jegyzet:

- rövid
- tényszerű
- időrendi
- elkülöníti a tényt és a feltételezést

## 15. Mit jelent az entity?

A Microsoft Sentinel és más SIEM-ek gyakran **entityként** kezelik a vizsgálat fő objektumait.

Példák:

- felhasználó
- számítógép
- IP-cím
- domain
- fájl
- folyamat

Egy incidens vizsgálatakor ezek kapcsolata nagyon fontos.

Például:

```text
User
 ↓
Computer
 ↓
Process
 ↓
IP address
```

Ez segít a történet felépítésében.

## 16. Alertből incident

Egy riasztás egy konkrét észlelt problémát jelezhet.

Egy incidens viszont több kapcsolódó riasztást és bizonyítékot tartalmazhat.

Példa:

```text
Alert 1 — suspicious login
Alert 2 — PowerShell activity
Alert 3 — malware detection
```

Ha ugyanazt a felhasználót és gépet érintik, egyetlen incidens részei lehetnek.

A Microsoft Sentinel jelenlegi dokumentációja is úgy kezeli az incidenst, mint az adott vizsgálathoz tartozó kapcsolódó riasztások és bizonyítékok összességét.

## 17. Egyszerű prioritási gondolkodás

Két riasztás:

### A

```text
1 sikertelen bejelentkezés
normál felhasználó
belső hálózat
```

### B

```text
sikeres külső bejelentkezés
domain admin fiók
éjjel
utána PowerShell
```

A B riasztást valószínűleg előbb kell megvizsgálni.

Miért?

Mert fontosabb:

- a fiók
- a hozzáférés
- az időpont
- a kapcsolódó tevékenység

## 18. Egyszerű ATT&CK-mapping

Egy eseménysor:

```text
Phishing e-mail
↓
PowerShell
↓
Scheduled Task
↓
External C2
```

Egyszerű mapping:

| Esemény | ATT&CK |
|---|---|
| phishing | Initial Access |
| PowerShell | Execution |
| scheduled task | Persistence |
| C2 kapcsolat | Command and Control |

A mapping segít rendszerezni a történetet.

Nem helyettesíti a bizonyítékot.

## 19. Egyszerű detection tuning példa

Első szabály:

```text
Minden 4625 eseményre riasztás
```

Eredmény:

```text
naponta 3000 riasztás
```

Ez használhatatlan.

Új szabály:

```text
Legalább 15 darab 4625
ugyanarra a felhasználóra
5 percen belül
```

Eredmény:

```text
naponta 8 riasztás
```

Ez már kezelhetőbb.

Ezután meg kell vizsgálni, hogy a valódi támadásokat továbbra is felismeri-e.

## 20. Egyszerű threat hunting kérdések

A threat hunting nem feltétlenül riasztásból indul.

Lehet egy hipotézis:

```text
Lehetséges, hogy támadók
PowerShellt használnak
kódolt parancsok futtatására.
```

Keresési kérdések:

- hol futott PowerShell
- kinél szerepel EncodedCommand
- milyen parent process indította
- volt-e külső kapcsolat
- más gépen megjelent-e ugyanaz a minta

A hunting célja proaktívan keresni a gyanús viselkedést.

## 21. Egyszerű CTI-hunting kapcsolat

CTI-jelentés:

```text
Egy támadócsoport gyakran használ:
phishinget
PowerShellt
scheduled taskot
```

A SOC nemcsak konkrét IoC-t kereshet.

Viselkedést is kereshet:

```text
Office → PowerShell → Scheduled Task
```

Ez gyakran tartósabb detektálási ötlet, mint egyetlen IP-cím.

## 22. Hogyan gondolkodjon egy kezdő?

Használható kérdéssor:

```text
1. Mi történt?
2. Miért riasztott a rendszer?
3. Mi normális ebben?
4. Mi szokatlan?
5. Milyen más adatforrás segíthet?
6. Mi történt előtte?
7. Mi történt utána?
8. Mi bizonyított tény?
9. Mi csak feltételezés?
10. Mi legyen a következő lépés?
```

Ez fontosabb készség, mint sok parancs fejből ismerete.

## 23. Biztonságos gyakorlás

Kezdőként érdemes:

- előre elkészített naplókat elemezni
- oktatási SIEM környezetet használni
- saját tesztadatokon keresni
- CTF vagy blue team lab környezetet használni
- ATT&CK technikákat példákhoz rendelni
- incident note-okat írni

Nem érdemes engedély nélkül:

- idegen rendszert vizsgálni
- támadó parancsokat futtatni
- malware-t saját gépen elindítani
- aktív támadó infrastruktúrához kapcsolódni

## 24. Mini gyakorlófeladat 1

Napló:

```text
18:01 — user1 failed login
18:01 — user1 failed login
18:02 — user1 failed login
18:04 — user1 successful login
18:06 — user1 created new account
```

Kérdések:

1. Mi a legfontosabb esemény?
2. Mi teszi gyanússá az idővonalat?
3. Milyen adatot kérnél még?
4. Eszkalálnád-e?

## 25. Mini gyakorlófeladat 2

```text
09:10 — outlook.exe
09:11 — winword.exe
09:12 — powershell.exe
09:12 — connection to 203.0.113.80
09:13 — new executable in Temp
```

Kérdések:

1. Milyen történet rajzolódhat ki?
2. Mi lehet normális magyarázat?
3. Mit ellenőriznél a PowerShellnél?
4. Milyen ATT&CK taktikák jelenhetnek meg?
5. Milyen adatot keresnél az EDR-ben?

## 26. Mini gyakorlófeladat 3

```text
02:10 — SSH failed
02:10 — SSH failed
02:11 — SSH successful
02:13 — sudo
02:15 — cron job created
```

Kérdések:

1. Miért érdekes a sikeres SSH?
2. Mit ellenőriznél a sudo eseménynél?
3. Miért lehet fontos a cronfeladat?
4. Milyen containment lehet szükséges, ha a kompromittálódás megerősítést nyer?

## 27. Mit érdemes kezdőként megjegyezni?

- Egy riasztás csak a vizsgálat kezdete.
- Mindig nézd meg az esemény előtti és utáni történéseket.
- Egyetlen esemény ritkán bizonyít támadást.
- A kontextus nélkül könnyű téves következtetésre jutni.
- Az idővonal az egyik legegyszerűbb és leghasznosabb eszköz.
- A tényt és a feltételezést külön kell kezelni.
- A CTI segíthet kontextust adni.
- A MITRE ATT&CK segít rendszerezni a viselkedést.
- A detection tuning csökkentheti a zajt.
- Az adatforrás kiesése maga is biztonsági probléma lehet.
- Egy jó SOC-elemző tudja, mikor kell tovább vizsgálni és mikor kell eszkalálni.
- Kezdőként a jó kérdések fontosabbak, mint a túl sok technikai parancs.

## 28. Ellenőrző kérdések

1. Mi legyen az első kérdés egy riasztásnál?
2. Miért fontos az idővonal?
3. Miért nem bizonyít támadást sok sikertelen bejelentkezés önmagában?
4. Mi teszi érdekesebbé a Wordből induló PowerShellt?
5. Mire használható egy malware hash?
6. Miért érdekes egy új adminisztrátori fiók?
7. Mit ellenőriznél sikeres SSH-belépés után?
8. Hogyan használható egy CTI-indikátor?
9. Miért fontos gyorsan eszkalálni ransomware-gyanúnál?
10. Mi az a beaconing?
11. Miért lehet false positive az impossible travel?
12. Mi a benign true positive?
13. Miért probléma, ha egy naplóforrás leáll?
14. Mit tartalmazzon egy incident note?
15. Mi az entity?
16. Mi a különbség alert és incident között?
17. Mi alapján lehet prioritást adni?
18. Mire jó az ATT&CK-mapping?
19. Miért kell tuningolni a detektálási szabályokat?
20. Mit jelent a threat hunting?

## Források

1. Microsoft Learn  
   **Security incident management in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/training/modules/incident-management-sentinel/

2. Microsoft Learn  
   **Investigate Microsoft Sentinel incidents in depth**  
   https://learn.microsoft.com/en-us/azure/sentinel/investigate-incidents

3. Microsoft Learn  
   **Navigate, triage, and manage Microsoft Sentinel incidents**  
   https://learn.microsoft.com/en-us/azure/sentinel/incident-navigate-triage

4. Microsoft Learn  
   **Use tasks to manage incidents in Microsoft Sentinel**  
   https://learn.microsoft.com/en-us/azure/sentinel/incident-tasks

5. MITRE ATT&CK  
   **Get Started**  
   https://attack.mitre.org/resources/

6. MITRE ATT&CK  
   **Adversary Emulation Plans**  
   https://attack.mitre.org/resources/adversary-emulation-plans/

7. Nemzeti Kiberbiztonsági Intézet  
   **Incidenskezelés**  
   https://nki.gov.hu/szolgaltatasok/tartalom/incidenskezeles/

8. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

---

[← Előző fejezet](12-detection-engineering.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](14-cheat-sheet.md)
