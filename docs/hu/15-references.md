# 15 — Források

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/15-references.md)

## Bevezetés

A SOC Analyst Handbook összeállításához elsősorban hivatalos, ellenőrizhető és szakmailag megbízható forrásokat használtam.

A cél nem az volt, hogy minél több link kerüljön a projektbe. Inkább olyan forrásokat választottam, amelyek:

- kezdők számára is használhatók
- szakmailag hitelesek
- rendszeresen frissülnek
- gyakorlati példákat is tartalmaznak
- további önálló tanulásra alkalmasak

A forrásokat témakörök szerint rendeztem.

## 1. NIST

A National Institute of Standards and Technology, röviden NIST, az egyik legfontosabb kiberbiztonsági szakmai forrás.

### NIST Cybersecurity Framework 2.0

https://www.nist.gov/cyberframework

A Cybersecurity Framework olyan általános keretrendszer, amely segít a szervezeteknek a kiberbiztonsági kockázatok kezelésében.

Fő funkciói:

- Govern
- Identify
- Protect
- Detect
- Respond
- Recover

A kézikönyv több fejezete is kapcsolódik ehhez a logikához.

### NIST SP 800-61 Rev. 3

Incident Response Recommendations and Considerations for Cybersecurity Risk Management

https://csrc.nist.gov/pubs/sp/800/61/r3/final

Ez a dokumentum az incidenskezelés egyik legfontosabb szakmai forrása.

A 10. fejezetben elsősorban ezt használtam az incident response jelenlegi NIST-szemléletének bemutatásához.

### NIST Incident Response Project

https://csrc.nist.gov/projects/incident-response

További incidenskezelési dokumentumok és szakmai anyagok találhatók itt.

## 2. CISA

A Cybersecurity and Infrastructure Security Agency, röviden CISA, az Egyesült Államok kiberbiztonsági és infrastruktúravédelmi szervezete.

### Use Logging on Business Systems

https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

Jól érthető bevezetés a naplózás fontosságába.

A 6. és 7. fejezethez különösen hasznos volt.

### Cybersecurity Incident and Vulnerability Response Playbooks

https://www.cisa.gov/sites/default/files/2024-08/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf

Konkrét incidenskezelési folyamatokat és playbook szemléletet mutat be.

### Cybersecurity Information Sharing

https://www.cisa.gov/topic/cybersecurity-information-sharing

Kiberfenyegetési információk megosztásával kapcsolatos háttéranyagok.

A CTI-fejezethez használtam.

## 3. MITRE ATT&CK

A MITRE ATT&CK az egyik legfontosabb nyilvános tudásbázis a támadói viselkedések rendszerezésére.

Főoldal:

https://attack.mitre.org/

### Get Started

https://attack.mitre.org/resources/

Kezdők számára jó kiindulópont.

### Enterprise Tactics

https://attack.mitre.org/tactics/

Az ATT&CK Enterprise taktikák listája.

### Data Sources

https://attack.mitre.org/datasources/

Azt mutatja be, milyen adatforrások lehetnek szükségesek egyes támadói technikák észleléséhez.

### CTI Training

https://attack.mitre.org/resources/training/cti/

Cyber Threat Intelligence és ATT&CK kapcsolatát bemutató oktatási anyag.

### ATT&CK Data and Tools

https://attack.mitre.org/resources/attack-data-and-tools/

Az ATT&CK adatformátumaihoz és eszközeihez kapcsolódó anyagok.

### Adversary Emulation Plans

https://attack.mitre.org/resources/adversary-emulation-plans/

Támadói viselkedések strukturált modellezésére szolgáló szakmai anyagok.

A handbookban ezt elsősorban szemléleti háttérként használtam.

## 4. Microsoft Learn

A Microsoft Learn különösen fontos forrás volt a Windows, PowerShell, Microsoft Sentinel és incidensvizsgálati részekhez.

Főoldal:

https://learn.microsoft.com/

### Windows Security Events

Például:

https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4624

A Windows eseményazonosítók értelmezéséhez használtam.

### Windows Event Log

https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log

A Windows naplózás működésének technikai háttere.

### PowerShell Logging

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging

A PowerShell naplózási lehetőségeit ismerteti.

### Microsoft Sentinel

https://learn.microsoft.com/en-us/azure/sentinel/

A SIEM, detektálási szabályok, incidensek és triage bemutatásához az egyik legfontosabb forrás volt.

### Scheduled Analytics Rules

https://learn.microsoft.com/en-us/azure/sentinel/scheduled-rules-overview

A SIEM detektálási szabályok felépítéséhez nyújt részletes háttéranyagot.

