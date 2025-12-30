Ez egy kiváló és átfogó anyagsor a **szoftverfejlesztői munkafolyamatokról**. A vizsgára való felkészüléshez lépésről lépésre, diáinként haladva dolgozzuk fel a témát, kiemelve a legfontosabb fogalmakat és összefüggéseket.

---

# 1. Bevezetés és Alapfogalmak (1-5. dia)

Az előadás célja, hogy bemutassa a fejlesztők **napi munkafolyamatát**. Ez nem csak a kódolásról szól, hanem egy komplex ciklusról, amit ma gyakran a **DevOps** szemlélettel írunk le.

### DevOps ciklus (4. dia)
A DevOps a fejlesztés (*Development*) és az üzemeltetés (*Operations*) szoros együttműködését jelenti. A dián látható "végtelen jel" szimbolizálja, hogy ez egy folyamatos, soha véget nem érő körforgás:
1.  **PLAN (Tervezés):** Feladatok meghatározása.
2.  **CODE (Kódolás):** A tényleges fejlesztés.
3.  **BUILD (Összeállítás):** A forráskódból futtatható termék készítése.
4.  **TEST (Tesztelés):** Helyesség ellenőrzése.
5.  **RELEASE (Kiadás):** Verziózott csomag készítése.
6.  **DEPLOY (Telepítés):** Kikerülés a szerverre/felhasználóhoz.
7.  **OPERATE (Üzemeltetés):** A rendszer futtatása.
8.  **MEASURE (Mérés):** Visszajelzések és metrikák gyűjtése.

---

# 2. A munka megkezdése: Mi a feladat? (6-10. dia)

Egy fejlesztő (különösen egy junior) jellemzően háromféle feladattal találkozik:
*   **Új funkció (Feature):** Valami olyat kell fejleszteni, ami még nincs.
*   **Hibajavítás (Bugfix):** Egy létező, de rosszul működő rész javítása.
*   **Átírás (Refactor):** A kód belső szerkezetének javítása a külső működés megváltoztatása nélkül.

### Bemenet: Issue, Story, Ticket (7-8. dia)
A fejlesztő nem "csak úgy" kódol, hanem egy konkrét leírás alapján dolgozik:
*   **Agilis/Open Source környezet:** Itt **Issue**-nak vagy **User Story**-nak hívják a feladatot. Eszközök: **Jira, GitHub**. Ezek általában rövidebb, lényegre törő leírások.
*   **Kritikus rendszerek (pl. vonatvezérlés):** Itt formálisabb **modul specifikációk** vannak. Eszközök: **IBM DOORS**. Ezek nagyon részletesek, táblázatokkal és modellekkel.

### Átvizsgálás és Tervezés (9-10. dia)
**Nagyon fontos vizsgapont:** Mielőtt a fejlesztő belecsapna a kódba, két dolgot kell tennie:
1.  **Review (Átvizsgálás):** Megnézni, hogy a feladat egyértelmű-e, megvalósítható-e, és tesztelhető-e. Ezzel rengeteg felesleges munkát lehet megspórolni.
2.  **Részletes terv:** Bonyolultabb feladatnál érdemes allépésekre bontani, **pszeudokódot** írni vagy **UML modellt** (pl. állapotgépet) skiccelni.

---

# 3. Kódolás és minőségbiztosítás (11-18. dia)

### Hibajavítás folyamata (11. dia)
Ha bugot javítunk, a sorrend kötött:
1.  **Reprodukálás:** El kell érni, hogy a hiba nálunk is jelentkezzen (különben nem tudjuk, javítottuk-e).
2.  **Hibakeresés (Fault localization):** Megtalálni a pontos helyet a kódban (debugging).
3.  **Javítás:** A kód módosítása.
4.  **Ellenőrzés:** Megoldódott a hiba? Nem rontottunk el mást? (Regressziós teszt).

### Refaktorálás és Technikai adósság (12. dia)
*   **Refaktorálás:** "A belső struktúra átalakítása a külső viselkedés megváltoztatása nélkül." Célja az olvashatóság és karbantarthatóság. *Példa: Egy 500 soros függvényt szétbontunk 10 kisebb, jól elnevezett részre (Extract Method).*
*   **Technikai adósság (Technical debt):** Ha sietünk és "tákolt" megoldást használunk, az adósság. Később ezt "kamattal" kell megfizetni (nehezebb lesz módosítani, több lesz a bug).

### Hogyan kódoljunk? (15-18. dia)
*   **Környezet:** Lehet helyi (saját PC) vagy távoli (pl. **GitHub Codespaces**).
*   **Pair Programming (Páros programozás):** Ketten ülnek egy gép előtt.
    *   *Driver:* Ő gépel, a taktikai részre figyel.
    *   *Navigator:* Ő figyel, stratégiai szemmel nézi a kódot, ellenőriz.
