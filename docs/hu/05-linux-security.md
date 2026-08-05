# 05 — Linux biztonság

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/05-linux-security.md)

## Bevezetés

A Linux sok szerveren, felhőszolgáltatásban, hálózati eszközön és biztonsági rendszerben megtalálható. Emiatt egy SOC-elemző gyakran találkozhat Linuxból származó naplókkal és riasztásokkal.

Ebben a fejezetben azokat az alapfogalmakat foglalom össze, amelyek egy kezdő számára is érthetőek. A cél nem az, hogy rendszergazdai szintű Linux-tudást adjak. Inkább azt szeretném bemutatni, hol lehetnek fontos nyomok, és milyen egyszerű kérdéseket érdemes feltenni egy vizsgálat során.

## 1. Mi az a Linux?

A Linux egy operációs rendszer alapját adó nyílt forráskódú kernel.

A hétköznapi használatban a Linux szóval gyakran egy teljes operációs rendszert jelölünk, például:

- Ubuntu
- Debian
- Fedora
- Red Hat Enterprise Linux
- Kali Linux
- Rocky Linux
- AlmaLinux

Ezeket Linux-disztribúcióknak nevezik.

A különböző disztribúciók sok mindenben hasonlítanak egymásra, de a parancsok, a csomagkezelés és a naplók helye eltérhet.

## 2. Miért fontos a Linux egy SOC-ban?

Linux-rendszereken gyakran futnak:

- webszerverek
- adatbázisok
- fájlszerverek
- felhőszolgáltatások
- konténerek
- hálózati szolgáltatások
- biztonsági eszközök

Egy Linux-rendszeren a következő események lehetnek érdekesek:

- sikeres és sikertelen bejelentkezések
- új felhasználói fiókok
- jogosultságváltozások
- `sudo` használata
- szolgáltatások indítása és leállítása
- ütemezett feladatok
- új vagy módosított fájlok
- hálózati kapcsolatok
- szoftverfrissítések
- biztonsági hibák kihasználására utaló jelek

## 3. A terminál és a shell

A **terminál** egy olyan felület, ahol szöveges parancsokat lehet kiadni.

A **shell** az a program, amely értelmezi ezeket a parancsokat.

Gyakori shell például:

```text
bash
zsh
sh
```

Egyszerű parancs:

```bash
pwd
```

Ez megmutatja, melyik könyvtárban vagyunk.

A terminál használata önmagában nem gyanús. Rendszergazdák és felhasználók is rendszeresen használják.

## 4. Felhasználók és csoportok

Linuxban minden folyamat és fájl valamilyen felhasználóhoz és csoporthoz kapcsolódik.

Néhány gyakori fióktípus:

- normál felhasználó
- rendszergazdai jogosultságot használó felhasználó
- szolgáltatásfiók
- root felhasználó

A **root** a legmagasabb jogosultságú fiók.

Egyszerű hasonlattal a root olyan, mint egy épület főkulcsa. Szinte mindenhez hozzáfér.

Ezért a root fiók használata különösen érzékeny biztonsági szempontból.

### Hasznos parancsok

Az aktuális felhasználó megtekintése:

```bash
whoami
```

A bejelentkezett felhasználók megtekintése:

```bash
who
```

A felhasználó csoportjainak megtekintése:

```bash
groups
```

## 5. Mi az a sudo?

A `sudo` segítségével egy engedélyezett felhasználó magasabb jogosultsággal hajthat végre egy parancsot.

Példa:

```bash
sudo apt update
```

Ez Ubuntu vagy Debian rendszeren frissíti a csomaglistát.

A `sudo` használata nem jelenti automatikusan azt, hogy valami rosszindulatú történt. Rendszergazdák gyakran használják.

Biztonsági szempontból érdekesebb lehet, ha:

- szokatlan felhasználó használja
- munkaidőn kívül történik
- ritkán használt vagy veszélyes parancs követi
- több sikertelen `sudo` próbálkozás látható
- egy szolgáltatásfiók próbál adminisztrátori parancsot futtatni

