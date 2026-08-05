# 04 — Windows biztonság

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/04-windows-security.md)

## Bevezetés

A Windows sok vállalatnál a mindennapi munka alapja. Munkaállomásokon és szervereken is használják, ezért egy SOC-elemző gyakran találkozik Windowsból származó riasztásokkal és naplóbejegyzésekkel.

Ebben a fejezetben azokat az alapfogalmakat foglalom össze, amelyek egy kezdő számára is érthetőek. A cél nem a Windows minden technikai részletének bemutatása, inkább azt szeretném megmutatni, hol keletkezhetnek fontos nyomok, és miért lehet egy esemény érdekes biztonsági szempontból.

## 1. Miért fontos a Windows egy SOC-ban?

Egy Windows-rendszeren sokféle esemény történik:

- a felhasználók bejelentkeznek
- programok indulnak el
- fájlok módosulnak
- szolgáltatások futnak a háttérben
- PowerShell-parancsok hajtódnak végre
- ütemezett feladatok indulnak
- a rendszer eseményeket naplóz

Ezek többsége normális. A SOC feladata nem az, hogy minden eseményt támadásnak tekintsen. Inkább azt kell megvizsgálni, hogy a tevékenység megszokott-e az adott felhasználónál és számítógépen.

## 2. Az Event Viewer

Az **Event Viewer**, magyarul Eseménynapló, a Windows egyik beépített eszköze. Itt lehet megtekinteni a rendszer által rögzített eseményeket.

A fontosabb naplók:

### Application

Az alkalmazások működésével kapcsolatos eseményeket tartalmazza.

Példa:

```text
Egy program váratlanul leállt.
```

Ez lehet egyszerű programhiba. Egy vizsgálat során akkor válhat érdekessé, ha más szokatlan eseményekkel egy időben jelenik meg.

### Security

A biztonsági eseményeket tartalmazza.

Például:

- sikeres bejelentkezés
- sikertelen bejelentkezés
- új felhasználói fiók
- jogosultságváltozás
- folyamatindítás

A napló tartalma attól is függ, milyen auditbeállítások vannak engedélyezve.

### System

A Windows rendszerösszetevőinek eseményeit tartalmazza.

Például:

- egy szolgáltatás elindult
- egy illesztőprogram hibát jelzett
- a számítógép váratlanul újraindult

### Applications and Services Logs

Itt egyes Windows-összetevők és programok részletesebb naplói találhatók.

Például:

```text
Microsoft-Windows-PowerShell
Microsoft-Windows-TaskScheduler
Microsoft-Windows-Windows Defender
```

A Nemzeti Kiberbiztonsági Intézet eseménynaplózásról szóló összefoglalója is kiemeli, hogy a megfelelő naplózás segíti a fenyegetések észlelését és az incidensek kivizsgálását.

## 3. Mi az az Event ID?

A Windows-eseményekhez gyakran tartozik egy számszerű azonosító. Ezt **Event ID-nak** nevezik.

Ez olyan, mint egy eseménytípus sorszáma.

Az Event ID önmagában nem elég a döntéshez. A részleteket is meg kell nézni:

- melyik felhasználó érintett
- melyik számítógépen történt
- honnan érkezett a kapcsolat
- mikor történt
- milyen program indult el

## 4. Néhány fontos Event ID

### 4624 — Sikeres bejelentkezés

Ez akkor jelenik meg, amikor létrejön egy bejelentkezési munkamenet.

Általában normális esemény. Gyanúsabb lehet, ha:

- szokatlan időpontban történik
- ismeretlen IP-címről érkezik
- rendszergazdai fiókot érint
- sok sikertelen próbálkozás előzi meg

### 4625 — Sikertelen bejelentkezés

Ez sikertelen belépési próbálkozást jelez.

Egyetlen eseményt okozhat elgépelés. Sok ilyen esemény rövid időn belül utalhat:

- rosszul beállított programra
- elmentett régi jelszóra
- brute force próbálkozásra
- jelszószórásra

### 4688 — Új folyamat indult

A **folyamat** egy futó program vagy programrész.

Példák:

```text
notepad.exe
powershell.exe
cmd.exe
```

A PowerShell vagy a Parancssor önmagában nem rosszindulatú. Azt kell megvizsgálni, milyen paranccsal és milyen körülmények között indult el.

### 4720 — Új felhasználói fiók jött létre

Ez lehet normális rendszergazdai művelet.

Gyanúsabb lehet, ha:

- munkaidőn kívül történik
- ismeretlen adminisztrátor végzi
- az új fiók gyorsan magas jogosultságot kap
- más szokatlan esemény előzi meg

### 7045 — Új szolgáltatás telepítése

Egy új szolgáltatás lehet normális szoftvertelepítés része.

Támadók is létrehozhatnak szolgáltatást azért, hogy egy program a háttérben fusson vagy újraindítás után is elinduljon.

