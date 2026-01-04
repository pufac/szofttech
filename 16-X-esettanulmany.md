Ez a diasor egy **esettanulmányon (a BME-s Házi Feladat Portál fejlesztésén)** keresztül mutatja be, hogyan kapcsolódnak össze a félév során tanult UML diagramok és tervezési elvek egy valódi projektben.

A vizsgára készüléshez a legfontosabb, hogy ne csak a definíciókat tudd, hanem azt is, **melyik diagramot melyik fázisban és miért használjuk.**

---

# 1. Bevezetés és az Életciklus (1–4. dia)

A projekt a klasszikus **V-modellre** épül (4. dia), ami a fejlesztési fázisokat és a hozzájuk tartozó ellenőrzési (tesztelési) szinteket mutatja be párhuzamosan:
*   **Bal szár (Tervezés):** Követelmények $\to$ Rendszerterv $\to$ Architektúra $\to$ Részletes tervek.
*   **V alja:** Implementáció (Kódolás).
*   **Jobb szár (Ellenőrzés):** Egységteszt $\to$ Integrációs teszt $\to$ Rendszerteszt $\to$ Validáció.

---

# 2. Követelmények (5–11. dia)

A modern fejlesztésben (2023 után) a hangsúly a 30 oldalas dokumentációk helyett az **agilis munkafolyamaton** és a **folyamatos visszajelzésen** van (6. dia).

### Projektmenedzsment szentháromság (10. dia):
Ez egy fontos elméleti alapvetés. Három tényező van: **Funkciók, Pénz, Idő**.
*   **Szabály:** Csak kettőt választhatsz, amit fixálsz, a harmadikban kompromisszumot kell kötni.
*   **A portál esete:** Az idő fix (félév vége), a pénz fix (0 Ft), tehát a **Funkciókból** kellett engedni (priorizálás: Must have vs. Nice to have).

### Származtatott követelmények (11. dia):
Nem minden követelmény jön közvetlenül az ügyféltől. Van, ami **kényszerekből** fakad.
*   *Példa:* "Pénzügyi keret 0 Ft" $\to$ származtatott követelmény: "Nem használhatunk fizetős felhő szolgáltatásokat (pl. GitHub Actions), saját infrastruktúrán kell futtatni mindent."

---

# 3. Rendszerterv: Use Case és Aktivitás (12–17. dia)

### Használati esetek (Use Case) (13. dia):
Itt dől el, kik a szereplők (**Aktorok**) és mik a fő céljaik.
*   *Példa:* A `Student` megtekintheti az állapotát (`View Status`). A `Teacher` felülbírálhatja azt (`Override Status`).
*   **Kapcsolatok:** Az `Override Status` **«include»** kapcsolatban van a `View Status`-szal (ahhoz, hogy felülírd, látnod kell).

### Forgatókönyv vs. Aktivitás diagram (17. dia):
Ez egy tipikus vizsgakérdés: mikor melyiket?
*   **Szöveges forgatókönyv:** Egyszerűbb, bárki megérti, de a párhuzamos lépéseket nehéz leírni vele.
*   **Aktivitás diagram:** Kötött jelölésrendszer, de kiválóan ábrázolja a **párhuzamosságot** és az **adatfolyamot**.

---

# 4. Architektúra (18–23. dia)

A portál **többrétegű kliens-szerver architektúrát** használ (19. dia).
*   **Külső függőségek:** Moodle (LTI protokollon keresztül), GitHub, SonarQube.
*   **Rétegek (22. dia):**
    *   *Szerver:* Megjelenítési réteg $\to$ Üzleti logika $\to$ Adatelérési réteg.
    *   *Kliens:* GUI $\to$ Adatelérés.

---

# 5. Teljesítmény modellezés (24–29. dia) – !!! VIZSGAPONT !!!

Ez a rész technikailag a legnehezebb, figyelj az alapfogalmakra (25. dia):
*   **Érkezési ráta ($\lambda$):** Egységnyi idő alatt beérkező kérések száma.
*   **Átbocsátás ($X$):** Egységnyi idő alatt feldolgozott kérések száma.
*   **Egyensúly:** Ha $\lambda = X$.

### A "Vergődés" (Thrashing) (27–28. dia):
A gyakorlatban, ha túl sok kérés jön ($\lambda$ túl nagy), a rendszer teljesítménye nem csak megáll, hanem **visszaesik**, sőt összeomolhat.
*   **Miért?** Mert az erőforrások (CPU, RAM) elmennek a **járulékos feladatokra**: taszkváltás (context switch), memória-felszabadítás (Garbage Collection). A gép többet foglalkozik az adminisztrációval, mint a hasznos munkával.
*   **Megoldás (29. dia):**
    *   *Vertikális skálázás:* Erősebb gép.
    *   *Horizontális skálázás:* Több gép (fürtözés).
    *   *Buffer (Várólista):* Ha betelik, inkább dobjuk el az új kérést (mint a Neptun túlterheléskor), de a bent lévők kiszolgálása maradjon stabil.

---

# 6. Interakciók és Részletes terv (33–42. dia)

### Szekvencia diagram (33-34. dia):
Azt mutatja meg, hogyan "beszélgetnek" a komponensek. Fontos, hogy mindenki csak azt hívhatja, akivel kapcsolatban van (interfész).

### Fogalmi modell (40–42. dia):
Osztálydiagram, ami a tartomány (domain) fogalmait rögzíti.
*   *Érdekesség:* **Asszociációs osztályok** használata. Pl. a `User` és a `Task` között a `TaskInstance` tárolja a konkrét hallgató eredményét egy konkrét feladaton.

---

# 7. Típuslekérdezés és Double Dispatch (43–45. dia) – !!! VIZSGAPONT !!!

Gyakori probléma: Van egy listánk feladatokból (`Task`), de tudnunk kellene, hogy az éppen egy `GitHubTask` vagy `SonarQubeTask`.

*   **Dinamikus megoldás (44. dia):** `instanceof` használata. **Üzleti logikában kerülendő**, mert nehéz karbantartani (ha jön egy új típus, minden `if-else`-t át kell írni).
*   **Statikus megoldás (Double Dispatch) (45. dia):** 
    1.  Meghívjuk a `task.do()` metódust.
    2.  A konkrét feladat (pl. `GitHubTask`) visszahívja a kezelőt: `handler.handleGitHubTask(this)`.
    *   **Előny:** A típus eldöntése fordítási időben történik, nincs szükség csúnya típusellenőrzésekre.

---

# 8. Implementáció és Üzemeltetés (53–60. dia)

*   **Git mágia (54. dia):** 700 hallgató kezeléséhez hallgatónként egy külön `remote`-ot (távoli tárhelyet) vettek fel.
*   **Kódgenerálás (56. dia):** Az adatsémából generálták az adatelérési réteget, hogy ne kelljen kézzel unalmas kódot írni.
*   **Monitorozás (58. dia):** Nem elég megírni a kódot, figyelni kell az éles üzemet. A dián látszik, hogyan ugrál meg a CPU használat a beadási határidők (heti workload) környékén.

---

### Összefoglaló a vizsgához:
1.  Értsd a **V-modell** fázisait.
2.  Tudd a **teljesítmény alapfogalmakat** ($\lambda, X$) és a **vergődés** okát.
3.  Tudd megindokolni, miért jobb a **Double Dispatch**, mint az `instanceof`.
4.  Értsd az **architektúra** hatását a teljesítményre (hány komponensen megy át egy kérés).

Sok sikert a tanuláshoz! Ha valamelyik technikai rész (pl. a Double Dispatch kódja) nem világos, írj bátran!