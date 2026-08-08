# 10 — Incidenskezelés

[← Vissza a magyar tartalomjegyzékhez](README.md) | [English version](../en/10-incident-response.md)

## Bevezetés

Egy biztonsági riasztás még nem feltétlenül jelent valódi támadást, ha azonban a vizsgálat azt mutatja, hogy tényleges kiberbiztonsági probléma történt, meg kell kezdeni annak kezelését.

Ezt nevezzük incident response-nak, magyarul incidenskezelésnek.

Az incidenskezelés célja, hogy a szervezet:

- gyorsan felismerje a problémát
- korlátozza a károkat
- megszüntesse a támadó jelenlétét
- biztonságosan helyreállítsa a működést
- megértse, mi történt
- tanuljon az esetből

A NIST SP 800-61 Rev. 3 az incidenskezelést a teljes kiberbiztonsági kockázatkezelés részeként kezeli.

## 1. Biztonsági esemény és incidens

A biztonsági esemény olyan történés, amely biztonsági szempontból érdekes lehet.

Példa:

```text
Egy felhasználó háromszor rossz jelszót adott meg.
```

Ez még nem biztos, hogy incidens.

A kiberbiztonsági incidens olyan esemény vagy eseménysor, amely valóban veszélyeztetheti a rendszert vagy az adatokat.

Példák:

- illetéktelen belépés
- malware-fertőzés
- adatlopás
- ransomware
- jogosultság megszerzése
- szolgáltatás megbénítása

## 2. Miért fontos a felkészülés?

A jó incidenskezelés az incidens előtt kezdődik.

Érdemes előre meghatározni:

- ki felel az incidenskezelésért
- kit kell értesíteni
- milyen naplókat gyűjt a szervezet
- hogyan történik az eszkaláció
- ki jogosult rendszert leválasztani
- milyen kommunikációs csatornákat használnak
- hol találhatók a biztonsági mentések
- mikor kell külső segítséget bevonni

## 3. Incident Response Plan

Az incident response plan egy előre elkészített incidenskezelési terv.

Tartalmazhatja:

- a szerepköröket
- a kapcsolattartókat
- az incidenskategóriákat
- az eszkaláció szabályait
- a kommunikáció menetét
- a dokumentálási követelményeket
- a külső bejelentés szabályait

A terv célja, hogy stresszes helyzetben se kelljen mindent az elejéről kitalálni.

## 4. Mi az a playbook?

A playbook egy konkrét incidensfajtára készített útmutató.

Lehet például:

- phishing playbook
- ransomware playbook
- kompromittált fiók playbook
- malware playbook

Egy phishing playbook kérdései lehetnek:

1. Ki kapta az e-mailt?
2. Kattintott-e a linkre?
3. Adott-e meg jelszót?
4. Más is megkapta-e?
5. Szükséges-e jelszócsere?
6. Le kell-e tiltani a domaint?

## 5. Észlelés és elemzés

Az incidens gyakran egy riasztással kezdődik.

A riasztás érkezhet:

- SIEM-ből
- EDR-ből
- vírusvédelemből
- tűzfalból
- felhasználói bejelentésből
- külső CERT vagy CSIRT értesítéséből

Az elemző megvizsgálhatja:

- az esemény idejét
- az érintett felhasználót
- a forrás IP-címet
- a folyamatokat
- a fájlokat
- a hálózati kapcsolatokat
- a kapcsolódó riasztásokat

## 6. Triage

A triage gyors első értékelést jelent.

A cél annak eldöntése, hogy:

- valódi problémáról lehet-e szó
- mennyire sürgős
- milyen rendszert érint
- hány felhasználó érintett
- szükséges-e eszkaláció

Nem ugyanolyan súlyos egy tesztgépen talált alacsony kockázatú malware, mint egy domain controller kompromittálása.

## 7. Containment

A containment jelentése korlátozás vagy elszigetelés.

Célja, hogy a támadás ne terjedjen tovább.

Lehetséges lépések:

- fertőzött gép leválasztása
- kompromittált fiók ideiglenes letiltása
- rosszindulatú domain blokkolása
- támadói IP-cím blokkolása
- veszélyeztetett szolgáltatás korlátozása

Fontos, hogy egy kritikus rendszer leállítása üzleti problémát is okozhat. Ezért a döntés nem mindig csak technikai.

## 8. Eradication

Az eradication a támadó jelenlétének és a probléma okának eltávolítását jelenti.

Példák:

- malware eltávolítása
- rosszindulatú fiók törlése
- sérülékenység javítása
- kompromittált jelszó cseréje
- rosszindulatú ütemezett feladat eltávolítása

Nem elég csak a látható tünetet megszüntetni.

## 9. Recovery

A recovery a normális működés biztonságos helyreállítása.

Lehetséges lépések:

- rendszer újratelepítése
- mentés visszaállítása
- jelszócsere
- frissítések telepítése
- szolgáltatások újraindítása
- fokozott megfigyelés

A cél nem pusztán a gyorsaság. A rendszernek biztonságosan kell újra működnie.

## 10. Bizonyítékok megőrzése

Egy incidens során fontos bizonyíték lehet:

- napló
- e-mail
- fájl
- memóriaadat
- lemezkép
- hálózati adat
- képernyőkép
- idővonal

Érdemes dokumentálni:

- mit gyűjtöttünk
- mikor gyűjtöttük
- honnan származik
- ki kezelte

## 11. Chain of Custody

A chain of custody azt dokumentálja, hogyan kezelték a bizonyítékot.

