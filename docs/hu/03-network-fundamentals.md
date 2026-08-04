# 03 — Hálózati alapismeretek

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/03-network-fundamentals.md)

## Bevezetés

Ebben a fejezetben azokat a hálózati alapfogalmakat foglalom össze, amelyek a források alapján hasznosak lehetnek egy kezdő SOC-elemző számára.

A fejezethez nemcsak nemzetközi protokoll-leírásokat, hanem magyar nyelvű oktatási anyagokat is felhasználtam. A Nemzeti Kiberbiztonsági Intézet *Informatikai behatolások és felismerésük* című anyaga a hálózati modellek, protokollok és támadási minták kapcsolatát is bemutatja.

A cél nem a teljes hálózati szakanyag bemutatása. Inkább annak megértése, hogy az IP-címek, portok, protokollok és hálózati naplók hogyan jelennek meg egy biztonsági vizsgálat során.

## 1. Az OSI-modell

Az OSI-modell hét rétegben írja le a hálózati kommunikációt.

| Réteg | Megnevezés | Példa |
|---:|---|---|
| 7 | Alkalmazási | HTTP, DNS, SMTP |
| 6 | Megjelenítési | kódolás, titkosítás |
| 5 | Viszony | munkamenetek kezelése |
| 4 | Szállítási | TCP, UDP |
| 3 | Hálózati | IPv4, IPv6, ICMP |
| 2 | Adatkapcsolati | Ethernet, MAC-cím |
| 1 | Fizikai | kábel, rádiójel |

A modell segíthet abban, hogy egy hálózati problémát vagy gyanús eseményt rétegenként vizsgáljunk.

## 2. A TCP/IP-modell

A TCP/IP-modell egyszerűbb felosztást használ.

| TCP/IP-réteg | Példák |
|---|---|
| Alkalmazási | HTTP, DNS, SMTP, SSH |
| Szállítási | TCP, UDP |
| Internet | IPv4, IPv6, ICMP |
| Hálózati hozzáférés | Ethernet, Wi-Fi, ARP |

A kommunikáció során az adat minden rétegen új információt kap. Ezt kapszulázásnak nevezik.

## 3. IP-címek

Az IP-cím egy hálózati interface logikai címe.

### IPv4

Példa:

```text
192.168.1.25
```

Gyakori privát tartományok:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

### IPv6

Példa:

```text
2001:db8:85a3::8a2e:370:7334
```

Az IPv6 nagyobb címtartományt biztosít. Egy SOC számára fontos lehet az IPv4 és az IPv6 forgalom figyelése is.

## 4. Alhálózatok

A CIDR (Classless Inter-Domain Routing) jelölés azt mutatja meg, hogy egy IP-cím hány bitje tartozik a hálózati részhez, és ez alapján meghatározható, mely része azonosítja a hálózatot, illetve mely része az állomást (hostot).

Példa:

192.168.1.25/24

A /24 azt jelenti, hogy az első 24 bit a hálózati rész.

Hálózati maszkja: 255.255.255.0

Hálózati cím: 192.168.1.0

Host rész: az utolsó 8 bit (például a 25)


## 5. MAC-cím és ARP

A MAC-cím (Media Access Control address) a hálózati interface hardveres azonosítója, ezért gyakran fizikai címnek is nevezik. Az adatkapcsolati rétegben (OSI 2. réteg) használják arra, hogy az eszközök egy helyi hálózaton azonosítani tudják egymást.

Példa:

```text
00:1A:2B:3C:4D:5E
```
Az ARP (Address Resolution Protocol) egy hálózati protokoll, amelynek feladata, hogy a helyi hálózaton egy IPv4-címhez megtalálja a hozzá tartozó MAC-címet.
Az ARP az IPv4-címeket kapcsolja össze a helyi hálózaton használt MAC-címekkel.

ARP spoofing esetén egy támadó hamis ARP-válaszokat küldhet.

Lehetséges jelek:

- egy IP-címhez váratlanul új MAC-cím tartozik
- több IP-cím ugyanahhoz a MAC-címhez kapcsolódik
- megváltozik az alapértelmezett átjáró
- kapcsolatmegszakadások jelennek meg

## 6. TCP és UDP

### A TCP (Transmission Control Protocol) egy kapcsolatközpontú szállítási rétegbeli protokoll. Mielőtt adatot küldene, megbízható kapcsolatot hoz létre a két végpont között.

A kapcsolat létrehozása a háromutas kézfogással történik:

Kliens → Szerver: SYN
„Kapcsolódni szeretnék.”
A kliens elküldi a saját kezdő sorszámát (Initial Sequence Number, ISN).

Szerver → Kliens: SYN-ACK
„Elfogadom a kapcsolatot, és nyugtázom a kérésed.”
A szerver elküldi a saját kezdő sorszámát, és visszaigazolja a kliensét.

