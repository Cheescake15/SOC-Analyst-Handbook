# 14 — SOC Analyst gyorssegédlet

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/14-cheat-sheet.md)

## Bevezetés

Ez a fejezet rövid összefoglaló az előző részek legfontosabb fogalmairól.

Nem helyettesíti a részletes fejezeteket.

Arra szolgál, hogy gyorsan vissza lehessen keresni:

- egy fontos fogalmat
- egy eseményazonosítót
- egy Linux vagy Windows parancsot
- egy SOC-vizsgálati kérdést
- egy ATT&CK kifejezést
- egy incidenskezelési lépést

## 1. SOC alapfogalmak

| Fogalom | Rövid jelentés |
|---|---|
| SOC | Security Operations Center, biztonsági műveleti központ |
| Alert | riasztás, amely további vizsgálatot igényelhet |
| Event | egy rendszerben történt esemény |
| Incident | valódi vagy valószínű biztonsági probléma |
| Triage | gyors első értékelés |
| Escalation | az ügy továbbadása magasabb szakmai szintre |
| Playbook | előre elkészített vizsgálati vagy válaszlépések |
| Runbook | konkrét műveleti lépések leírása |
| False positive | téves riasztás |
| False negative | valódi támadás, amelyet a szabály nem észlelt |

## 2. Hálózati alapfogalmak

| Fogalom | Rövid jelentés |
|---|---|
| IP-cím | egy eszköz hálózati címe |
| MAC-cím | hálózati interfész fizikai azonosítója |
| DNS | domainneveket IP-címekhez rendel |
| DHCP | automatikusan hálózati beállításokat ad |
| TCP | kapcsolat-orientált hálózati protokoll |
| UDP | gyorsabb, kapcsolat nélküli protokoll |
| ICMP | hálózati állapot- és hibajelzések |
| NAT | belső és külső címek közötti címfordítás |
| Port | egy szolgáltatás logikai végpontja |
| HTTPS | titkosított HTTP-kommunikáció |

## 3. Gyakori portok

| Port | Szolgáltatás |
|---:|---|
| 20/21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

Fontos:

```text
Egy port önmagában nem bizonyít támadást.
```

Mindig vizsgálni kell a kapcsolat kontextusát.

## 4. Windows fontos eseményazonosítók

| Event ID | Jelentés |
|---:|---|
| 4624 | sikeres bejelentkezés |
| 4625 | sikertelen bejelentkezés |
| 4688 | új folyamat indult |
| 4720 | új felhasználói fiók |
| 4728 | felhasználó hozzáadása globális biztonsági csoporthoz |
| 4732 | felhasználó hozzáadása helyi biztonsági csoporthoz |
| 4740 | felhasználói fiók zárolása |
| 7045 | új szolgáltatás telepítése |

Egy Event ID mindig csak kiindulópont.

A részleteket is meg kell nézni.

## 5. Windows gyors parancsok

### Folyamatok

```powershell
Get-Process
```

### Szolgáltatások

```powershell
Get-Service
```

### Ütemezett feladatok

```powershell
Get-ScheduledTask
```

### Legutóbbi rendszeresemények

```powershell
Get-WinEvent -LogName System -MaxEvents 20
```

### Event Viewer

```powershell
eventvwr.msc
```

## 6. Linux gyors parancsok

### Aktuális felhasználó

```bash
whoami
```

### Bejelentkezett felhasználók

```bash
who
```

### Felhasználó és csoportok

```bash
id
groups
```

### Fájlok és jogosultságok

```bash
ls -l
```

### Folyamatok

```bash
ps aux
```

### Aktív hálózati kapcsolatok

```bash
ss -tulpen
```

### Naplók

```bash
journalctl -n 20
```

### Futó szolgáltatások

```bash
systemctl --type=service --state=running
```

### Cronfeladatok

```bash
crontab -l
```

## 7. Linux fájljogosultságok

| Jel | Jelentés |
|---|---|
| r | read, olvasás |
| w | write, írás |
| x | execute, végrehajtás |

Példa:

```text
-rwxr-x---
```

Ez azt jelenti:

- tulajdonos: olvasás, írás, futtatás
- csoport: olvasás, futtatás
- más: nincs jogosultság

## 8. Fontos Linux könyvtárak

| Könyvtár | Jelentés |
|---|---|
| /home | felhasználói fájlok |
| /etc | konfigurációk |
| /var/log | naplók |
| /tmp | ideiglenes fájlok |
| /usr/bin | programok |
| /root | root saját könyvtára |
| /proc | folyamat- és kernelinformáció |

## 9. Naplóelemzés gyors mezők

Egy naplóbejegyzésnél gyakran ezeket érdemes keresni:

- timestamp
- user
- hostname
- source IP
- destination IP
- source port
- destination port
- process
- command line
- file name
- hash
- event ID
- result

## 10. Gyors vizsgálati kérdések

Egy riasztásnál:

```text
1. Mi történt?
2. Mikor történt?
3. Ki vagy mi érintett?
4. Mi történt előtte?
5. Mi történt utána?
6. Normális lehet?
7. Mi teszi gyanússá?
8. Milyen adat hiányzik?
9. Van kapcsolódó CTI?
10. Mi legyen a következő lépés?
```

## 11. SIEM alapfogalmak

| Fogalom | Rövid jelentés |
|---|---|
| SIEM | központi biztonsági naplógyűjtés és elemzés |
| Ingestion | adatok beérkezése |
| Parsing | napló mezőkre bontása |
| Normalisation | mezők egységesítése |
| Query | keresés az adatokban |
| Detection Rule | riasztási szabály |
| Correlation | több esemény összekapcsolása |
| Dashboard | áttekintő nézet |
| Severity | riasztás súlyossága |
| Tuning | szabály finomhangolása |

## 12. Detection Engineering gyors összefoglaló

Jó detektálás építési sorrendje:

```text
Fenyegetés megértése
↓
Adatforrás kiválasztása
↓
Detektálási logika
↓
Tesztelés
↓
False positive-ok
↓
Tuning
↓
Dokumentáció
↓
Felülvizsgálat
```

## 13. False positive és false negative

### False positive

A szabály riaszt, de nincs valódi támadás.

### False negative

Valódi támadás történik, de a szabály nem jelez.

Mindkettő probléma.

## 14. Sigma gyors összefoglaló

A Sigma egy nyílt detektálási szabályformátum.

Gyakori mezők:

```text
title
logsource
detection
condition
falsepositives
level
tags
```

Egyszerű példa:

```yaml
title: Failed Windows Logon

logsource:
  product: windows
  service: security

detection:
  selection:
    EventID: 4625
  condition: selection

level: low
```

## 15. Cyber Threat Intelligence alapfogalmak

| Fogalom | Rövid jelentés |
|---|---|
| CTI | elemzett fenyegetési információ |
| Threat actor | támadó személy vagy csoport |
| IoC | kompromittálódásra utaló technikai jel |
| TTP | támadói taktika, technika és eljárás |
| Feed | folyamatosan frissülő CTI-forrás |
| Confidence | elemzői bizonyosság szintje |
| TLP | információ megosztási szabálya |
| STIX | strukturált CTI-formátum |
| TAXII | CTI-adatok továbbításának mechanizmusa |

## 16. Gyakori IoC-k

- IP-cím
- domain
- URL
- fájl hash
- e-mail-cím
- fájlnév

Fontos:

```text
IoC önmagában nem mindig bizonyít támadást.
```

## 17. TLP 2.0

| Jelölés | Rövid jelentés |
|---|---|
| TLP:RED | nagyon szűk körben osztható meg |
| TLP:AMBER | korlátozott megosztás |
| TLP:GREEN | közösségen belül megosztható |
| TLP:CLEAR | szabadon megosztható |

## 18. MITRE ATT&CK alapfogalmak

| Fogalom | Jelentés |
|---|---|
| Tactic | a támadó célja |
| Technique | a cél elérésének módja |
| Sub-technique | pontosabb technika |
| Procedure | konkrét megvalósítás |
| Group | ismert fenyegetési szereplő |
| Software | malware vagy támadói eszköz |
| Matrix | taktikák és technikák vizuális rendszere |

## 19. Gyakori ATT&CK taktikák

- Reconnaissance
- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command and Control
- Exfiltration
- Impact

Nem szükséges mindet fejből tudni.

A logikájuk megértése fontosabb.

## 20. Egy fontos ATT&CK példa

```text
T1059.001 — PowerShell
```

Ez a Command and Scripting Interpreter technika PowerShell altechnikája.

## 21. Malware típusok

| Típus | Rövid jelentés |
|---|---|
| Virus | más fájlhoz kapcsolódva terjedhet |
| Worm | önállóan terjedhet |
| Trojan | ártalmatlan programnak álcázza magát |
| Ransomware | titkosít vagy hozzáférést blokkol, majd váltságdíjat kér |
| Spyware | megfigyel és adatot gyűjt |
| Keylogger | billentyűleütéseket rögzít |
| Backdoor | rejtett hozzáférést biztosít |
| Downloader | további malware-t tölt le |
| Dropper | malware-komponenst helyez el |
| Bot | távolról irányított fertőzött eszköz |
| Rootkit | támadói jelenlét elrejtésére szolgálhat |

## 22. Malware-gyanú esetén

Ellenőrizhető:

- fájl neve
- fájl helye
- hash
- folyamat
- parent process
- hálózati kapcsolat
- vírusvédelmi riasztás
- más gépen való előfordulás

Kezdőként:

```text
Ismeretlen malware-t
ne futtass saját gépen.
```

## 23. Incident Response gyors összefoglaló

Klasszikus lépések:

```text
Preparation
↓
Detection and Analysis
↓
Containment
↓
Eradication
↓
Recovery
↓
Lessons Learned
```

A NIST újabb szemlélete ezt a teljes Cybersecurity Framework-be helyezi.

## 24. Incident Response kulcsszavak