## 5. A bejelentkezési típus

A Windows bejelentkezési eseményeinél a **Logon Type** megmutatja, milyen módon történt a belépés.

| Logon Type | Egyszerű jelentés |
|---:|---|
| 2 | helyi bejelentkezés |
| 3 | hálózati hozzáférés |
| 5 | szolgáltatás indította |
| 7 | zárolt gép feloldása |
| 10 | távoli asztali bejelentkezés |
| 11 | gyorsítótárazott vállalati belépés |

A 10-es típus például Remote Desktop kapcsolatnál jelenhet meg.

Ez nem automatikusan gyanús. Érdekesebb lehet, ha ismeretlen külső címről történik, vagy a szervezetben ritkán használnak távoli asztalt.

## 6. Felhasználók és jogosultságok

A Windowsban nem minden felhasználó rendelkezik azonos jogosultsággal.

Egy rendszergazda például:

- programokat telepíthet
- rendszerbeállításokat módosíthat
- felhasználói fiókokat kezelhet
- szolgáltatásokat indíthat vagy állíthat le

A **legkisebb jogosultság elve** azt jelenti, hogy mindenki csak annyi hozzáférést kapjon, amennyi a munkájához valóban szükséges.

Ez csökkentheti a lehetséges kárt akkor is, ha egy fiókot illetéktelen személy szerez meg.

## 7. Mi az a Registry?

A **Windows Registry**, magyarul rendszerleíró adatbázis, egy központi beállítástár.

Egyszerű hasonlattal olyan, mint egy nagy, rendszerezett beállításgyűjtemény.

Fő részei:

```text
HKEY_LOCAL_MACHINE
HKEY_CURRENT_USER
HKEY_USERS
HKEY_CLASSES_ROOT
HKEY_CURRENT_CONFIG
```

A Registry módosítása lehet normális programtelepítés része.

Támadók is használhatják arra, hogy:

- programot indítsanak bejelentkezéskor
- módosítsák a rendszer viselkedését
- kikapcsoljanak egy védelmi beállítást
- tartósan jelen maradjanak a gépen

A kézi módosítása kockázatos. Kezdőként csak ellenőrzött laborban érdemes vele kísérletezni.

## 8. Windows-szolgáltatások

A **szolgáltatás** olyan program, amely általában a háttérben fut.

Példák:

- Windows Update
- Print Spooler
- Windows Event Log
- Microsoft Defender Antivirus Service

Lehetséges indítási módok:

- Automatic
- Automatic Delayed Start
- Manual
- Disabled

Egy új szolgáltatás gyanúsabb lehet, ha:

- megtévesztő neve van
- ismeretlen programot indít
- ideiglenes mappából fut
- rendszerszintű jogosultságot használ
- más gyanús esemény után jelenik meg

Nem szabad találomra szolgáltatásokat letiltani, mert több közülük szükséges a Windows működéséhez.

## 9. Ütemezett feladatok

A **Task Scheduler**, magyarul Feladatütemező, automatikusan indíthat el programokat és parancsokat.

Egy feladat két fontos része:

- a **trigger**, vagyis mi indítja el
- az **action**, vagyis mit hajt végre

Példa:

```text
Minden nap 18:00-kor induljon el a mentési program.
```

A feladatütemezés teljesen normális funkció.

Támadó is használhatja azért, hogy:

- egy program rendszeresen elinduljon
- a program újraindítás után is működjön
- a végrehajtás később történjen

Gyanúsabb lehet egy feladat, ha:

- ismeretlen programot indít
- ideiglenes mappából fut
- kódolt PowerShell-parancsot használ
- furcsa időközönként ismétlődik

## 10. PowerShell

A PowerShell egy Windowsban elérhető parancssori és automatizálási eszköz.

Rendszergazdák használhatják:

- felhasználók kezelésére
- rendszeradatok lekérdezésére
- fájlműveletekre
- távoli adminisztrációra
- ismétlődő feladatok automatizálására

A PowerShell önmagában nem kártékony. Támadók azért is használhatják, mert erős és sok rendszeren eleve megtalálható.

Gyanús lehet például:

- nagyon hosszú vagy nehezen olvasható parancs
- kódolt tartalom
- internetes letöltés
- biztonsági beállítás módosítása
- ismeretlen szkript futtatása
- PowerShell indítása egy Office-programból

A Microsoft dokumentációja szerint a PowerShell eseményei az Event Viewerben is megtekinthetők. A részletesebb naplózási lehetőségek közé tartozik a Script Block Logging.

Az NKI PowerShell-alapú fenyegetésekről szóló anyagai is bemutatják, hogy támadók gyakran legitim Windows-eszközöket használnak fel. Ezt **living off the land** módszernek is nevezik.

## 11. Folyamatok és a process tree