Kliens → Szerver: ACK
„Megkaptam a válaszodat.”
A kapcsolat létrejön, és elkezdődhet az adatátvitel.

### UDP

Az UDP kapcsolat nélküli protokoll.

Nincs háromutas kézfogás, és nincs garantált kézbesítés.

Gyakran használja:

- DNS
- DHCP
- hang- és videóforgalom
- egyes VPN-megoldások

## 7. Portok

A portszám segít azonosítani, melyik szolgáltatás fogadja a kapcsolatot.

Port	     
Szolgáltatás	                          
Rövid leírás


22	         SSH (Secure Shell)	                           Titkosított távoli bejelentkezés és parancsvégrehajtás

25	         SMTP (Simple Mail Transfer Protocol)	         E-mail küldés levelezőszerverek között

53	         DNS (Domain Name System)	                     Domainnevek feloldása IP-címekké

80	         HTTP (Hypertext Transfer Protocol)	            Titkosítás nélküli webforgalom

123	      NTP (Network Time Protocol)	                  Hálózati időszinkronizáció

389	      LDAP (Lightweight Directory Access Protocol)	   Címtárszolgáltatások elérése

443	      HTTPS (HTTP Secure)	                           Titkosított webforgalom TLS/SSL használatával

445	      SMB (Server Message Block)	                     Fájl- és nyomtatómegosztás Windows hálózatokon

3389	      RDP (Remote Desktop Protocol)	                  Távoli asztali kapcsolat Windows rendszereken

A portszám önmagában nem bizonyítja, milyen alkalmazás használja a kapcsolatot.

Gyanús lehet például:

- RDP-kapcsolat ismeretlen külső címről
- SMB-forgalom az internet felé
- sok célport rövid idő alatt
- ritka porton tartós külső kapcsolat

## 8. DNS

A DNS neveket kapcsol IP-címekhez.

Példa:

```text
example.com → 93.184.216.34
```

Gyakori rekordok:

| Rekord | Funkció |
|---|---|
| A | IPv4-cím |
| AAAA | IPv6-cím |
| CNAME | álnév |
| MX | levelezőszerver |
| NS | névszerver |
| TXT | szöveges adat |
| PTR | IP-címhez tartozó név |

Gyanús DNS-minták lehetnek:

- nagyon hosszú domainnevek
- sok véletlenszerűnek tűnő aldomain
- sok sikertelen lekérdezés
- ismert rosszindulatú domain
- szokatlan mennyiségű TXT-lekérdezés

Ezek önmagukban nem bizonyítanak támadást, de további vizsgálatot indokolhatnak.

Az NKI DNS-biztonságról szóló magyar nyelvű összefoglalói arra is felhívják a figyelmet, hogy a DNS eredeti működése több biztonsági és adatvédelmi kihívást tartalmaz. A DNSSEC, a DNS over HTTPS és más megoldások különböző módon próbálják csökkenteni ezeket a problémákat.

## 9. DHCP

A DHCP (Dynamic Host Configuration Protocol) egy hálózati protokoll, amely automatikusan kiosztja az eszközök számára a szükséges hálózati beállításokat.

Ahelyett, hogy minden számítógépen, telefonon vagy nyomtatón kézzel kellene beállítani az IP-címet, a DHCP-szerver automatikusan elvégzi ezt.

Például:

- IP-cím
- alhálózati maszk
- alapértelmezett átjáró
- DNS-szerver

DORA a DHCP-címkiosztás négy lépésének rövidítése:

D – Discover (Felderítés)

A DHCP-kliens (például egy számítógép vagy telefon) még nem rendelkezik IP-címmel.
Egy broadcast üzenetet küld a hálózatra, hogy DHCP-szervert keressen.
Üzenet: DHCP Discover

O – Offer (Ajánlat)
A DHCP-szerver válaszol a kliensnek.
Felajánl egy szabad IP-címet és a hozzá tartozó hálózati beállításokat.
Üzenet: DHCP Offer

R – Request (Kérés)
A kliens kiválasztja az egyik DHCP-ajánlatot (ha több szerver válaszolt).
Jelzi a szervernek, hogy elfogadja az ajánlott IP-címet.
Üzenet: DHCP Request

A – Acknowledge (Nyugtázás)
A DHCP-szerver megerősíti az IP-cím kiosztását.
A kliens ezután használhatja az IP-címet a megadott bérleti idő alatt.
Üzenet: DHCP ACK

Egyszerűen:

Kliens → DHCP Discover → Szerver

Szerver → DHCP Offer → Kliens

Kliens → DHCP Request → Szerver

Szerver → DHCP ACK → Kliens

