Ez a diasor a **szoftvertesztelés alapfogalmait, folyamatát és stratégiáit** tekinti át. Vizsgára készülve ezek a strukturált kategóriák (szintek, típusok, technikák) a legfontosabbak.

Íme a részletes feldolgozás:

---

# 1. Alapfogalmak és definíciók (1-13. dia)

A tesztelés nem csak a hiba megkeresése, hanem egy összetett minőségbiztosítási tevékenység.

### A tesztelés három megközelítése (8-10. dia):
1.  **IEEE definíció:** A rendszer végrehajtása meghatározott körülmények között, az eredmények megfigyelése és kiértékelése.
2.  **ISTQB (folyamat-központú):** Olyan tevékenységek sorozata, amely megállapítja, hogy a termék teljesíti-e a követelményeket és "alkalmas-e a célra" (fit for purpose).
3.  **Bach & Bolton (felfedező):** Tanulási folyamat, kísérletezés, amivel megismerjük a termék korlátait.

### Alapfogalmak (11. dia) – *Kritikus a vizsgához!*
*   **SUT (System Under Test):** A rendszer, amit éppen tesztelünk.
*   **Teszteset (Test Case):** Bemenetek + végrehajtási feltételek + **elvárt eredmény**.
*   **Tesztkészlet (Test Suite):** Összetartozó tesztesetek csoportja.
*   **Teszt-orákulum (Test Oracle):** Az a módszer, amivel eldöntjük, hogy a teszt sikeres-e (pl. egy dokumentum, egy régi programverzió vagy akár az emberi szem).
*   **Eredmény (Verdict):** `Pass` (átment), `Fail` (elbukott), `Error` (a tesztkörnyezet hibás), `Inconclusive` (nem dönthető el).

### Miért nem lehet mindent tesztelni? (12. dia)
**Kimerítő (exhaustive) tesztelés lehetetlen.** Példa: Ha egy függvénynek 2 darab 32 bites egész száma van, az $2^{64}$ variáció. Másodpercenként 1 millió teszttel ez **585 000 évig** tartana. Ezért kell intelligensen kiválasztani a teszteseteket.

---

# 2. V&V: Verifikáció és Validáció (19. dia)

Ez a szoftvertechnológia egyik legfontosabb megkülönböztetése:
*   **Verifikáció:** „Jól építem meg a rendszert?” (A terveknek megfelel-e? Objektív, automatizálható).
*   **Validáció:** „A jó rendszert építem meg?” (A felhasználó tényleg ezt akarta-e? Szubjektív, az elfogadásra fókuszál).

---

# 3. A tesztelési folyamat (ISTQB modell) (18-32. dia)

A tesztelés nem csak a futtatásból áll, hanem egy 5 lépéses ciklusból:
1.  **Tervezés és Irányítás:** Hatáskör (scope) kijelölése, kockázatok felmérése.
2.  **Analízis és Tervezés:** Mit teszteljünk? Tesztesetek kidolgozása.
3.  **Megvalósítás és Végrehajtás:** Tesztkörnyezet beállítása, tesztek futtatása, naplózás.
4.  **Kilépési feltételek ellenőrzése:** Elértük a célokat? (Pl. 90% feletti lefedettség).
5.  **Lezárás:** Tapasztalatok összegzése, hibajegyek archiválása.

### Shift Left elv (23. dia) – *Modern trend!*
A hibák 50%-a a követelményelemzés és tervezés során keletkezik. Minél később találjuk meg a hibát, annál drágább javítani (exponenciálisan nő a költség!).
*   **Shift Left:** „Told balra” a tesztelést, azaz kezdd el már a fejlesztés legelején (pl. statikus elemzéssel, kódátnézéssel).

---

# 4. Tesztelési szintek (33-41. dia)

A szoftvert különböző nagyításban vizsgáljuk:

1.  **Egységteszt (Unit test):** Egyetlen metódus vagy osztály tesztelése (fejlesztő végzi, izoláltan, gyorsan).
2.  **Integrációs teszt:** Több modul együttműködése (pl. adatbázis elérése, API hívások).
3.  **Rendszerteszt:** A teljes szoftver ellenőrzése a követelmények alapján.
4.  **Elfogadási teszt (Acceptance):** A megrendelő végzi, hogy átveszi-e a terméket.

### Tesztelési piramis (41. dia)
Az ideális szoftverprojektben:
*   Alul van a legtöbb **automatizált egységteszt** (olcsó, gyors).
*   Középen kevesebb integrációs teszt.
*   A csúcson van a legkevesebb **manuális teszt** (drága, lassú).

---

# 5. Teszttervezési technikák (43-47. dia)

Hogyan választunk teszteseteket?

*   **Specifikáció alapú (Black-box):** Nem ismerjük a kódot, csak azt, hogy mit kellene csinálnia.
    *   *Ekvivalencia partíciók:* Azonos módon viselkedő értékek csoportosítása (pl. 0-100 között minden szám "ugyanaz").
    *   *Határérték analízis:* A hibák gyakran a széleken vannak (pl. 0, 1, 99, 100 tesztelése).
*   **Struktúra alapú (White-box / Fehér doboz):** Látjuk a kódot. A cél, hogy minden sor és minden döntési ág lefusson legalább egyszer (**kódlefedettség**).
*   **Hibaalapú / Mutációs tesztelés (47. dia):** Szándékosan hibát teszünk a kódba (mutánsok), és megnézzük, hogy a tesztjeink észreveszik-e. Ha nem, akkor a tesztkészletünk nem elég jó.
*   **Tapasztalati (Exploratory):** A tesztelő tudására és kreativitására épít.

---

# 6. Agilis tesztelés (51. dia)

A **Tesztelési Kvadránsok** (Agile Testing Quadrants) segítenek csoportosítani a teszteket:
*   **Q1 (Technológiai fókusz, fejlesztés támogatása):** Egységtesztek, CI.
*   **Q2 (Üzleti fókusz, fejlesztés támogatása):** Funkcionális példák, prototípusok.
*   **Q3 (Üzleti fókusz, termék kritikája):** Felderítő tesztelés, felhasználói elfogadás.
*   **Q4 (Technológiai fókusz, termék kritikája):** Teljesítmény, biztonság, terheléses tesztelés.

---

### Összefoglaló a vizsgához:
1.  Tudd megkülönböztetni a **Verifikációt** (kód vs terv) és a **Validációt** (termék vs igény).
2.  Értsd a **Tesztelési piramist**: miért van sok egységteszt és kevés GUI teszt?
3.  Ismerd a **Shift Left** lényegét (korai tesztelés = olcsóbb hibajavítás).
4.  Tudd felidézni a **Black-box** (pl. határérték) és **White-box** (lefedettség) technikák közötti különbséget.

Sok sikert a felkészüléshez! Ha valamelyik technika (pl. MC/DC lefedettség vagy mutációs teszt) nem világos, kérdezz bátran!