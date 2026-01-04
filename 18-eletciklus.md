Ez a diasor a **Szoftver életciklus modelleket (SDLC)** tárgyalja, ami a szoftvertechnológia "hogyan csináljuk" részének az alapja. A vizsgán ezek a modellek (Vízesés, V-modell, Agilis) alapvető összehasonlítási pontok.

Íme a diasor részletes, magyarázó feldolgozása:

---

### 1. Bevezetés és alapfogalmak (1–14. dia)

A szoftver nem olyan, mint egy fizikai tárgy. A 4. dia emlékeztet a sajátosságaira:
*   **Nincs gyártási költség:** A másolás szinte ingyen van.
*   **Nem "kopik" el:** A szoftver nem romlik el fizikailag, de a környezet változása miatt elavulhat.
*   **Logikai entitás:** A hibák nem fizikai törések, hanem logikai tévedések.
*   **Módosítás:** Könnyűnek tűnik átírni, de egy nagy rendszerben ez rendkívül kockázatos.

**Mi az az életciklus (SDLC)? (11. dia)**
A szoftver útja az **ötlettől a nyugdíjazásig (kivezetésig)**. Nem csak a kódolásról szól, hanem a tervezésről, tesztelésről és az üzemeltetésről is.

**A szoftver mérete és a hibák (8. dia):**
Ma egy kritikus rendszer (pl. helikopter vezérlése) 70-80%-a szoftver. 
*   **Statisztika:** Egy átlagos programozó 1000 soronként 10-12 hibát vét. 
*   **Tanulság:** Mivel egy modern rendszer több millió sorból áll, a hibák elkerülhetetlenek. A modellek célja, hogy ezeket strukturáltan kezeljük.

---

### 2. A Vízesés modell (Waterfall) (15–20. dia)

Ez a legrégebbi, 1970-es évekből származó modell (Winston Royce).

*   **Lényege (16. dia):** A fázisok szigorúan egymás után következnek, mint a vízesés lépcsői:
    1.  Követelmények elemzése
    2.  Tervezés (Rendszerterv)
    3.  Implementáció (Kódolás)
    4.  Integráció és tesztelés
    5.  Telepítés/Üzemeltetés
*   **Előnyei:** Egyszerű, tiszta szerkezet, könnyen dokumentálható.
*   **Hátrányai (17. dia):** **Rugalmatlan.** Ha a tesztelésnél derül ki, hogy elrontottuk a követelményeket, szinte lehetetlen visszamenni. A felhasználó csak a folyamat legvégén látja a terméket.
*   **Mikor jó? (19. dia):** Kicsi projekteknél, ahol a technológia ismert és a követelmények **kőbe vannak vésve**.

**A hibák költsége (18. dia) – !!! VIZSGAPONT !!!**
Minél később derül ki egy hiba, annál drágább javítani. Ha a követelmény fázisban találjuk meg, az 1x költség. Ha az üzemeltetés során, az akár **30x-100x** annyiba is kerülhet!

---

### 3. A V-modell (21–28. dia)

A V-modell a Vízesés modell továbbfejlesztése, kifejezetten **kritikus rendszerekhez** (autóipar, repülés, orvosi eszközök).

*   **A "V" alak lényege (23. dia):** A modell bal szára a tervezés (lebontás), a jobb szára az ellenőrzés (összeépítés).
*   **Vízszintes kapcsolat (V&V):** Minden tervezési lépéshez tartozik egy tesztelési lépés. 
    *   A **Modul tervezéshez** tartozik a **Modul ellenőrzés**.
    *   A **Rendszer specifikációhoz** tartozik a **Rendszer validáció**.
*   **Nyomonkövethetőség (Traceability) (24. dia):** Minden kódsornak visszafejthetőnek kell lennie egy követelményre, és minden követelményhez kell tartoznia egy tesztnek.
*   **Inkonzisztencia (26. dia):** A V-modell segít észrevenni, ha két követelmény üti egymást (pl. "a mozdony ne legyen módosítható" VS "legyen távolról leállítható").

---

### 4. Agilis fejlesztés (29–37. dia)

Az agilis módszertan a 2000-es évek elején jött létre válaszként a merev modellekre.

*   **Előzmények (30-31. dia):** PDCA ciklus (Deming) és a Spirál modell (Boehm), ami már a kockázatokra koncentrált.
*   **Agilis Kiáltvány (33. dia) – !!! Ezt tudni kell !!!**
    1.  **Egyének és interakciók** fontosabbak, mint a folyamatok és eszközök.
    2.  **Működő szoftver** fontosabb, mint az átfogó dokumentáció.
    3.  **Együttműködés az ügyféllel** fontosabb, mint a szerződéses alkudozás.
    4.  **Válaszkészség a változásra** fontosabb, mint a terv követése.
*   **Működése (34. dia):** Rövid, 2-4 hetes ciklusok (iterációk). Minden ciklus végén van egy működő (bár nem teljes) szoftver.
*   **12 Alapelv (35-36. dia):** Ügyfélelégedettség, változások befogadása, gyakori szállítás, napi közös munka, bizalom, személyes beszélgetés.

---

### 5. Sikeresség és Kitekintés (38–46. dia)

**Hogyan mérjük a sikert? (39. dia)**
*   Hagyományos: Időben (On Time), Keretben (On Budget), Funkciókban (On Scope) vagyunk-e?
*   **Ellenpéldák (40. dia):** 
    *   *Titanic (film):* Túllépte a keretet és az időt, de óriási anyagi siker lett (Oscar-díjak). 
    *   *Motorola Iridium:* Időben és keretben kész lett, de senki nem akarta megvenni (üzleti bukás).
*   **Statisztika (41. dia):** Az agilis projektek sikerrátája (42%) sokkal magasabb, mint a vízeséséé (13%).

**EU szabályozás (Cyber Resilience Act - 43. dia):**
A jövőben a szoftver is terméknek minősül az EU-ban. Ha kritikus (pl. operációs rendszer, jelszókezelő), szigorú harmadik fél általi tanúsításra lesz szükség.

---

### Összefoglaló táblázat a vizsgához (45. dia):

| Modell | Jellemző | Mikor válaszd? |
| :--- | :--- | :--- |
| **Vízesés** | Merev, lineáris, fázisokra bontott. | Kicsi projekt, fix igények. |
| **V-modell** | Tesztelés-orientált, erős nyomonkövetés. | Kritikus rendszerek (biztonság). |
| **Agilis** | Iteratív, rugalmas, változásbarát. | Bizonytalan igények, gyors piac. |

**Extra fogalom: Hype-görbe (10. dia):** Egy új technológia útja a túlzott lelkesedéstől a csalódáson át a valódi hasznosságig. Ne tévesszen meg a kezdeti lelkesedés egy eszközzel kapcsolatban!

Sok sikert a vizsgához! Ha valamelyik modell (pl. a V-modell diagramja) nem világos, szólj!