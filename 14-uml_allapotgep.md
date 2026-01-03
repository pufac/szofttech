Ez a diasor az **UML Állapotgépeket (State Machines)** dolgozza fel. Az állapotgépek a szoftvertechnológia „reaktív” oldalát mutatják be: hogyan változik a rendszer állapota külső vagy belső események hatására.

Íme a részletes, vizsgára fókuszáló magyarázat:

---

# 1. Alapfogalmak és Motiváció (1-6. dia)

Az állapotalapú modellezés olyan rendszerekhez való, amelyek **eseményvezéreltek**.

*   **Állapot (State):** A rendszer egy olyan helyzete, amelyben egy bizonyos feltétel (invariáns) igaz. Egy adott pillanatban a rendszer pontosan egy (egyszerű) állapotban van.
*   **Reaktív rendszerek (3. dia):** Olyan rendszerek, amelyek folyamatosan eseményekre várnak, és a válaszuk nemcsak az eseménytől, hanem az előtörténettől (az aktuális állapottól) is függ. *Példa: Egy bankautomata (ATM) máshogy reagál a „számbeírás” eseményre, ha épp PIN-kódot kér, és máshogy, ha a felveendő összeget.*
*   **Matematikai háttér (FSM - 4. dia):** Az állapotgép egy 5-ös fogat: $M = (S, I, O, f, g, s_0)$, ahol vannak állapotok, bemeneti/kimeneti ábécé, átmeneti függvény és kezdőállapot.
*   **Lefutás (Trace - 5. dia):** Események és válaszok sorozata. Az állapotgép meghatározza, mely sorozatok „érvényesek” (elfogadottak).

---

# 2. Állapotok és Átmenetek (7-8. dia)

Ez az állapotgép „szintaxisa” (hogyan rajzoljuk le):

*   **Állapot:** Lekerekített téglalap.
*   **Átmenet (Transition):** Nyíl a forrás és cél között.
*   **Kezdőállapot (Initial):** Tele fekete kör. Ez egy **pseudoállapot**, mert a rendszer nem „időzik” benne, csak megmutatja, hol indul a folyamat.
*   **Átmenet felirata (8. dia):** `esemény [őrfeltétel] / effektus`
    *   *Trigger:* Az esemény, ami kiváltja.
    *   *Guard (Őrfeltétel):* Logikai feltétel szögletes zárójelben; csak ha igaz, akkor tüzel az átmenet.
    *   *Effect (Effektus):* Egy rövid tevékenység, ami az átmenet közben hajtódik végre.

---

# 3. Összetett állapotok (Finomítás) (9-16. dia)

Ez a rész az UML állapotgépek ereje: a hierarchia.

*   **Egyszerű állapot:** Nincsenek alállapotai.
*   **Összetett állapot (Composite State):** Belül saját állapotgépe (régiója) van.
    *   **OR-finomítás (12. dia):** Hierarchikus. Ha a rendszer az `Off` állapotban van, akkor vagy `Standby`, vagy `Disconnected`. De nem mindkettő egyszerre!
    *   **AND-finomítás (13-14. dia):** Párhuzamos (ortogonális). Több régió van, és **mindegyikben** van egy aktív állapot.
    *   *Példa (GPS karóra):* Az `On` állapotban egyszerre fut a kijelző (`Image`) és a hang (`Sound`) kezelése. Beállíthatod a kijelzőt, miközben a hangot is némítod.

---

# 4. Állapotkonfiguráció és Történet (17-22. dia)

**Állapotkonfiguráció (18. dia):** Összetett rendszernél nem egy állapot aktív, hanem egy halmaz.
*   *Példa (20. dia):* `{On, SoundOn, Show, Clock}` – ez azt jelenti, hogy a gép be van kapcsolva, szól a hang, a kijelző mutat valamit, és konkrétan az órát mutatja.

**Belépés a régiókba (21. dia):**
*   *Implicit:* Csak az összetett állapotra mutat a nyíl $\to$ a belső kezdőállapotban indul.
*   *Explicit:* A nyíl közvetlenül egy belső állapotra mutat.

**History (Történet) (22. dia):** Egy kis körben lévő 'H' betű. Ha egy állapotból kilépünk (pl. hívás jön a telefonra), a History megjegyzi, hol tartottunk, és visszatéréskor nem a kezdőállapottól indul, hanem onnan, ahol abbahagytuk.
*   *Shallow (H):* Csak az aktuális szintet jegyzi meg.
*   *Deep (H*):* A teljes belső hierarchiát megjegyzi.

---

# 5. Belső viselkedések és Completion (23-26. dia)

Egy állapoton belül három speciális esemény lehet (23. dia):
1.  **entry:** Belépéskor azonnal lefut (pl. `lámpa_be()`).
2.  **exit:** Kilépés előtt azonnal lefut (pl. `naplózás()`).
3.  **doActivity:** Az állapotban való tartózkodás alatt fut (pl. `idő_frissítése()`). Ez hosszan tarthat és megszakítható.

**Completion Transition (24. dia):** Olyan nyíl, aminek nincs felirata. Akkor tüzel automatikusan, ha az állapot belső munkája (a `doActivity`) befejeződött.

---

# 6. Végrehajtási szemantika (RTC) (27-33. dia)

**Run-to-Completion (RTC) elv:** A legfontosabb szabály! Amíg a rendszer egy eseményt feldolgoz és átmegy az új állapotba, addig **nem foglalkozik új eseménnyel**. Az események egy sorba (pool) kerülnek.

**Konfliktusfeloldás (30. dia):** Mi van, ha két nyíl is elindulhatna ugyanarra az eseményre?
*   **Prioritás:** Mindig a **beljebb lévő** (specifikusabb) állapot átmenete győz a kinti (általánosabb) szemben.
*   *Példa:* Ha az autó „Vészhelyzet” állapotban van, az ottani „Fék” esemény fontosabb, mint a sima „Vezetés” állapot „Fék” eseménye.

---

# 7. Implementációs minták (34-41. dia)

Hogyan lesz ebből kód?

1.  **Nested Switch (Egymásba ágyazott switch - 40. dia):**
    *   Külső switch: melyik állapotban vagyunk?
    *   Belső switch: milyen esemény jött?
    *   *Előnye:* Egyszerű, nem kell hozzá könyvtár. *Hátránya:* Bonyolult gépnél átláthatatlan „spagetti” kód lesz.
2.  **State Table (Állapottábla - 41. dia):**
    *   Egy 2D tömb: `tábla[állapot][esemény]`. A cellában van a következő állapot és a végrehajtandó függvény.
    *   *Előnye:* Nagyon gyors és matematikai pontosságú.
3.  **State Pattern (Tervezési minta):** Objektumorientált megoldás, ahol minden állapot egy külön osztály (ezt a Szoftvertechnikák tárgyban tanuljátok részletesen).

---

### 🎓 Vizsgatippek:
*   **AND vs OR finomítás:** Tudd megkülönböztetni a szaggatott vonalat (AND - párhuzamos) a sima alállapotoktól (OR - választás).
*   **Prioritás:** Mindig a legmélyebben lévő alállapot átmenete az erősebb!
*   **RTC:** Értsd, hogy a feldolgozás atomi, nem szakítható félbe egy újabb eseménnyel.
*   **History:** Tudd, mi a különbség a sima H és a H* között (a H* „emlékszik” az al-al-állapotokra is).

Sok sikert a felkészüléshez! Ha egy konkrét ábrát (pl. a 31. dián lévő prioritás példát) szeretnél elemezni, írj!