Ez a diasor a **szoftverprojektek menedzseléséről, ütemezéséről és méréséről** szól. A szoftverfejlesztés nem csak kódolás, hanem erőforrások, idő és költségek összehangolása is. A vizsgán a mérések (EVA), az ütemezés (GANTT/PERT) és a becslési módszerek (COCOMO) a legfontosabbak.

Íme a részletes feldolgozás:

---

# 1. Projekt alapfogalmak (1–12. dia)

### Mi a projekt? (5. dia)
A projekt egy **menedzselt folyamat**, amely:
*   Meghatározott időtartamú (van kezdete és vége).
*   Célja egy konkrét termék vagy szolgáltatás átadása.
*   Erőforrásokat (emberek, pénz, eszközök) használ fel.
*   Felelőse és csapata van.

### Skálázódás (6. dia)
A projektmenedzsment módszerei változnak a projekt méretétől függően:
*   **Kis projekt:** 4-8 ember, pár hónap (pl. egy új mobil app funkció).
*   **Óriásprojekt:** 10+ év, több száz ember, több ezer oldalnyi dokumentáció (pl. egy atomerőmű vagy egy helikopter szoftverrendszere).

### PRINCE2 keretrendszer (7–8. dia)
A **PRINCE2** (*PRojects IN Controlled Environments*) egy brit kormányzati eredetű, nemzetközileg elterjedt módszertan.
*   **7 téma köré épül:** Üzleti eset (megéri-e?), Szervezet (ki mit csinál?), Minőség, Terv, Kockázat, Változás, Haladás.
*   Segít kontrollált mederben tartani a fejlesztést.

### Tipikus dokumentumok (9. dia) – *Vizsgán fontosak!*
*   **Project Charter (Alapító dokumentum):** A projekt "alkotmánya" (célok, keretek).
*   **Project Handbook (Kézikönyv):** A szabályok gyűjteménye (hogyan kommunikálunk?).
*   **Quality Assurance Handbook:** Hogyan mérjük a minőséget?
*   **Final Project Report:** Záró jelentés, "post-mortem" elemzés (mit tanultunk?).

### A menedzsment "szentháromsága" (10. dia)
A három fő kényszer: **Költség (Budget), Idő (Time), Terjedelem (Scope)**.
*   **Szabály:** Nem lehet mind a hármat egyszerre maximalizálni. Ha több funkciót akarsz (Scope), több időbe vagy pénzbe fog kerülni. A minőség (Quality) ezen tényezők metszetében áll.

---

# 2. Feladatok lebontása és ütemezése (13–21. dia)

A projektet kezelhető darabokra kell bontani.

### WBS – Work Breakdown Structure (15–16. dia)
A **WBS** a projekt hierarchikus lebontása. 
*   A legfelső szint maga a projekt, amit **munkacsomagokra (Work Package - WP)** bontunk.
*   A legalsó szinten a konkrét feladatok és a **deliverable-ök (leszállítandók)** vannak.
*   *Példa:* NASA WBS – látszik, hogyan válik ketté a szoftver, a hardver és a menedzsment ág.

### GANTT-diagram (18–19. dia)
Ez egy idővonalas ábrázolás. Megmutatja:
*   Melyik feladat meddig tart.
*   **Függőségeket (19. dia):**
    *   *Finish-to-Start (FS):* "B" csak akkor kezdődhet, ha "A" befejeződött (a leggyakoribb).
    *   *Start-to-Start (SS):* Egyszerre kell elkezdeni őket.
    *   *Finish-to-Finish (FF):* Egyszerre kell befejezni őket.

### Kritikus út és Tartalék (Slack) (20. dia) – !!! VIZSGAPONT !!!
*   **Kritikus út:** Azoknak a feladatoknak a láncolata, amelyeknél **ha bármelyik késik egy napot, az egész projekt késni fog egy napot**. Itt nincs tartalék idő.
*   **Tartalék (Slack):** Az az idő, amennyit egy feladat késhet anélkül, hogy a projekt befejezési dátumát kitolná.

### PERT-diagram (21. dia)
Egy irányított gráf, ami a feladatok logikai sorrendjét mutatja. Segít kiszámolni a projekt várható időtartamát a leghosszabb út (kritikus út) alapján.

---

# 3. Költségek követése: EVA (22–31. dia) – !!! KIEMELTEN FONTOS !!!