Az Ubuntu hivatalos dokumentációja is kiemeli, hogy a `sudo` jogosultságot csak szükség esetén szabad használni.

A Nemzeti Kiberbiztonsági Intézet több olyan sérülékenységről is beszámolt, amely a `sudo` eszközt érintette. Ez jól mutatja, hogy egy alapvető rendszereszköz biztonsági hibája komoly kockázatot jelenthet.

## 6. Fájlok és jogosultságok

Linuxban minden fájlhoz és könyvtárhoz jogosultságok tartoznak.

A három alapvető jogosultság:

- `r` = read, vagyis olvasás
- `w` = write, vagyis írás
- `x` = execute, vagyis végrehajtás

A jogosultságok három csoportra vonatkoznak:

- tulajdonos
- csoport
- mindenki más

Példa:

```text
-rwxr-x---
```

Egyszerűen értelmezve:

- a tulajdonos olvashatja, módosíthatja és futtathatja
- a csoport olvashatja és futtathatja
- más felhasználók nem férnek hozzá

### Hasznos parancs

```bash
ls -l
```

Ez megmutatja a fájlok jogosultságait, tulajdonosát és csoportját.

### Biztonsági jelentőség

Gyanús lehet, ha:

- érzékeny fájl mindenki számára írható
- egy fontos konfigurációs fájl tulajdonosa megváltozik
- egy korábban nem futtatható fájl végrehajthatóvá válik
- ismeretlen program jelenik meg rendszerkönyvtárban

## 7. Fontos könyvtárak

A Linux fájlrendszere több fontos könyvtárból áll.

| Könyvtár | Egyszerű jelentés |
|---|---|
| `/home` | felhasználók saját fájljai |
| `/etc` | rendszer- és programbeállítások |
| `/var/log` | sok rendszer naplófájljai |
| `/tmp` | ideiglenes fájlok |
| `/usr/bin` | sok futtatható program |
| `/bin` | alapvető parancsok |
| `/root` | a root felhasználó saját könyvtára |
| `/proc` | futó folyamatokkal és kernellel kapcsolatos adatok |

A `/tmp` könyvtár különösen érdekes lehet, mert minden felhasználó számára elérhető ideiglenes terület. Normális programok is használják, de támadók is helyezhetnek el itt fájlokat.

## 8. Linux-naplók

A naplók helye disztribúciónként eltérhet.

Gyakori naplófájlok:

```text
/var/log/auth.log
/var/log/secure
/var/log/syslog
/var/log/messages
```

### auth.log vagy secure

Ezekben gyakran hitelesítési események találhatók.

Például:

- sikeres SSH-bejelentkezés
- sikertelen bejelentkezés
- `sudo` használata
- felhasználóváltás

Ubuntu és Debian rendszereken gyakori az `/var/log/auth.log`.

Red Hat alapú rendszereken gyakori a `/var/log/secure`.

### syslog vagy messages

Általános rendszereseményeket tartalmazhatnak.

Például:

- szolgáltatások hibái
- rendszerüzenetek
- hardverrel kapcsolatos események
- alkalmazások üzenetei

A pontos naplóhelyet mindig az adott disztribúció dokumentációja alapján érdemes ellenőrizni.

## 9. journalctl

A modern Linux-rendszerek gyakran a `systemd-journald` szolgáltatást használják a naplók gyűjtésére.

A `journalctl` parancs segítségével ezek a naplók lekérdezhetők.

Az összes elérhető bejegyzés megtekintése:

```bash
journalctl
```

A legutóbbi bejegyzések:

```bash
journalctl -n 20
```

Egy szolgáltatás naplói:

```bash
journalctl -u ssh
```

A jelenlegi rendszerindítás eseményei:

```bash
journalctl -b
```

A hibaszintű események:

```bash
journalctl -p err
```

A Microsoft Azure Linux dokumentációja is a `journalctl` használatát javasolja a kernel, a szolgáltatások és az alkalmazások eseményeinek lekérdezésére.