A **process tree**, magyarul folyamatfa, megmutatja, melyik program melyik másik programból indult el.

Normális példa:

```text
explorer.exe
└── notepad.exe
```

Érdekesebb példa:

```text
winword.exe
└── powershell.exe
    └── rundll32.exe
```

Ez azt mutatja, hogy a Word elindította a PowerShellt, amely egy további Windows-eszközt indított el.

Ez még nem bizonyít támadást, de további vizsgálatot indokolhat.

Az elemző megkérdezheti:

- megnyitott-e a felhasználó egy dokumentumot
- honnan származott a fájl
- milyen PowerShell-parancs futott
- történt-e hálózati kapcsolat
- létrejött-e új fájl vagy ütemezett feladat

## 12. Active Directory és Kerberos röviden

Sok vállalat **Active Directoryt**, röviden AD-t használ a felhasználók, számítógépek és jogosultságok központi kezelésére.

Egyszerű hasonlattal az AD olyan, mint egy vállalati címtár és beléptetőrendszer együtt.

A **domain controller** olyan szerver, amely részt vesz a bejelentkezések ellenőrzésében.

A **Kerberos** egy gyakori hitelesítési protokoll Windows-tartományokban.

A felhasználó sikeres hitelesítés után jegyeket kap. Ezekkel igazolhatja a jogosultságát különböző szolgáltatások felé anélkül, hogy minden alkalommal újra elküldené a jelszavát.

Kezdőként ezt érdemes megjegyezni:

- az AD központilag kezeli a vállalati identitásokat
- a domain controller fontos biztonsági szerepet tölt be
- a Kerberos jegyeket használ
- egy kiemelt jogosultságú fiók elvesztése nagy kockázatot jelenthet

## 13. Egyszerű vizsgálati példa

A SIEM a következő eseményeket jelzi:

```text
02:11 — több sikertelen bejelentkezés
02:15 — sikeres távoli bejelentkezés
02:17 — powershell.exe elindult
02:18 — új ütemezett feladat jött létre
```

Ezek együtt érdekesebbek, mint külön-külön.

Egy kezdő elemző a következőket ellenőrizheti:

1. melyik felhasználói fiók érintett
2. honnan érkezett a bejelentkezés
3. a felhasználó felismeri-e a tevékenységet
4. milyen PowerShell-parancs futott
5. mit indít az új ütemezett feladat
6. létrejött-e új fájl
7. történt-e külső hálózati kapcsolat
8. van-e hasonló esemény más gépen

A cél először az események időrendi összekapcsolása.

## 14. Hasznos, főként megtekintő parancsok

Futó folyamatok:

```powershell
Get-Process
```

Szolgáltatások:

```powershell
Get-Service
```

Ütemezett feladatok:

```powershell
Get-ScheduledTask
```

Legutóbbi rendszeresemények:

```powershell
Get-WinEvent -LogName System -MaxEvents 20
```

Event Viewer megnyitása:

```powershell
eventvwr.msc
```

Ezeket csak saját vagy engedélyezett rendszeren szabad használni.

## 15. Mit érdemes kezdőként megjegyezni?

- Az Event Viewer a Windows-események fontos forrása.
- Az Event ID egy eseménytípust jelöl, de a részleteket is el kell olvasni.
- A PowerShell, a szolgáltatások és az ütemezett feladatok normális adminisztrációs eszközök.
- Ugyanezeket az eszközöket támadók is felhasználhatják.
- Egy eseményt mindig a környezetével együtt kell értelmezni.
- Több egymást követő esemény gyakran fontosabb, mint egyetlen önálló bejegyzés.

## 16. Ellenőrző kérdések

1. Mire használható az Event Viewer?
2. Mi a különbség az Application, Security és System napló között?
3. Mit jelent az Event ID?
4. Mit jelezhet a 4624-es esemény?
5. Mit jelezhet a 4625-ös esemény?
6. Miért fontos a 4688-as esemény?
7. Mit jelent a legkisebb jogosultság elve?
8. Mi a Windows Registry?
9. Mi az a Windows-szolgáltatás?
10. Mi a trigger és az action egy ütemezett feladatnál?
11. Miért használják a PowerShellt rendszergazdák és támadók is?
12. Mit mutat meg a process tree?
13. Mi az Active Directory?
14. Mi a Kerberos alapvető szerepe?
15. Miért fontos több eseményt időrendben összekapcsolni?

## Források

1. Microsoft Learn  
   **4624: An account was successfully logged on**  
   https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4624

2. Microsoft Learn  
   **about Logging Windows PowerShell**  
   https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging

3. Microsoft Learn  
   **Get-WinEvent**  
   https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent

4. Microsoft Learn  
   **Task Scheduler**  
   https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page

5. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](03-network-fundamentals.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](05-linux-security.md)
