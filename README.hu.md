# SOC Analyst Kézikönyv

[English](README.md) | [Magyar](README.hu.md)

> Kétnyelvű, gyakorlati kézikönyv leendő SOC-elemzők számára a biztonsági műveletek, a hálózatok, az operációs rendszerek védelme, a naplóelemzés, a SIEM, a threat intelligence, a MITRE ATT&CK, az incidenskezelés, a malware-ek és a detektálástervezés alapjairól.

## A projektről

A **SOC Analyst Kézikönyv** oktatási és portfóliócélú dokumentációs projekt kiberbiztonsági hallgatók és leendő Blue Team szakemberek számára.

A repository ugyanazt az alapvető tananyagot két nyelven tartalmazza:

- [English documentation](docs/en/)
- [Magyar dokumentáció](docs/hu/)

Az angol változat segíti a szakmai angol nyelv fejlesztését, és nemzetközi portfólióként is használható. A magyar változat támogatja a fogalmak pontos megértését és a tananyag könnyebb feldolgozását.

## Célközönség

A kézikönyv kiberbiztonsági hallgatóknak, leendő SOC-elemzőknek, pályakezdő Blue Team szakembereknek, kiberbiztonsági területre átlépő informatikusoknak és a biztonsági műveletek alapjai iránt érdeklődőknek szól.

## Tanulási célok

A kézikönyv feldolgozása után az olvasó képes lesz:

1. bemutatni egy Security Operations Center célját és alapvető felépítését;
2. megkülönböztetni a Tier 1, Tier 2 és Tier 3 elemzői feladatköröket;
3. értelmezni a legfontosabb hálózati protokollokat és forgalmi mintákat;
4. felismerni fontos Windows- és Linux-biztonsági eseményeket;
5. értelmezni gyakori naplóbejegyzéseket és gyanús tevékenységeket;
6. bemutatni a SIEM-rendszerek szerepét a biztonsági megfigyelésben;
7. megkülönböztetni a kompromittálódás indikátorait a támadói viselkedésmintáktól;
8. eseményeket MITRE ATT&CK technikákhoz rendelni;
9. ismertetni az incidenskezelés főbb szakaszait;
10. megérteni a malware-ek és a detektálástervezés alapjait.

## A repository felépítése

```text
SOC-Analyst-Handbook/
├── README.md
├── README.hu.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
└── docs/
    ├── en/
    └── hu/
```

## A kézikönyv fejezetei

| Sorszám | Fejezet | Főbb témák |
|---:|---|---|
| 01 | Bevezetés a biztonsági műveletekbe | SOC, Blue Team, elemzői szerepkörök, NOC és SOC |
| 02 | Hogyan működik egy SOC? | Emberek, folyamatok, technológia, riasztások és eszkaláció |
| 03 | Hálózati alapismeretek | OSI, TCP/IP, DNS, HTTP(S), DHCP, ARP és ICMP |
| 04 | Windows biztonság | Event Viewer, hitelesítés, folyamatok, szolgáltatások és PowerShell |
| 05 | Linux biztonság | Felhasználók, jogosultságok, sudo, naplók, systemd és cron |
| 06 | Naplóelemzés | Windows-, Sysmon-, webszerver-, tűzfal- és hitelesítési naplók |
| 07 | SIEM-alapismeretek | Splunk, Microsoft Sentinel, Wazuh és QRadar |
| 08 | Kiberfenyegetettségi hírszerzés | IOC, IOA, TTP, CVE, CVSS, STIX és TAXII |
| 09 | MITRE ATT&CK | Taktikák, technikák és események leképezése |
| 10 | Incidenskezelés | Felkészülés, észlelés, válaszadás, helyreállítás és fejlesztés |
| 11 | Malware-alapok | Trójaiak, férgek, RAT-ok, rootkitek, ransomware és spyware |
| 12 | Detektálástervezés | Sigma, YARA, KQL és SPL alapfogalmak |
| 13 | Gyakorlati példák | Irányított elemzési helyzetek és dokumentációs példák |
| 14 | SOC Analyst gyorssegédlet | Event ID-k, portok, parancsok és vizsgálati szempontok |
| 15 | Hivatkozások | Szabványok, hivatalos dokumentációk és további források |

## Dokumentációs alapelvek

- kezdőbarát, de szakmailag pontos megfogalmazás;
- gyakorlati példákkal támogatott magyarázatok;
- egységes szerkezet a két nyelvi változatban;
- elsősorban hivatalos és elsődleges források használata;
- a szakkifejezések kontextusban történő magyarázata;
- kizárólag védekezési és engedélyezett felhasználás;
- a külső forrásból származó információk megfelelő hivatkozása.

## A projekt állapota

- [x] Repository-struktúra
- [x] Magyar és angol README
- [x] Kétnyelvű fejezetstruktúra
- [ ] Magyar fejezetek kidolgozása
- [ ] Angol fejezetek kidolgozása
- [ ] Szakmai ellenőrzés
- [ ] Nyelvi ellenőrzés
- [ ] Végleges hivatkozásjegyzék

## Etikus használat

A repository kizárólag oktatási, védekezési, engedélyezett vizsgálati és ellenőrzött tanulási célokat szolgál.

Tilos engedély nélkül rendszerekhez hozzáférni, azokat megfigyelni, vizsgálni vagy módosítani.

## Közreműködés

Javaslatokat és javításokat szívesen fogadunk. Módosítás kezdeményezése előtt olvasd el a [CONTRIBUTING.md](CONTRIBUTING.md) fájlt.

## Licenc

A repository oktatási tartalmai — eltérő megjelölés hiányában — [MIT licenc](LICENSE) alatt érhetők el.

## Jogi nyilatkozat

A kézikönyv nem helyettesíti a gyártói dokumentációkat, a szervezeti eljárásrendeket, a jogi tanácsadást vagy a professzionális incidenskezelési útmutatókat.

## Szerző

Készítette Varga Lea kiberbiztonsági tanulási és portfólióprojektként.
