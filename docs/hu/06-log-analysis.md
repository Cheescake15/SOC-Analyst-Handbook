# 06 — Naplóelemzés

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/06-log-analysis.md)

## Bevezetés

A számítógépek, szerverek, alkalmazások és hálózati eszközök folyamatosan feljegyzik, mi történik velük. Ezeket a feljegyzéseket naplóknak, angolul logoknak nevezzük.

Egyetlen naplóbejegyzés gyakran csak egy apró részlet. Több bejegyzést időrendbe rendezve viszont kirajzolódhat egy teljes történet.

Ebben a fejezetben kezdő szinten mutatom be, mi a naplóelemzés, milyen adatokat érdemes keresni, és hogyan lehet egy eseménysort egyszerűen értelmezni.

## 1. Mi az a napló?

A napló egy rendszer által automatikusan létrehozott feljegyzés.

Egyszerű hasonlattal olyan, mint egy digitális eseménynapló.

Egy bejegyzés megmutathatja:

- mikor történt valami
- melyik rendszerben történt
- melyik felhasználó érintett
- milyen program futott
- sikeres vagy sikertelen volt-e a művelet
- milyen IP-cím kapcsolódott hozzá

Példa:

```text
2026-08-06 08:14:22
User: andrea
Action: Login
Result: Failed
Source IP: 203.0.113.24
```

## 2. Miért fontosak a naplók?

A naplók segíthetnek:

- hibák felismerésében
- felhasználói tevékenység ellenőrzésében
- támadások észlelésében
- incidensek kivizsgálásában
- események időrendjének összeállításában
- bizonyítékok megőrzésében

A CISA és a Nemzeti Kiberbiztonsági Intézet anyagai is kiemelik, hogy megfelelő naplózás nélkül nehéz megérteni, mi történt egy rendszerben.

## 3. Gyakori naplóforrások

- Windows
- Linux
- tűzfal
- router
- VPN
- DNS-szerver
- webszerver
- levelezőrendszer
- vírusvédelem
- EDR
- felhőszolgáltatás
- adatbázis
- üzleti alkalmazás

Egy vizsgálat során gyakran több forrás adatait kell összevetni.

## 4. Egy naplóbejegyzés fontos mezői

### Időbélyeg

Megmutatja, mikor történt az esemény.

```text
2026-08-06T08:14:22+02:00
```

Az időzóna is fontos. Az egyik rendszer használhat helyi időt, a másik UTC-időt.

### Felhasználó

```text
User: admin
```

### Forrás- és célcím

```text
Source IP: 198.51.100.17
Destination IP: 10.0.0.25
Destination Port: 22
```

### Eseménytípus

```text
Login failed
File created
Service started
Connection blocked
```

### Eredmény

```text
Result: Success
```

## 5. Strukturált és nem strukturált naplók

### Strukturált napló

Jól elkülönített mezőket tartalmaz.

```json
{
  "time": "2026-08-06T08:14:22Z",
  "user": "andrea",
  "action": "login",
  "result": "failed",
  "source_ip": "203.0.113.24"
}
```

### Nem strukturált napló

Inkább szöveges mondat.

```text
Failed password for andrea from 203.0.113.24 port 52311 ssh2
```

A strukturált adat általában könnyebben kereshető.

## 6. Mit jelent a normalizálás?

A különböző rendszerek ugyanazt az adatot más néven tárolhatják.

```text
src_ip
source_ip
client_ip
remote_address
```

Mindegyik jelentheti a forrás IP-címét.

A **normalizálás** során ezeket egységes mezőnévre alakítják. A SIEM-rendszerek gyakran elvégzik ezt a feladatot.

## 7. Idővonal készítése

A naplóelemzés egyik legfontosabb lépése az események időrendbe rendezése.

```text
09:02 — sikertelen bejelentkezés
09:03 — sikertelen bejelentkezés
09:04 — sikeres bejelentkezés
09:06 — fájlletöltés
09:08 — PowerShell elindítása
09:10 — kapcsolat ismeretlen külső címhez
```

Külön-külön egyik esemény sem feltétlenül bizonyít támadást. Együtt viszont már egy vizsgálandó eseménysort mutatnak.

## 8. Keresés és szűrés

Nagy rendszerben rengeteg naplóbejegyzés keletkezhet.

Gyakori szűrési feltételek:

- időszak
- felhasználónév
- IP-cím
- számítógépnév
- eseménytípus
- hibakód
- folyamatnév
- port
- eredmény

Példa:

```text
Mutasd az admin felhasználó
sikertelen bejelentkezéseit
az elmúlt 24 órából.
```

A jó keresés egyértelmű kérdésből indul.

## 9. Mi számít gyanúsnak?

A gyanús nem ugyanaz, mint a bizonyítottan rosszindulatú.

Egy esemény érdekesebb lehet, ha:

- ritkán fordul elő
- szokatlan időpontban történik
- fontos fiókot érint
- ismeretlen IP-címhez kapcsolódik
- több rendszeren egyszerre jelenik meg
- más gyanús esemény követi