A DORA-folyamat után az eszköz teljes értékű hálózati kapcsolatot tud létrehozni.

Egy jogosulatlan DHCP-szerver hibás átjárót vagy DNS-szervert adhat a klienseknek.

## 10. ICMP

Az ICMP hálózati állapot- és hibaüzenetek továbbítására szolgál.


Az ICMP segíthet:

- az elérhetőség ellenőrzésében
- útvonalproblémák felismerésében
- hibák jelzésében

Szokatlan ICMP-forgalom felderítéshez vagy tunnelhez is kapcsolódhat.

## 11. HTTP és HTTPS

A HTTP webes kommunikációhoz használt protokoll.

Gyakori metódusok:

- GET
- POST
- PUT
- DELETE

Gyakori állapotkódok:

| Kód | Jelentés |
|---:|---|
| 200 | sikeres kérés |
| 301 | átirányítás |
| 400 | hibás kérés |
| 401 | hitelesítés szükséges |
| 403 | hozzáférés megtagadva |
| 404 | nem található |
| 500 | szerverhiba |

A HTTPS a HTTP-forgalmat titkosított kapcsolaton továbbítja.

A tartalom titkosított lehet, de egyes metaadatok továbbra is láthatók.

Például:

- forrás- és cél-IP
- kapcsolat időpontja
- kapcsolat időtartama
- adatforgalom mennyisége

## 12. NAT

A NAT belső és külső IP-címek közötti címfordítást végez.

Egy nyilvános IP-cím mögött több belső eszköz is lehet.

Vizsgálatkor ezért szükség lehet:

- NAT-naplókra
- tűzfalnaplókra
- forrásportokra
- pontos időbélyegekre
- DHCP-adatokra

## 13. Egyszerű SOC-példa

Egy munkaállomás ötpercenként kapcsolódik ugyanahhoz a külső IP-címhez a 443-as porton.

Ez lehet normál frissítési folyamat, de lehet gyanús kommunikáció is.

Az elemző ellenőrizheti:

1. melyik folyamat indítja a kapcsolatot
2. melyik domain tartozik az IP-címhez
3. ismert-e a cél a szervezetben
4. más eszközökön is látható-e
5. szabályos időközönként ismétlődik-e
6. mekkora az adatforgalom
7. van-e kapcsolódó riasztás

A rendszeresen ismétlődő kapcsolatot beaconingnek nevezhetik.


## 14. Összefoglalás

Egy kezdő SOC-elemző számára hasznos az alábbi fogalmak megértése:

- IP-cím
- TCP és UDP
- port
- DNS
- DHCP
- ARP
- ICMP
- HTTP és HTTPS
- NAT

A cél nem minden hálózati részlet megtanulása, hanem annak felismerése, hogy egy esemény normálisnak vagy szokatlannak tűnik-e.


## Források

1. IETF RFC 9293: Transmission Control Protocol  
   https://datatracker.ietf.org/doc/html/rfc9293

2. IETF RFC 8200: Internet Protocol, Version 6 Specification  
   https://datatracker.ietf.org/doc/html/rfc8200

3. IETF RFC 1034: Domain Names, Concepts and Facilities  
   https://datatracker.ietf.org/doc/html/rfc1034

4. IETF RFC 1035: Domain Names, Implementation and Specification  
   https://datatracker.ietf.org/doc/html/rfc1035

5. IETF RFC 9110: HTTP Semantics  
   https://datatracker.ietf.org/doc/html/rfc9110

6. MITRE ATT&CK: Network Traffic  
   https://attack.mitre.org/datasources/DS0029/

7. Nemzeti Kiberbiztonsági Intézet  
   **Informatikai behatolások és felismerésük**  
   https://nki.gov.hu/wp-content/uploads/2019/07/04-Informatikai-behatol%C3%A1sok-%C3%A9s-felismer%C3%A9s%C3%BCk.pdf

8. Nemzeti Kiberbiztonsági Intézet  
   **DNS biztonsági és adatvédelmi technológiák előnyei és hátrányai**  
   https://nki.gov.hu/it-biztonsag/tanacsok/dns-biztonsagi-es-adatvedelmi-technologiak-elonyei-es-hatranyai/

9. Nemzeti Kiberbiztonsági Intézet  
   **Egyes népszerű DNS biztonsági és adatvédelmi technológiák főbb jellemzőinek összehasonlítása**  
   https://nki.gov.hu/it-biztonsag/tudastar/egyes-nepszeru-dns-biztonsagi-es-adatvedelmi-technologiak-fobb-jellemzoinek-osszehasonlitasa/

10. Gyaraki Réka szerk.  
    **Az információbiztonság alapjai**  
    Nemzeti Közszolgálati Egyetem, 2023  
    https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](02-how-a-soc-works.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](04-windows-security.md)