A vizsgák egyik leggyakoribb számítási feladata az **Earned Value Analysis (EVA)**.

### Alapfogalmak (24. dia):
1.  **PV (Planned Value):** Mennyit terveztünk elkölteni az adott időpontig?
2.  **AC (Actual Cost):** Mennyit költöttünk el ténylegesen?
3.  **EV (Earned Value):** A ténylegesen elvégzett munka értéke a tervek szerint. (Pl. ha a 10 milliós munka 40%-a kész, akkor az EV = 4 millió).

### Metrikák (26. dia):
*   **Költségeltérés (CV = EV – AC):** Ha negatív, túlléptük a keretet.
*   **Ütemterv eltérés (SV = EV – PV):** Ha negatív, csúszásban vagyunk.
*   **CPI (EV / AC):** Költséghatékonyság. Ha < 1, drágábban dolgozunk a tervezettnél.
*   **SPI (EV / PV):** Haladási sebesség. Ha < 1, lassabbak vagyunk.

*Példa (27. dia):* Ha a terv szerint 50-nél kéne járnunk (PV), de csak 30 az értékünk (EV) és 35-öt költöttünk (AC), akkor késünk is és drágák is vagyunk.

---

# 4. Költség- és méretbecslés (32–43. dia)

Mielőtt elindul a projekt, meg kell becsülni, mennyi ideig tart majd.

### COCOMO modell (35–37. dia) – !!! VIZSGAPONT !!!
A *COnstructive COst MOdel* a forráskód becsült méretére (**KLoC** - ezer sor kód) alapoz.
*   **Képlet:** $Effort = a \times (KLoC)^b \times EAF$
*   $a, b$: Konstansok a projekt típusától függően (Organic - egyszerű, Embedded - bonyolult beágyazott).
*   **EAF (Effort Adjustment Factor):** Költségszorzók (pl. a csapat tapasztalata, az adatbázis mérete - 36. dia).

### Funkciópontok (Function Points - FP) (41. dia)
Nem a kódsorokat számoljuk (mert az nyelvfüggő), hanem a szoftver funkcióit:
*   Bemenetek, kimenetek száma.
*   Lekérdezések, adatfájlok, interfészek száma.
Mindegyikhez rendelünk egy súlyt (Complexity), és ezeket összeadjuk.

---

# 5. PM a gyakorlatban és az MI (44–51. dia)

### Big Tech vs. KKV (45–46. dia)
*   A **Google, Amazon, Netflix** típusú cégek hírhedtek arról, hogy nincs központi módszertanuk. A csapatok nagy autonómiát kapnak (**Plan-Build-Ship** ciklus), de a tervezési dokumentáció (Design Doc) kötelező.
*   Magyarországon a cégek 60%-a Agilis/Scrum módszertant használ (48. dia).

### DORA metrikák (49–50. dia) – *Modern mérőszámok!*
A DevOps csapatok teljesítményét ma már ezzel mérik:
1.  **Deployment Frequency:** Milyen gyakran élesítünk? (Elite: naponta többször).
2.  **Lead Time for Changes:** Mennyi idő telik el a commit és az élesítés között?
3.  **Time to Restore Service:** Mennyi idő alatt javítjuk ki, ha leáll a rendszer?
4.  **Change Failure Rate:** Az élesítések hány százaléka bukik el?

### Az MI hatása (51. dia)
A 2024-es adatok szerint:
*   A fejlesztők 75%-a használ már MI-t.
*   **3-7% termelékenységnövekedést** hoz.
*   Bár sokan használják kódíráshoz, 39% még mindig bizalmatlan az MI által generált kód minőségével szemben.

---

### Összefoglaló a vizsgához:
1.  **Projekt kényszerek:** Tudd a Scope-Idő-Pénz háromszöget.
2.  **EVA számítás:** Értsd a PV, AC, EV összefüggéseit. Tudd kiszámolni a CPI-t és SPI-t!
3.  **Kritikus út:** Tudd definiálni (leghosszabb út, nulla tartalékidő).
4.  **COCOMO:** Mire épül? (KLoC + szorzók).
5.  **DORA:** Sorold fel a 4 fő metrikát.

Sok sikert a vizsgára! Ha bármelyik EVA képlet vagy a GANTT függőségek nem világosak, írj, és hozok rá gyakorló példát!