### Példa

Egy dolgozó minden hétköznap Budapestről jelentkezik be 8 és 9 óra között.

Egy vasárnap hajnali 3 órakor másik országból történő belépés szokatlan lehet.

Lehetséges magyarázat:

- utazás
- VPN használata
- hibás helymeghatározás
- kompromittált fiók

## 10. True positive és false positive

### True positive

A riasztás valódi biztonsági problémát jelez.

### False positive

A riasztás normális eseményt jelölt gyanúsnak.

### Benign true positive

A szabály helyesen ismerte fel a mintát, de a tevékenység engedélyezett volt.

Például egy jóváhagyott biztonsági teszt.

## 11. A kontextus szerepe

Példa:

```text
powershell.exe started
```

Ez lehet:

- normális rendszergazdai feladat
- szoftvertelepítés
- vállalati szkript
- támadói tevékenység

További kérdések:

- ki indította el
- melyik gépen futott
- milyen parancsot kapott
- mi volt a szülőfolyamata
- kapcsolódott-e külső címhez
- történt-e fájlmódosítás

## 12. Időszinkronizálás

Ha két rendszer órája eltér, az események rossz sorrendben jelenhetnek meg.

Az elemzőnek érdemes ellenőriznie:

- milyen időzónát használ a napló
- UTC vagy helyi idő szerepel-e
- pontos-e a rendszeróra
- történt-e óraátállítás

A rendszerek gyakran NTP-t használnak az idő szinkronizálására.

## 13. Naplómegőrzés és védelem

A naplók megőrzési idejét befolyásolhatja:

- tárhely
- jogszabály
- belső szabályzat
- üzleti igény
- incidensvizsgálati szükséglet
- adatvédelmi követelmény

A naplókat védeni is kell.

Fontos lehet:

- központi naplógyűjtés
- hozzáférések korlátozása
- mentés
- módosítások ellenőrzése
- naplózás leállásának észlelése

Egy támadó megpróbálhatja eltüntetni a nyomait, ezért a naplózás váratlan leállása is vizsgálandó.

## 14. Egyszerű vizsgálati példa

```text
14:21 — 15 sikertelen VPN-bejelentkezés
14:24 — sikeres VPN-bejelentkezés
14:27 — távoli asztali kapcsolat
14:30 — új rendszergazdai fiók
14:34 — naplózási szolgáltatás leállítása
```

Kezdő elemzőként érdemes megkérdezni:

1. melyik felhasználó érintett
2. honnan érkezett a kapcsolat
3. felismeri-e a felhasználó a belépést
4. ki hozta létre az új fiókot
5. milyen jogosultságot kapott
6. mi állította le a naplózást
7. történt-e más rendszeren hasonló esemény

## 15. Egyszerű elemzési módszer

1. Fogalmazd meg a kérdést.
2. Határozd meg az időszakot.
3. Gyűjtsd össze az érintett azonosítókat.
4. Keresd meg a kapcsolódó eseményeket.
5. Készíts idővonalat.
6. Válaszd szét az ismert és ismeretlen adatokat.
7. Dokumentáld a következtetést és a következő lépést.

## 16. Mit érdemes kezdőként megjegyezni?

- A napló egy rendszer által készített eseményfeljegyzés.
- Egyetlen bejegyzés ritkán ad teljes képet.
- Az időbélyeg és az időzóna nagyon fontos.
- Több adatforrást gyakran össze kell kapcsolni.
- A szokatlan esemény nem automatikusan támadás.
- A kontextus segít a helyes értelmezésben.
- A naplókat meg kell őrizni és védeni kell.
- Egy egyszerű idővonal sokat segíthet.

## 17. Ellenőrző kérdések

1. Mi az a napló?
2. Miért fontosak a naplók egy SOC számára?
3. Milyen mezőket tartalmazhat egy naplóbejegyzés?
4. Mi a különbség a strukturált és a nem strukturált napló között?
5. Mit jelent a normalizálás?
6. Miért fontos az idővonal?
7. Milyen mezők alapján lehet szűrni?
8. Mi a true positive?
9. Mi a false positive?
10. Mi a benign true positive?
11. Miért fontos a kontextus?
12. Miért szükséges az időszinkronizálás?
13. Mit jelent a naplómegőrzés?
14. Miért kell védeni a naplókat?
15. Mit tartalmazzon egy egyszerű vizsgálati dokumentáció?

## Források

1. Cybersecurity and Infrastructure Security Agency  
   **Use Logging on Business Systems**  
   https://www.cisa.gov/audiences/small-and-medium-businesses/secure-your-business/use-logging-on-business-systems

2. Microsoft Learn  
   **Event Viewer**  
   https://learn.microsoft.com/en-us/shows/inside/event-viewer

3. Microsoft Learn  
   **Windows Event Log**  
   https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log

4. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

5. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](05-linux-security.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](07-siem-fundamentals.md)