### Incident Investigation

https://learn.microsoft.com/en-us/azure/sentinel/investigate-incidents

A riasztások, entitások és incidensek vizsgálatát mutatja be.

## 5. Ubuntu dokumentáció

A Linux-fejezethez az Ubuntu hivatalos dokumentációját is használtam.

### User Management

https://ubuntu.com/server/docs/how-to/security/user-management/

Felhasználók, jogosultságok és `sudo` használata.

### OpenSSH Server

https://ubuntu.com/server/docs/how-to/security/openssh-server/

SSH beállítások és biztonsági alapok.

### Security Suggestions

https://ubuntu.com/server/docs/explanation/security/security_suggestions/

Általános Linux szerverbiztonsági ajánlások.

## 6. IETF

Az **Internet Engineering Task Force**, röviden IETF, az internetes szabványok egyik legfontosabb forrása.

A hálózati alapok fejezethez több RFC-dokumentumot használtam.

### TCP — RFC 9293

https://datatracker.ietf.org/doc/html/rfc9293

### IPv6 — RFC 8200

https://datatracker.ietf.org/doc/html/rfc8200

### DNS — RFC 1034

https://datatracker.ietf.org/doc/html/rfc1034

### DNS — RFC 1035

https://datatracker.ietf.org/doc/html/rfc1035

### HTTP Semantics — RFC 9110

https://datatracker.ietf.org/doc/html/rfc9110

Ezek technikai dokumentumok, ezért kezdőként nem szükséges teljes egészében elolvasni őket.

Elsősorban fogalmak ellenőrzésére hasznosak.

## 7. Sigma Detection Format

A Sigma egy nyílt, gyártófüggetlen detektálási szabályformátum.

Főoldal:

https://sigmahq.io/

### Documentation

https://sigmahq.io/docs/

### Sigma Rules

https://sigmahq.io/docs/basics/rules.html

A 12. fejezetben a Sigma segítségével mutattam be, hogyan lehet detektálási logikát strukturált formában leírni.

## 8. FIRST és TLP

A **Forum of Incident Response and Security Teams**, röviden FIRST, több nemzetközi kiberbiztonsági együttműködés és szabvány gazdája.

### Traffic Light Protocol 2.0

https://www.first.org/tlp/

A TLP azt jelzi, milyen körben osztható meg egy információ.

A CTI-fejezetben szereplő jelölések:

- TLP:RED
- TLP:AMBER
- TLP:GREEN
- TLP:CLEAR

## 9. CERT-EU

A CERT-EU az Európai Unió intézményeinek és szervezeteinek kiberbiztonsági közösségét támogatja.

### Cyber Threat Intelligence Framework

https://www.cert.europa.eu/publications/threat-intelligence/cyber-threat-intelligence-framework/

A CTI folyamat, elemzés, bizonytalanság és confidence kezeléséhez használtam.

## 10. Nemzeti Kiberbiztonsági Intézet

A **Nemzeti Kiberbiztonsági Intézet**, röviden NKI, a projekt egyik legfontosabb magyar nyelvű forrása.

Főoldal:

https://nki.gov.hu/

Az NKI előnye, hogy:

- magyar nyelvű
- hazai környezethez kapcsolódik
- gyakorlati riasztásokat közöl
- sérülékenységeket és aktuális fenyegetéseket is bemutat

### Incidenskezelés

https://nki.gov.hu/szolgaltatasok/tartalom/incidenskezeles/

### Eseménynaplózás

https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

### CTI és OpenCTI

https://nki.gov.hu/it-biztonsag/tanacsok/egy-ingyenes-nyilt-forrasu-cti-cyber-threat-intelligence-platform/

### Ransomware

https://nki.gov.hu/figyelmeztetesek/riasztas/riasztas-zsarolovirus-ransomware-tamadasokkal-kapcsolatban/

### Linux és sudo sérülékenységek

https://nki.gov.hu/it-biztonsag/hirek/kritikus-sebezhetosegek-a-sudo-parancssori-eszkozben-jogosultsagkiterjesztes-veszelye-fenyegeti-a-linux-rendszereket/

Az NKI oldalán a témák gyorsan változnak, ezért mindig érdemes a legfrissebb figyelmeztetéseket is ellenőrizni.

## 11. Nemzeti Közszolgálati Egyetem

A magyar szakirodalom egyik fontos forrása volt:

### Az információbiztonság alapjai

Gyaraki Réka szerk.

Nemzeti Közszolgálati Egyetem, 2023

https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

A kötet átfogó magyar nyelvű bevezetést ad többek között:

- információbiztonsági alapfogalmakhoz
- kockázatkezeléshez
- szervezeti biztonsághoz
- hálózati és rendszerbiztonsághoz

A handbook több fejezetében is háttérforrásként használtam.

## 12. MISP

A **MISP**, vagyis Malware Information Sharing Platform, nyílt forrású threat intelligence platform.

https://www.misp-project.org/

A rendszer lehetővé teszi:

- IoC-k tárolását
- fenyegetési információk megosztását
- kapcsolatok kezelését
- strukturált CTI-adatcserét

A CTI tanulásának következő lépéseként érdemes lehet megismerni.

## 13. OpenCTI

Az OpenCTI egy nyílt forrású Cyber Threat Intelligence platform.

https://filigran.io/solutions/opencti/

Segíthet:

- threat actorok rendszerezésében
- IoC-k kezelésében
- ATT&CK technikák kapcsolásában
- CTI-adatok vizualizálásában

Az NKI magyar nyelvű bemutatót is készített róla.

## 14. Kiegészítő tanulási források

A hivatalos dokumentáció mellett gyakorlati oktatási környezetek is hasznosak lehetnek.

Ilyenek például:

- Microsoft Learn tanulási modulok
- CyberDefenders
- Blue Team Labs Online
- TryHackMe blue team tananyagok
- LetsDefend
- MITRE ATT&CK training

Ezek használatakor érdemes mindig ellenőrzött, jogszerű gyakorlókörnyezetben dolgozni.

## 15. Hogyan értékeljünk egy forrást?

Nem minden internetes kiberbiztonsági tartalom egyformán megbízható.

Egy forrásnál érdemes megkérdezni:

1. Ki publikálta?
2. Hivatalos szervezet vagy ismert szakmai szereplő?
3. Mikor frissítették?
4. Hivatkozik elsődleges forrásra?
5. Más megbízható forrás megerősíti?
6. Tényeket közöl vagy véleményt?
7. Egyértelműen jelzi a bizonytalanságot?

## 16. Elsődleges és másodlagos források

### Elsődleges forrás

Az eredeti dokumentum vagy adat.

Példák:

- NIST szabvány
- Microsoft dokumentáció
- MITRE ATT&CK technikaoldal
- IETF RFC
- CISA advisory

### Másodlagos forrás

Az elsődleges forrást magyarázza vagy összefoglalja.

Például:

- szakmai blog
- tankönyv
- oktatási cikk
- híroldal

A handbookban lehetőség szerint elsődleges forrásokat használtam, és ezeket magyar nyelvű szakmai anyagokkal egészítettem ki.

## 17. Miért fontos a frissesség?

A kiberbiztonság gyorsan változik.

Változhat:

- egy termék működése
- egy Event ID dokumentációja
- egy MITRE ATT&CK technika
- egy SIEM-funkció
- egy sérülékenység állapota
- egy támadási kampány

Ezért a kézikönyv használatakor mindig érdemes az eredeti forrás aktuális változatát is ellenőrizni.

## 18. A források szerepe ebben a projektben

A források használatának célja az volt, hogy a repository ne csak saját jegyzetek gyűjteménye legyen.

A kutatómunka segítségével:

- a fogalmak ellenőrizhetőek
- a szakmai állítások visszakereshetőek
- a fejezetek továbbtanulási lehetőséget adnak
- a repository szakmailag megalapozottabb
- a projekt később könnyebben frissíthető

## 19. Ajánlott tanulási sorrend

Ha valaki a kézikönyv után tovább szeretne tanulni, egy lehetséges sorrend:

```text
1. NIST CSF
2. Windows és Linux naplózás
3. Microsoft Sentinel vagy más SIEM
4. MITRE ATT&CK
5. Sigma
6. CTI
7. Incident Response
8. Gyakorlati blue team laborok
```

Nem szükséges mindent egyszerre megtanulni.

## 20. Záró megjegyzés

A kiberbiztonságban nincs olyan kézikönyv, amely hosszú időre teljesen kész marad.

Új technológiák, új támadási módszerek és új védelmi megoldások jelennek meg.

Ezért ezt a repository-t inkább folyamatosan bővíthető tanulási projektnek tekintem.

A cél nem az volt, hogy szakértői szintű enciklopédiát készítsek.

A cél egy olyan kezdőbarát kézikönyv létrehozása volt, amely:

- segít rendszerezni az alapokat
- támogatja a további tanulást
- megmutatja, hol találhatók megbízható szakmai források
- később új fejezetekkel és gyakorlati példákkal továbbfejleszthető

---

[← Előző fejezet](14-cheat-sheet.md) | [Vissza a tartalomjegyzékhez](README.md)