## 10. SSH

Az **SSH**, vagyis Secure Shell, titkosított távoli hozzáférést biztosít.

Gyakran a 22-es portot használja.

Példa:

```bash
ssh user@server.example
```

Az SSH teljesen normális adminisztrációs eszköz.

Gyanús lehet, ha:

- sok sikertelen bejelentkezés történik
- ismeretlen külső IP-címről érkezik kapcsolat
- root fiókkal próbálnak belépni
- szokatlan időpontban történik sikeres belépés
- a belépés után ismeretlen program indul
- új SSH-kulcs kerül az `authorized_keys` fájlba

Az Ubuntu dokumentációja külön felhívja a figyelmet az `authorized_keys` fájl megfelelő jogosultságaira.

## 11. Folyamatok

A folyamat egy futó program vagy programrész.

Futó folyamatok megtekintése:

```bash
ps aux
```

Interaktív folyamatnézet:

```bash
top
```

Ha telepítve van:

```bash
htop
```

Gyanúsabb lehet egy folyamat, ha:

- szokatlan néven fut
- ideiglenes könyvtárból indul
- sok processzort használ
- ismeretlen külső címhez kapcsolódik
- root jogosultsággal fut
- a neve megtévesztően hasonlít egy rendszerfolyamathoz

A magas processzorhasználat önmagában nem bizonyít támadást. Okozhatja hibás program vagy normális nagy terhelés is.

## 12. Szolgáltatások és systemctl

A modern Linux-rendszereken sok szolgáltatást a `systemd` kezel.

Szolgáltatás állapotának megtekintése:

```bash
systemctl status ssh
```

Futó szolgáltatások listája:

```bash
systemctl --type=service --state=running
```

Egy szolgáltatás indítása:

```bash
sudo systemctl start ssh
```

Egy szolgáltatás engedélyezése rendszerindításkor:

```bash
sudo systemctl enable ssh
```

Kezdőként elsősorban megtekintő parancsokat érdemes használni. Szolgáltatások leállítása vagy módosítása működési problémát okozhat.

## 13. Cron és ütemezett feladatok

A **cron** segítségével parancsok és programok meghatározott időpontban automatikusan elindíthatók.

Ez hasonló a Windows Feladatütemezőjéhez.

A felhasználó cronfeladatainak listája:

```bash
crontab -l
```

Példa:

```text
0 2 * * * /home/user/backup.sh
```

Ez minden nap hajnali 2 órakor elindítja a `backup.sh` fájlt.

A cron teljesen normális rendszerfunkció.

Támadók is használhatják arra, hogy:

- programjuk rendszeresen elinduljon
- újraindítás után is fennmaradjanak
- egy későbbi időpontban hajtsanak végre parancsot

Gyanús lehet, ha:

- ismeretlen szkriptet indít
- `/tmp` könyvtárból futtat programot
- internetes letöltést végez
- kódolt vagy nehezen olvasható parancsot tartalmaz

## 14. Csomagok és frissítések

A Linux-disztribúciók csomagkezelővel telepítik és frissítik a programokat.

Ubuntu és Debian rendszeren gyakori:

```bash
sudo apt update
sudo apt upgrade
```

Red Hat alapú rendszereken gyakori:

```bash
sudo dnf update
```

A frissítések azért fontosak, mert biztonsági hibákat javíthatnak.

Az NKI rendszeresen közöl Linuxot érintő sérülékenységekről szóló figyelmeztetéseket. Ezek azt mutatják, hogy a kernel, a `sudo` és más alapvető összetevők hibái is jelentős kockázatot jelenthetnek.

## 15. Egyszerű vizsgálati példa

A naplókban a következő események jelennek meg:

```text
01:42 — több sikertelen SSH-bejelentkezés
01:47 — sikeres belépés egy külső IP-címről
01:49 — sudo használata
01:51 — új cronfeladat létrehozása
01:52 — kapcsolat egy ismeretlen külső címhez
```

Ezek együtt érdekesebbek, mint külön-külön.

