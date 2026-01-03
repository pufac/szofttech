Ez a diasor az **UML aktivitásmodelleket** (Activity Models) mutatja be mélyrehatóan. Míg az osztálydiagram a rendszer statikus vázát adja meg, az aktivitásdiagram a **folyamatokat, munkafolyamatokat és algoritmusokat** írja le.

A vizsgán a legfontosabb rész a **vezérlési csomópontok** (fork, join, decision, merge) és a **tokenjáték** (végrehajtási szemantika) pontos ismerete.

---

# 1. Alapfogalmak és felhasználás (1–6. dia)

Az aktivitásdiagram a viselkedési modellek közé tartozik.

*   **Mi a folyamat? (3. dia):** Egymással összefüggő tevékenységek halmaza, amely bemeneteket kimenetekké alakít. Rokonai a folyamatábrák (flow chart) és a GANTT diagramok.
*   **Mire használjuk? (4. dia):**
    1.  **Magas szinten:** Üzleti folyamatok leírása (pl. egy webshop rendelési folyamata: kosárba rakás -> fizetés -> szállítás). Gyakran a **használati esetek (Use Case)** részletes kifejtésére használják.
    2.  **Alacsony szinten:** Egy bonyolult algoritmus vagy metódus belső logikájának specifikálása (ciklusok, elágazások).
*   **Párhuzamosság (6. dia):** Az aktivitások alapvetően **párhuzamos végrehajtást** engednek meg. Ha két lépés között nincs függőség, azok elméletben egyszerre is futhatnak.

---

# 2. Vezérlési folyam elemei (7–19. dia)

### A. Elemi egység: Akció (Action) (8. dia)
Egy lekerekített téglalap. Ez egy elemi lépés (pl. "Email küldése"). Nem bontjuk tovább ezen a szinten.

### B. Kezdő és végpontok (9, 17. dia) – *Fontos különbség!*
*   **Initial Node (Tele pötty):** Itt indul a folyamat. Lehet több is, ekkor több szálon indul el a végrehajtás egyszerre.
*   **Activity Final (Pötty körrel):** Megállítja a **teljes** aktivitást. Minden szál megszűnik.
*   **Flow Final (Körben X) (17. dia):** Csak az **adott szálat** öli meg. Ha a porszívónál a "Szenzor figyelés" ág eléri a Flow Finalt, a "Motor hajtás" ág még futhat tovább.

### C. Elágazás és Összevonás (Decision & Merge) (11–13. dia)
*   **Decision (Üres rombusz):** Egy bemenet, több kimenet. A kimenő ágakon **őrfeltételek (guards)** vannak (szögletes zárójelben: `[feltétel]`). **Fontos:** Csak egyetlen ágon mehet tovább a vezérlés! (XOR logika).
*   **Merge (Üres rombusz):** Több bemenet, egy kimenet. Nem vár senkire: amint bármelyik ágon érkezik valami, továbbengedi.

### D. Párhuzamosítás és Szinkronizáció (Fork & Join) (14. dia)
*   **Fork (Vastag fekete vonal):** Egy szálat szétbont több, párhuzamosan futó szálra.
*   **Join (Vastag fekete vonal):** **Szinkronizációs pont**. Megvárja, amíg az **összes** bejövő ág befejeződik, és csak akkor engedi tovább a folyamatot egyetlen szálon.

---

# 3. Adatfolyam modellezése (20–27. dia)

Az aktivitásdiagram nemcsak azt mondja meg, mi után mi jön, hanem azt is, hogy az adatok hogyan vándorolnak.

*   **ObjectNode (21. dia):** Egy téglalap, ami adatot reprezentál.
*   **Pin (21. dia):** Az akciók szélére rajzolt kis négyzetek. Ez az akció "be- és kimenete" (mint egy függvény paraméterei).
*   **Vezérlés vs. Adat (24. dia):** Az adatfolyam (ObjectFlow) magában hordozza a vezérlést is. Ha az "A" akció egy adatot ad a "B"-nek, akkor "B" nem indulhat el "A" előtt.

---

# 4. Végrehajtási szemantika: A Tokenjáték (28–50. dia)

Ez a rész magyarázza meg, hogyan "működik" a diagram. Képzeljük el, hogy apró bogyók (tokenek) vándorolnak az éleken.

*   **Szabályok:**
    *   Egy akció akkor indul el (tüzel), ha **minden** bemeneti pinjén és élén van token.
    *   A **Fork** minden kimenetére tesz egy-egy másolatot a tokenből.
    *   A **Join** csak akkor ad ki tokent, ha **minden** bemenetére érkezett egy.
    *   A **Decision** csak az egyik (igaz) irányba engedi a tokent.

---

# 5. Tanácsok és Tipikus hibák (51–59. dia) – *Várható vizsgakérdés!*

A legtöbb pontot a **Deadlock (holtpont)** felismerésével lehet szerezni a vizsgán.

### Tipikus hiba 1: Decision után Join (54-55. dia)
Ha egy rombuszból (Decision) elágazunk, majd egy vastag vonallal (Join) akarjuk összevárni, az **Deadlock**. Miért? Mert a Decision csak az egyik ágon küld tokent, a Join viszont az összeset várja. Soha nem fog továbbmenni a folyamat.
*   **Megoldás:** Decision után Merge (rombusz) kell.

### Tipikus hiba 2: Fork után Merge
Ha a Fork szétválasztja a szálakat, de Merge-be futtatjuk őket, akkor a rákövetkező akció **kétszer** fog lefutni (minden beérkező tokenre egyszer). Ez általában nem szándékos hiba.

### Jótanácsok (58. dia):
*   A folyamat bal felülről induljon és jobb alul végezzen.
*   Az őrfeltételek (`[ ]`) fedjék le az összes lehetőséget, de ne legyen átfedés köztük (pl. ne legyen egyszerre `[x > 0]` és `[x >= 0]`).
*   Használjunk **Partíciókat (Swimlanes)** (27. dia): Függőleges sávok, amik megmutatják, ki a felelős az adott részért (pl. "Vevő", "Szerver", "Bank").

---

### 🎓 Vizsgatippek összefoglalva:
1.  **Fork/Join vs. Decision/Merge:** Mindig nézd meg, hogy üres rombusz (választás) vagy vastag vonal (párhuzamosság) van-e ott.
2.  **Holtpont keresés:** Ha látsz egy Join-t, nézd meg a bemeneteit. Van rá esély, hogy valamelyik ágon soha nem érkezik token? Ha igen -> Deadlock.
3.  **Flow Final vs. Activity Final:** Kicsi kör X-szel (Flow) = csak egy szál hal meg. Pötty körben (Activity) = a porszívó is kikapcsol, a program kilép.

Szeretnéd, hogy egy konkrét példán (pl. a 12. dián lévő ciklusnál) végigjátszuk a tokeneket?