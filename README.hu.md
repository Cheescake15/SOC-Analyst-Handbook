# SOC Analyst Kézikönyv

> Gyakorlati, kezdőbarát útmutató a Security Operations Center működéséhez, a naplóelemzéshez, a fenyegetések észleléséhez, az incidenskezeléshez és a Blue Team alapvető feladataihoz.

## A projektről

A **SOC Analyst Kézikönyv** oktatási és portfóliócélú projekt kiberbiztonsági hallgatók, pályakezdő SOC-elemzők és Blue Team iránt érdeklődők számára.

A repository két nyelven készül:

- [English documentation](docs/en/)
- [Magyar dokumentáció](docs/hu/)

Az angol változat segíti a szakmai angol nyelv fejlesztését és nemzetközi portfólióként is használható. A magyar változat biztosítja a fogalmak pontosabb megértését és a tananyag könnyebb feldolgozását.

## Tanulási célok

A kézikönyv feldolgozása után az olvasó képes lesz:

1. bemutatni egy SOC célját és működését;
2. megkülönböztetni a Tier 1, Tier 2 és Tier 3 feladatköröket;
3. értelmezni az alapvető hálózati protokollokat és forgalmi mintákat;
4. felismerni fontos Windows- és Linux-biztonsági eseményeket;
5. alapvető naplóelemzési feladatokat végrehajtani;
6. egyszerű SPL- és KQL-lekérdezéseket írni;
7. értelmezni Sigma- és YARA-szabályokat;
8. megkülönböztetni az IOC-kat és a támadói viselkedésmintákat;
9. eseményeket MITRE ATT&CK technikákhoz rendelni;
10. egy biztonsági incidenst dokumentálni és megfelelően eszkalálni.

## Repository-struktúra

```text
soc-analyst-handbook/
├── README.md
├── README.hu.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
├── docs/
│   ├── en/
│   └── hu/
├── diagrams/
├── images/
├── labs/
├── scripts/
└── detections/
    ├── sigma/
    ├── yara/
    ├── kql/
    └── spl/
```

## Fejezetek

| Sorszám | Fejezet | Főbb témák |
|---:|---|---|
| 01 | Bevezetés | SOC, Blue Team, elemzői szerepkörök, NOC és SOC |
| 02 | A SOC működése | Emberek, folyamatok, technológia, riasztási életciklus |
| 03 | Hálózati alapismeretek | OSI, TCP/IP, DNS, HTTP(S), DHCP, ARP, ICMP |
| 04 | Windows biztonság | Event Viewer, hitelesítés, folyamatok, szolgáltatások, PowerShell |
| 05 | Linux biztonság | Felhasználók, jogosultságok, sudo, naplók, systemd, cron |
| 06 | Naplóelemzés | Windows, Sysmon, webszerver-, tűzfal- és hitelesítési naplók |
| 07 | SIEM | Splunk, Microsoft Sentinel, Wazuh, QRadar |
| 08 | Threat Intelligence | IOC, IOA, TTP, CVE, CVSS, STIX, TAXII |
| 09 | MITRE ATT&CK | Taktikák, technikák és leképezés |
| 10 | Incidenskezelés | Felkészülés, észlelés, válasz, helyreállítás |
| 11 | Malware-alapok | Trójai, féreg, RAT, rootkit, ransomware, spyware |
| 12 | Detektálástervezés | Sigma, YARA, KQL, SPL |
| 13 | Laborok | Wireshark, Windows Logs, Sysmon, Splunk, Wazuh |
| 14 | Gyorssegédlet | Parancsok, Event ID-k, portok és lekérdezések |
| 15 | Hivatkozások | Szabványok, dokumentációk és további források |

## Etikus használat

A repository kizárólag oktatási, védekezési, engedélyezett vizsgálati és ellenőrzött laboratóriumi célokat szolgál.

Tilos engedély nélkül rendszerekhez hozzáférni, azokat vizsgálni, megfigyelni vagy módosítani. A felhasználó felelőssége a vonatkozó jogszabályok, szervezeti szabályzatok és szakmai etikai elvek betartása.

## Licenc

A repository oktatási tartalmai és kódpéldái — eltérő megjelölés hiányában — MIT licenc alatt érhetők el.