Példa:

```text
09:20 — lemezkép elkészült
09:25 — SHA-256 hash rögzítve
09:30 — biztonságos tárhelyre került
09:35 — átadva a forenzikai elemzőnek
```

Ez különösen jogi vagy hatósági ügyben fontos.

## 12. Dokumentáció

Egy incidens során folyamatosan érdemes dokumentálni.

Példa:

```text
10:12 — riasztás érkezett
10:17 — felhasználó megkeresve
10:25 — jogosulatlan belépés megerősítve
10:31 — fiók letiltva
10:45 — gép izolálva
```

A dokumentáció segít a vizsgálat követésében és a későbbi visszatekintésben.

## 13. Kommunikáció

Egy komoly incidens során több csapat dolgozhat együtt:

- SOC
- IT
- vezetőség
- jogi csapat
- adatvédelmi szakértők
- kommunikáció
- HR
- külső szolgáltatók

Fontos előre tudni, ki kommunikálhat belső és külső szereplőkkel.

## 14. Lessons Learned

Az incidens lezárása után érdemes megnézni:

- hogyan jutott be a támadó
- mi működött jól
- mi lassította a vizsgálatot
- mely naplók hiányoztak
- kell-e új detektálási szabály
- kell-e módosítani a playbookot
- szükséges-e képzés

A cél a tanulás és a folyamat javítása.

## 15. A NIST újabb szemlélete

A klasszikus incidenskezelési folyamat gyakran így jelenik meg:

```text
Preparation
Detection and Analysis
Containment, Eradication and Recovery
Post-Incident Activity
```

A NIST SP 800-61 Rev. 3 ezt már a Cybersecurity Framework 2.0 egészébe helyezi:

```text
Govern
Identify
Protect
Detect
Respond
Recover
```

Ez azt hangsúlyozza, hogy az incidenskezelés nem csak akkor kezdődik, amikor megszólal egy riasztás.

## 16. Egyszerű ransomware-példa

```text
09:05 — felhasználó jelzi, hogy nem nyílnak meg a fájlok
09:08 — SOC ellenőrzi az EDR-riasztást
09:12 — gép izolálva
09:17 — hasonló aktivitás keresése más gépeken
09:25 — újabb érintett rendszer azonosítva
09:30 — incidens eszkalálva
```

Egy valódi ransomware-incidens ennél jóval összetettebb lehet.

## 17. Mit ne tegyen egy kezdő?

Komoly incidensnél jóváhagyás nélkül nem érdemes:

- gépeket tömegesen leállítani
- fájlokat törölni
- bizonyítékokat módosítani
- támadó infrastruktúrához aktívan kapcsolódni
- nyilvánosan kommunikálni
- ismeretlen eszközt futtatni éles rendszeren

Az egyik legfontosabb készség annak felismerése, mikor kell eszkalálni.

## 18. Mit érdemes kezdőként megjegyezni?

- Nem minden biztonsági esemény incidens.
- A felkészülés az incidens előtt kezdődik.
- A triage segít a sürgősség megítélésében.
- A containment a terjedés korlátozása.
- Az eradication a probléma okának megszüntetése.
- A recovery a biztonságos helyreállítás.
- A bizonyítékokat óvatosan kell kezelni.
- Minden fontos lépést dokumentálni kell.
- Az incidenskezelés technikai és szervezeti feladat.
- Az eset után tanulni kell a történtekből.
- Ha bizonytalan vagy, eszkalálj.

## 19. Ellenőrző kérdések

1. Mi a különbség esemény és incidens között?
2. Mi az incidenskezelés célja?
3. Miért fontos a felkészülés?
4. Mi az incident response plan?
5. Mi az a playbook?
6. Mit jelent a triage?
7. Mit jelent a containment?
8. Mit jelent az eradication?
9. Mit jelent a recovery?
10. Miért fontos a bizonyítékok megőrzése?
11. Mi az a chain of custody?
12. Miért fontos a dokumentáció?
13. Mit jelent a lessons learned?
14. Miért kell több szervezeti terület együttműködése?
15. Mit hangsúlyoz a NIST SP 800-61 Rev. 3?

## Források

1. National Institute of Standards and Technology  
   **NIST SP 800-61 Rev. 3 — Incident Response Recommendations and Considerations for Cybersecurity Risk Management**  
   https://csrc.nist.gov/pubs/sp/800/61/r3/final

2. National Institute of Standards and Technology  
   **Incident Response Project**  
   https://csrc.nist.gov/projects/incident-response

3. Cybersecurity and Infrastructure Security Agency  
   **Federal Government Cybersecurity Incident and Vulnerability Response Playbooks**  
   https://www.cisa.gov/sites/default/files/2024-08/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf

4. Nemzeti Kiberbiztonsági Intézet  
   **Incidenskezelés**  
   https://nki.gov.hu/szolgaltatasok/tartalom/incidenskezeles/

5. Nemzeti Kiberbiztonsági Intézet  
   **Kézikönyv készült a szervezetek eseménynaplózásának meghatározásához**  
   https://nki.gov.hu/it-biztonsag/hirek/kezikonyv-keszult-a-szervezetek-esemenynaplozasanak-meghatarozasahoz/

6. Gyaraki Réka szerk.  
   **Az információbiztonság alapjai**  
   Nemzeti Közszolgálati Egyetem, 2023  
   https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf

---

[← Előző fejezet](09-mitre-attack.md) | [Vissza a tartalomjegyzékhez](README.md) | [Következő fejezet →](11-malware-basics.md)