Egy kezdő elemző megvizsgálhatja:

1. melyik fiókkal történt a belépés
2. ismert-e a forrás IP-cím
3. jogosult volt-e a felhasználó a `sudo` használatára
4. milyen parancs futott
5. mit tartalmaz az új cronfeladat
6. melyik folyamat hozta létre a külső kapcsolatot
7. történt-e fájlmódosítás
8. van-e hasonló esemény más szerveren

A cél itt is az események időrendi összekapcsolása.

## 16. Hasznos, főként megtekintő parancsok

```bash
whoami
who
id
groups
ls -l
ps aux
ss -tulpen
journalctl -n 20
systemctl --type=service --state=running
crontab -l
```

Ezeket csak saját vagy engedélyezett rendszeren szabad használni.

## 17. Mit érdemes kezdőként megjegyezni?

- A root a legmagasabb jogosultságú Linux-fiók.
- A `sudo` ideiglenesen magasabb jogosultságot adhat.
- A fájljogosultságok meghatározzák, ki olvashat, írhat vagy futtathat egy fájlt.
- A hitelesítési naplók fontosak a bejelentkezések vizsgálatakor.
- A `journalctl` sok modern Linux-rendszeren központi naplólekérdező eszköz.
- Az SSH normális távoli adminisztrációs eszköz, de támadók is próbálhatják kihasználni.
- A cron és a szolgáltatások normális funkciók, de tartós jelenlétre is felhasználhatók.
- Egyetlen esemény helyett érdemes eseménysort vizsgálni.

## 18. Ellenőrző kérdések

1. Mi a Linux-disztribúció?
2. Mi a különbség a terminál és a shell között?
3. Miért érzékeny a root fiók?
4. Mire használható a `sudo`?
5. Mit jelent az `r`, `w` és `x` jogosultság?
6. Mire szolgál az `/etc` könyvtár?
7. Milyen naplókban találhatók hitelesítési események?
8. Mire használható a `journalctl`?
9. Mi az SSH?
10. Miért lehet érdekes egy új SSH-kulcs?
11. Mire szolgál a `systemctl`?
12. Mi az a cron?
13. Miért fontosak a rendszerfrissítések?
14. Miért nem bizonyít önmagában támadást a magas processzorhasználat?
15. Miért fontos több eseményt időrendben összekapcsolni?

## Források

1. Ubuntu Server Documentation  
   **User management**  
   https://ubuntu.com/server/docs/how-to/security/user-management/

2. Ubuntu Server Documentation  
   **OpenSSH server**  
   https://ubuntu.com/server/docs/how-to/security/openssh-server/

3. Ubuntu Server Documentation  
   **Security suggestions**  
   https://ubuntu.com/server/docs/explanation/security/security_suggestions/

4. Microsoft Learn  
   **Logging and Monitoring on Azure Linux**  
   https://learn.microsoft.com/en-us/azure/azure-linux/logging-monitoring

5. Microsoft Learn  
   **Schedule an antivirus scan using crontab**  
   https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scan-crontab

6. Nemzeti Kiberbiztonsági Intézet  
   **Kritikus sebezhetőségek a Sudo parancssori eszközben**  
   https://nki.gov.hu/it-biztonsag/hirek/kritikus-sebezhetosegek-a-sudo-parancssori-eszkozben-jogosultsagkiterjesztes-veszelye-fenyegeti-a-linux-rendszereket/

7. Nemzeti Kiberbiztonsági Intézet  
   **Linuxos sérülékenységek hulláma**  
   https://nki.gov.hu/it-biztonsag/hirek/linuxos-serulekenysegek-hullama/

8. Nemzeti Kiberbiztonsági Intézet  
   **Riasztás a Linux rendszereket érintő Copy Fail sérülékenységről**  
   https://nki.gov.hu/figyelmeztetesek/riasztas/riasztas-a-linux-rendszereket-erinto-copy-fail-serulekenysegrol/

9. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](04-windows-security.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](06-log-analysis.md)
