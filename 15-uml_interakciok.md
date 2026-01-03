Ez a diasor az **UML interakciókat**, azon belül is legfőképpen a **szekvenciadiagramokat** dolgozza fel. Míg az állapotgép a rendszer teljes életútját írja le, az interakciók csak egy-egy konkrét **forgatókönyvet (scenario)** mutatnak be.

Íme a részletes, vizsgára fókuszáló magyarázat:

---

# 1. Mi az az interakció? (1-5. dia)

Az interakciók a rendszer **dinamikus viselkedését** mutatják be szereplők (objektumok, komponensek) közötti üzenetváltásokon keresztül.

*   **Forgatókönyv (Scenario):** Események egy konkrét sorozata. 
*   **"Interactions do not tell the complete story" (3. dia):** Ez egy kulcsfontosságú mondat. Az interakció (pl. szekvenciadiagram) **részleges** leírást ad. Csak egy-egy fontosabb példát vagy tesztesetet mutat be, nem az összes lehetséges variációt.
*   **Mire jó?**
    *   Használati esetek (Use Case-ek) részletezésére (hogyan valósul meg a "Vásárlás" folyamata).
    *   Protokollok leírására (milyen sorrendben kell jönniük a hálózati csomagoknak).
    *   Belső hívási láncok vizualizálására (debugolásnál segít látni, ki kit hív).

---

# 2. Interakció diagram típusok (6-7. dia)

Négy típust különböztetünk meg:
1.  **Szekvencia diagram (Sequence Diagram):** A legnépszerűbb. Az idő fentről lefelé halad, az üzenetek sorrendjén van a hangsúly.
2.  **Kommunikáció diagram:** Az objektumok közötti kapcsolaton van a hangsúly, az üzeneteket sorszámozzuk (pl. 1, 1.1, 2).
3.  **Interaction Overview:** Olyan, mint egy aktivitásdiagram, ahol a csomópontok maguk is interakciók.
4.  **Időzítési diagram (Timing Diagram):** Precíz időzítéseket mutat (pl. "a válasznak 50 ms-on belül meg kell érkeznie").

---

# 3. Szekvenciadiagram alapvető elemei (8-12. dia)

*   **Életvonal (Lifeline):** Egy függőleges szaggatott vonal. Egy **szerepet** képvisel az interakcióban. 
    *   *FONTOS:* A fejlécében a nevet **nem húzzuk alá**, mert nem egy konkrét memóriabeli objektumot, hanem egy szerepet (role) jelöl.
*   **Üzenet (Message):**
    *   **Szinkron hívás (Tele nyílhegy):** A hívó fél megáll és vár a válaszra (blokkoló hívás).
    *   **Aszinkron üzenet (Nyitott nyílhegy):** A küldő továbbmegy, nem vár választ (pl. jelzés küldése).
    *   **Válaszüzenet (Szaggatott nyíl):** A szinkron hívás visszatérési értéke.
*   **Futási specifikáció (Execution Specification):** Az életvonalon lévő vékony téglalap. Azt jelzi, hogy az adott szereplő éppen dolgozik (aktív) vagy vár.
*   **Létrehozás és Törlés:** A `<<create>>` üzenet egy új életvonalat indít, a törlést (megsemmisülést) egy nagy **X** jelzi az életvonal alján.

---

# 4. Összetett logikai elemek (Combined Fragments) (13-14. dia)

Ha a forgatókönyvben elágazás vagy ciklus van, azt keretekkel (Fragment) jelöljük:
*   **alt (Alternatives):** Olyan, mint az `if-else`. Több ága van, de **pontosan egy** fog lefutni közülük az őrfeltételek alapján.
*   **opt (Optional):** Olyan, mint egy sima `if`. Vagy lefut a keret belseje, vagy semmi nem történik.
*   **loop:** Ciklus. A keretben lévő rész többször ismétlődik.
*   **break:** Megszakítás. Ha a feltétel teljesül, a keret lefut, és a diagram maradék része kimarad (mint a kivételkezelés vagy a `break` utasítás).
*   **par (Parallel):** Az ágak párhuzamosan, tetszőleges sorrendben futhatnak.

---

# 5. Újrafelhasználás (Interaction Use) (15-16. dia)

*   **ref keret:** Segítségével egy másik, már megtervezett interakcióra hivatkozhatunk. Ez segít a diagramokat áttekinthető méretűre bontani (dekompozíció).
*   **Gate (Kapu):** Azok a pontok a keret szélén, ahol az üzenetek "be- vagy kilépnek" a hivatkozott interakcióba.

---

# 6. Szemantika: Miért veszélyes a diagram? (20-25. dia) – *Kritikus vizsgapont!*

A szekvenciadiagram értelmezése nem olyan egyértelmű, mint gondolnánk. Az UML interakciók **részleges rendezést (Partial Order)** definiálnak.

### Alapszabály (23. dia):
1.  **Causality (Okság):** Egy üzenet fogadása (`?x`) csak a küldése (`!x`) **után** történhet meg.
2.  **Egy életvonalon belül:** Az események sorrendje kötött (fentről lefelé).
3.  **Életvonalak között:** Ha nincs köztük üzenet, akkor az eseményeik sorrendje **nem meghatározott**!

### Weak Sequencing (Gyenge sorrendezés) (24. dia):
Ez az alapértelmezett működés. 
*   **Példa:** Van két üzenet: `x` és `y`. Az `A` életvonalon előbb küldjük `x`-et, aztán `y`-t. A `B` életvonalon előbb fogadjuk `x`-et, aztán `y`-t.
*   **Kérdés:** Mi a sorrend a fogadott `x` (`?x`) és a küldött `y` (`!y`) között? 
*   **Válasz:** Nincs köztük kényszer! Lehet, hogy `B` hamarabb megkapja `x`-et, mint hogy `A` elküldené `y`-t, de az is lehet, hogy fordítva.

### Üzenetsorrend számozása (25. dia):
Vigyázat! A CASE eszközök gyakran megszámozzák az üzeneteket (1: m1, 2: m2). Ez elhiteti velünk, hogy m1 mindenképpen előbb van, mint m2. **De az elosztott rendszereknél ez nem biztos!** Ha m1 és m2 küldése között nincs függőség, bármelyik érkezhet előbb a célhoz.

---

# 7. Értelmezések (28. dia)

Mindig tisztázni kell, mi a modell célja:
*   **Érvényes (Valid) trace:** Olyan sorrend, ami megfelel a diagramnak.
*   **Érvénytelen (Invalid) trace:** Amit a diagram tilt (pl. egy `neg` keretben lévő sorozat).
*   **Nem meggyőző (Inconclusive):** Olyan eseménysor, amiről a diagram nem mond semmit.

---

### 🎓 Vizsgatippek:
1.  **Szimbólumok:** Tudd a különbséget a tele és a nyitott nyílhegy között (szinkron vs aszinkron).
2.  **Rendezés:** Értsd meg a "Weak Sequencing" fogalmát. Ne feledd: két különböző életvonalon történő esemény között csak akkor van sorrendiség, ha üzenet köti össze őket.
3.  **alt vs opt:** Az `alt`-nál kötelező választani egy ágat, az `opt`-nál el is maradhat a cselekvés.
4.  **ref:** Tudd, hogy ez a diagramok egymásba ágyazására és a bonyolultság csökkentésére való.

Sok sikert a vizsgához! Ha egy konkrét trace-sorozatot (mint a 20. dián) szeretnél elemezni, írd meg, és végigmegyünk rajta!