| Fogalom | Rövid jelentés |
|---|---|
| Triage | első értékelés |
| Containment | terjedés korlátozása |
| Eradication | támadó jelenlétének megszüntetése |
| Recovery | biztonságos helyreállítás |
| Evidence | bizonyíték |
| Chain of Custody | bizonyíték kezelésének dokumentálása |
| Escalation | ügy továbbadása |
| Lessons Learned | incidens utáni tanulságok |

## 25. Phishing gyors ellenőrzőlista

Vizsgáld:

- feladó címe
- domain
- link célja
- melléklet
- sürgető megfogalmazás
- jelszóbekérés
- más címzettek
- kattintás történt-e
- hitelesítő adat megadás történt-e
- kapcsolódó CTI

## 26. Gyanús PowerShell gyors ellenőrzőlista

Vizsgáld:

- user
- computer
- command line
- parent process
- EncodedCommand
- external connection
- created file
- scheduled task
- antivirus alert
- related events

## 27. Sikertelen bejelentkezés gyors ellenőrzőlista

Vizsgáld:

- hány próbálkozás
- milyen időablak
- melyik felhasználó
- melyik IP
- más fiókok is érintettek-e
- történt-e sikeres belépés utána
- ismert-e a forrás
- van-e hasonló korábbi esemény

## 28. SSH gyors ellenőrzőlista

Vizsgáld:

- source IP
- user
- failed attempts
- successful login
- sudo
- cron
- új fájl
- új SSH-kulcs
- külső kapcsolat

## 29. Ransomware gyors ellenőrzőlista

Vizsgáld:

- hány gép érintett
- fájlok tömeges változása
- zsaroló üzenet
- közös folyamat
- közös felhasználó
- fájlszerver érintett-e
- mentések állapota
- EDR-riasztások
- terjedés jelei

Ransomware-gyanú esetén gyors eszkaláció szükséges lehet.

## 30. Prioritási kérdések

Egy riasztás sürgősebb lehet, ha:

- kiemelt jogosultságú fiókot érint
- kritikus szerveren történik
- több rendszeren jelenik meg
- adatlopásra utal
- aktív malware kapcsolódik hozzá
- külső támadó infrastruktúrával kommunikál
- gyorsan terjed
- üzleti működést veszélyeztet

## 31. Incident note gyors sablon

```text
Alert:
[riasztás neve]

Time:
[időpont]

User:
[felhasználó]

Host:
[gép]

Source IP:
[IP]

What happened:
[rövid leírás]

Timeline:
[időrendi események]

Checks performed:
[mit ellenőriztem]

Known facts:
[bizonyított tények]

Unknown:
[mi hiányzik]

Assessment:
[értékelés]

Next step:
[következő lépés]
```

## 32. Hasznos elemzői kifejezések

A dokumentációban hasznos lehet:

```text
Observed
Confirmed
Likely
Possible
No evidence found
Further investigation required
User confirmation pending
Activity appears legitimate
Escalation recommended
```

Ezek segítenek elválasztani a tényeket a feltételezésektől.

## 33. Amit kezdőként ne felejts el

- Ne feltételezz többet, mint amit az adatok bizonyítanak.
- Mindig nézd az idővonalat.
- Ellenőrizd a felhasználót, gépet és IP-címet.
- Keress kapcsolódó eseményeket.
- Egyetlen IoC nem mindig bizonyít támadást.
- Egyetlen Event ID nem mindig bizonyít támadást.
- A PowerShell önmagában nem rosszindulatú.
- A magas port vagy a 443-as port önmagában nem gyanús.
- A false positive normális része a SOC munkának.
- Ha nincs elég adat, ezt dokumentáld.
- Ha bizonytalan vagy és a kockázat magas, eszkalálj.
- Engedély nélkül ne vizsgálj idegen rendszert.
- Ismeretlen malware-t ne futtass saját gépen.

## 34. Végső gondolkodási minta

```text
Mi történt?
↓
Miért lehet fontos?
↓
Milyen bizonyítékom van?
↓
Mi lehet normális magyarázat?
↓
Milyen adat hiányzik?
↓
Mi történt előtte és utána?
↓
Mekkora a kockázat?
↓
Mi legyen a következő lépés?
```

Ez a gondolkodási folyamat a kézikönyv egyik legfontosabb tanulsága.

## Források

A gyorssegédlet az előző fejezetekben használt hivatalos és szakmai forrásokra épül, többek között:

1. NIST  
   **Cybersecurity Framework 2.0**  
   https://www.nist.gov/cyberframework

2. NIST  
   **SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

3. MITRE ATT&CK  
   https://attack.mitre.org/

4. Microsoft Learn  
   **Microsoft Sentinel documentation**  
   https://learn.microsoft.com/en-us/azure/sentinel/

5. Sigma Detection Format  
   https://sigmahq.io/docs/

6. FIRST  
   **Traffic Light Protocol 2.0**  
   https://www.first.org/tlp/

7. Nemzeti Kiberbiztonsági Intézet  
   https://nki.gov.hu/

---

[← Előző fejezet](13-practical-examples.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](15-references.md)