*   **Kódolási irányelvek:** Szabályok (pl. hol legyen a kapcsos zárójel). A **Linter** eszközök ezeket automatikusan ellenőrzik.
*   **Statikus analízis:** A kód vizsgálata **futtatás nélkül**. Olyan hibákat talál meg, mint a nullával való osztás vagy a soha el nem érhető kód (pl. **SonarQube**).

---

# 4. Build és Függőségek (19-26. dia)

### Miért nem elég a fordító (gcc/javac)? (20. dia)
Egy nagy projektnél több száz fájl van, külső könyvtárakat használunk, és különböző verziókat akarunk (pl. Debug vagy Release). Kézzel ezt lehetetlen kezelni.

### Build keretrendszerek (21-24. dia)
Az automatizált build folyamata:
**Előkészítés → Fordítás → Tesztelés → Csomagolás → Telepítés.**
Eszközök: **Maven, Gradle (Java), CMake (C++), MSBuild (.NET).**

*   **Maven elv: "Convention over configuration":** Ha betartod a standard könyvtárstruktúrát (pl. forráskód az `src/main/java`-ban, tesztek az `src/test/java`-ban), akkor alig kell konfigurálnod valamit, a Maven tudni fogja, mit hol keressen.

### Függőségkezelés (25-26. dia)
A programunk külső könyvtárakat (dependency) használ. Ezeket nem érdemes kézzel másolgatni.
*   **Központi tárhelyek:** **Maven Central, npm Registry, NuGet.**
*   **Tranzitív függőség:** Ha a mi programunknak kell az 'A' csomag, de az 'A'-nak kell a 'B', akkor a build eszköz automatikusan letölti a 'B'-t is.

---

# 5. Tesztelés és Integráció (27-37. dia)

### TDD - Tesztvezérelt fejlesztés (30. dia)
Ez egy speciális módszer. A ciklus:
1.  **Teszt írása:** Még nincs is kész a funkció, a teszt elbukik (**Red**).
2.  **Kód írása:** Csak annyit írunk, hogy a teszt átmenjen (**Green**).
3.  **Refactor:** Szépítjük a kódot.

### Definition of Done (DoD) (31. dia)
Egy ellenőrző lista: mikor mondhatjuk egy feladatra, hogy tényleg KÉSZ? (Kód kész, tesztek futnak, dokumentáció megvan, átnézték).

### CI - Folytonos Integráció (33-37. dia)
A legnagyobb probléma, ha 10 fejlesztő külön dolgozik 2 hétig, és a végén próbálják összeönteni a kódot (**Merge conflict**).
*   **CI elve:** Mindenki naponta többször töltse fel a kódját a központi **Verziókezelőbe** (Git).
*   **CI szerver (pl. Jenkins, GitHub Actions):** Minden feltöltésnél automatikusan elindítja a Buildet és a Teszteket. Ha valaki elrontott valamit, azonnal (pár percen belül) kiderül.

---

# 6. Kiadás és Üzemeltetés (38-45. dia)

### Semantic Versioning (SemVer) (40. dia)
A verziószám felépítése: **MAJOR . MINOR . PATCH** (pl. 2.1.3)
*   **MAJOR:** Ha olyat változtattál, ami miatt a régi kódok nem fognak működni (visszafelé nem kompatibilis).
*   **MINOR:** Új funkció, de a régi dolgok még működnek.
*   **PATCH:** Csak hibajavítás.

### Continuous Delivery (CD) (43. dia)
Célja, hogy a szoftver **bármelyik pillanatban** alkalmas legyen az élesítésre.
*   **Continuous Deployment:** Itt a folyamat teljesen automatikus, a kód sikeres tesztek után emberi beavatkozás nélkül kikerül az éles szerverre.

### Monitorozás (45. dia)
A fejlesztő felelőssége nem ér véget a kódolással. Figyelni kell az éles rendszert (CPU használat, hibaüzenetek száma). "Aki fejleszti, az üzemelteti" (You build it, you run it) – ha éjjel leáll a szerver, a fejlesztőt riasztják.

---

### Összefoglaló ábra (47. dia)
Ez a dia a legfontosabb a vizsgára! Nézd végig az ikonokat:
1.  **Funkció** leírása.
2.  **Tervezés** (Terv).
3.  **Fejlesztő** megírja a kódot (Kódolási szabályok, Statikus analízis mellett).
4.  **Verziókezelőbe** rakja.
5.  **Felülvizsgáló** (másik fejlesztő) átnézi.
6.  **CI kiszolgáló** buildeli és teszteli (Egységteszt, Rendszerteszt).
7.  **Éles környezetbe** kerül, ahol a **Felügyelet** (monitorozás) figyeli.

Sok sikert a vizsgához! Ha valamelyik fogalom (pl. Maven POM fájl vagy a Merge conflict) nem világos, kérdezz bátran!