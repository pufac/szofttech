Ez a diasor a szoftvertechnológia egyik legfontosabb gyakorlati kérdéskörét, a **minőségi forráskód előállítását és ellenőrzését** tárgyalja. A vizsgán ezek a módszerek (statikus analízis, kód felülvizsgálat, irányelvek) alapvetőek.

Íme a részletes kidolgozás:

---

# 1. Alapfogalmak és Motiváció (1-7. dia)

### Miért kell a "szép" kód? (5. dia)
A dián látható **rossz példa** (C# kód) tökéletesen illusztrálja a problémát. Bár a kód lefordul és működik, mégis csapnivaló:
*   **Mágikus számok:** Mit jelent a `0.1m` vagy a `0.7m`? (Kedvezmény? Adó?)
*   **Érthetetlen típusok:** Mit takar a `type == 2`? 
*   **Karbantarthatatlan:** Ha változik az üzleti logika, ember legyen a talpán, aki ezt hiba nélkül átírja.

### Ellenőrzési módszerek (6. dia) – *Vizsgán gyakori kérdés!*
Két fő csoportra osztjuk a kód ellenőrzését:
1.  **Statikus:** A program **futtatása nélkül** vizsgáljuk a terméket (kódot, dokumentációt). 
    *   *Példa:* Kódolvasás, statikus analízis eszközök.
2.  **Dinamikus:** A programot **futtatjuk**, bemeneteket adunk neki és nézzük az eredményt.
    *   *Példa:* Tesztelés, szimuláció.

### A jó kód 4 pillére (7. dia)
*   **Szintaktikailag helyes:** A fordító elfogadja.
*   **Jó minőségű:** Olvasható, karbantartható (irányelvek segítenek).
*   **Hibáktól mentes:** Nem száll el futás közben (analízis és tesztelés segíti).
*   **Specifikációnak megfelelő:** Pontosan azt csinálja, amit az ügyfél kért.

---

# 2. Olvashatóság és Kódolási Irányelvek (8-20. dia)

**Aranyszabály (8. dia):** Egy kódot egyszer írunk meg, de **sokszor olvasunk**. Ezért az olvashatóságra kell optimalizálni, nem az írás gyorsaságára.

### Mitől olvasható a kód? (9. dia)
*   **Alapok:** Egységes formázás, beszédes változónevek (pl. `index` helyett `customerListIndex`).
*   **Illeszkedés:** Használjuk az adott nyelv stílusát. 
    *   *Példa:* Java-ban `camelCase` a metódus, C#-ban `PascalCase`. Ne írj Java kódot C# stílusban!
*   **Szakterület:** Ne keverjük az üzleti logikát (pl. kamatszámítás) a technikai részletekkel (pl. SQL lekérdezés).

### Kódolási irányelvek fajtái (11-17. dia)
1.  **Szakterület specifikus:** Pl. a **MISRA C** (12. dia). Az autóiparban használják, ahol a biztonság kritikus. Tiltja az olyan veszélyes dolgokat, mint a `goto` vagy a nem egyértelmű logikai kifejezések.
2.  **Szervezet specifikus:** Pl. a **Google Java Style Guide** (14-15. dia). Meghatározza a kapcsos zárójelek helyét, a változók sorrendjét az osztályon belül.
3.  **Platform specifikus:** Pl. a **.NET Design Guidelines** (16-17. dia). Megmondja, hogyan dobjunk kivételeket (pl. ne kontrollflow-ra használjuk a kivételt).

**Apple "goto fail" hiba (13. dia):** Egy tanulságos példa. Egy elírt behúzás és egy dupla `goto` miatt a biztonsági ellenőrzés kimaradt az iPhone-okból. Egy statikus analízis eszköz ezt azonnal kiszúrta volna!

### Hogyan tartsuk be? (18-19. dia)
Ne a fejlesztőnek kelljen fejben tartania mindent! Használjunk:
*   **IDE formázót:** Egy gombnyomásra "széppé" teszi a kódot (pl. VS Code formatter).
*   **Lintert:** Gépelés közben pirossal aláhúzza, ha sértjük a szabályokat.

---

# 3. Kód felülvizsgálat (Code Review) (21-26. dia)

**Definíció:** Emberek olvassák és elemzik egymás kódját.

### Típusai (23. dia):
*   **Inspekció (Formal):** Nagyon alapos, lassú, de hatékony. Szerepkörök vannak (moderátor, jegyző).
*   **Modern, pehelysúlyú:** Gyors, eszközökkel támogatott (pl. GitHub Pull Request).

### Miért jó? (23. dia)
*   Nem csak a hibát találja meg.
*   **Tudástranszfer:** A junior tanul a seniortól a megjegyzésekből.
*   **Csapatszellem:** Közös felelősség a kódért.

---

# 4. Statikus Analízis (27-39. dia)

**Definíció (29. dia):** Automatikus szoftveres vizsgálat futtatás nélkül.

### Hogyan működik? (30. dia)
Az eszköz felépít egy **AST-t (Abstract Syntax Tree)**, ami a kód fa-szerű logikai váza. Ezen a fán keres ismert "rossz mintákat" (anti-patterns).
*   *Példa szabály:* "Stringeket `.equals()`-szal hasonlíts össze, ne `==`-vel!"

### SonarQube – A "standard" eszköz (32-36. dia)
A SonarQube egy platform, ami méri a kód minőségét:
*   **Technical Debt (Technikai adósság):** Megbecsüli percekben/órákban, mennyi ideig tartana kijavítani a kódminőségi hibákat (code smells).
*   **Quality Gate (Minőségi kapu):** Beállítható, hogy ha a kód nem ér el egy bizonyos szintet (pl. 80% feletti tesztlefedettség), akkor ne engedje "beolvasztani" a végleges kódba.

### Fontos elméleti fogalmak (38. dia) – *Várható vizsgakérdés!*
A statikus analízis nem tévedhetetlen:
*   **False Positive (Hamis pozitív):** Az eszköz hibát jelez, de a kód valójában jó. (Zavaró, de túlélhető).
*   **False Negative (Hamis negatív):** Van hiba a kódban, de az eszköz **nem vette észre**. Ez a veszélyesebb!

---

# 5. Kitekintés és NASA példa (41-43. dia)

**Lehet-e hibamentes kódot írni?**
Gyakorlatilag nem, de a NASA a **Space Shuttle** programnál megközelítette (42. dia). 
*   **Stat:** 0,11 hiba / 1000 sor kód.
*   **Ár:** 1000 USD / kódsor! 
Ez jól mutatja, hogy a minőségnek ára van: ha életkritikus rendszert építünk, a fejlesztés 10x lassabb és 100x drágább lehet.

### Összefoglalás a vizsgához:
1.  Ismerd a **Statikus vs Dinamikus** különbséget.
2.  Tudd, mi az a **Technical Debt** és miért veszélyes.
3.  Tudd elmagyarázni a **False Positive/Negative** fogalmát.
4.  Értsd a **Code Review** és a **Linting** hasznát (tudástranszfer, egységesség).

Sok sikert a vizsgához! Ha van olyan részlet (pl. az AST vagy a MISRA C konkrét szabályai), amibe mélyebben belemenjünk, jelezd!