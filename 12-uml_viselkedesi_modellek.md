Ez a diasor az **UML viselkedési modellek** alapjaiba vezeti be a hallgatót. Míg a strukturális modellek (mint az osztálydiagram) azt írják le, hogy *miből áll* a rendszer, a viselkedési modellek azt mutatják be, hogyan *működik* az időben, hogyan reagál az eseményekre.

Íme a részletes, vizsgaközpontú feldolgozás:

---

# 1. Bevezetés és Alapkérdések (1-6. dia)

A viselkedésmodellezés célja a rendszer dinamikájának leírása. A következő kérdésekre keresünk választ (5. dia):
*   **Hogyan változik az állapot az időben?** (pl. be van-e kapcsolva a gép?)
*   **Mik az elvárt és tiltott viselkedések?** (pl. ne lehessen pénzt kivenni fedezet nélkül.)
*   **Hogyan reagál a külvilágra?** (eseményvezérelt működés.)
*   **Milyen sorrendben következnek a lépések?** (folyamatleírás.)

### Három fő megközelítés (5. dia):
1.  **Állapotalapú (State-based):** A rendszer állapotai és az azok közötti átmenetek (pl. Állapotgép).
2.  **Vezérlési folyam (Control-flow):** A műveletek egymásutánisága (pl. Aktivitásdiagram).
3.  **Adatfolyam (Data-flow):** Hogyan vándorolnak az adatok a feldolgozó egységek között.

**Mit modellezünk? (6. dia):** Leírhatunk egy apró belső algoritmust (kódszint), egy gép működését (pl. kávégép válaszai), vagy akár komplex hálózati protokollokat (pl. TCP kézfogás).

---

# 2. Az UML hatóköre: Diszkrét vs. Folytonos (7. dia)

Ez egy fontos elméleti határvonal:
*   **UML modellezi:** A **diszkrét** idejű és értékű viselkedést. Véges számú állapotunk van, az átmenetek pillanatszerűek, és eseményekre reagálunk.
*   **UML NEM modellezi:** A **folytonos** rendszereket. Ha differenciálegyenletekkel leírható fizikai folyamatokról (pl. egy motor fordulatszámának finom szabályozása) van szó, akkor nem UML-t, hanem pl. MATLAB/Simulinket használunk.

---

# 3. Az UML viselkedési modellcsaládjai (8-9. dia)

Az UML három fő eszközt ad a kezünkbe:

1.  **Állapotgép (State Machine):** A rendszer diszkrét állapotait mutatja (mint a főnevek). Megmutatja, milyen eseményre milyen válasz érkezik.
2.  **Aktivitás (Activity):** A lépéseket, akciókat írja le (mint az igék). Meghatározza a sorrendiséget és a függőségeket.
3.  **Interakciók (Interaction):** Ide tartozik a **szekvenciadiagram**, a kommunikációs diagram és az időzítési diagram.
    *   **FONTOS (9. dia):** Az állapotgéppel ellentétben az interakció diagramok **nem a teljes viselkedést** írják le, hanem csak **forgatókönyveket** (scenariokat). Pl. a szekvenciadiagram egyetlen konkrét sikeres lefutást mutat be, nem az összes lehetséges hibát.

---

# 4. Közös elemek és "Lefutások" (10-12. dia)

### Hogyan történik a végrehajtás? (10. dia)
*   A **Viselkedés (Behavior)** akciókat hajt végre.
*   Az **Esemény (Event)** valami, ami megtörténik (pl. gombnyomás).
*   Az **Üzenet (Message)** közvetíti az igényt (hívás vagy jelzés).
*   **Tanács:** A küldés és a fogadás két külön esemény! Ezért modellezhető az, hogy egy hálózaton az üzenet késik vagy elveszik.

### Lefutások / Trace-ek (11-12. dia)
Egy rendszer elvileg végtelen sokféle dolgot csinálhatna. A modellünk célja, hogy **korlátozza** ezt a halmazt az "elfogadott/elvárt" lefutásokra.
*   **Szimuláció:** Megnézzük, mi történik egy adott bemenetre a modell szerint.
*   **Verifikáció:** Megvizsgáljuk az *összes* lehetséges lefutást, hogy biztosan nem kerülünk-e rossz állapotba (pl. holtpont).

---

# 5. Események és Aktív Objektumok (13-14. dia)

### Eseménytípusok az UML-ben (13. dia):
1.  **TimeEvent:** Időzítés (pl. "5 másodperc után" vagy "éjfélkor").
2.  **ChangeEvent:** Amikor egy logikai feltétel igazzá válik (pl. `hőmérséklet > 100`).
3.  **MessageEvent:** Üzenet érkezése (metódushívás vagy szignál).

### Aktív Objektum (Active Object) (14. dia)
Olyan objektum, amelynek **saját "élete" (szála)** van. Létrehozás után azonnal elindul a belső viselkedése, és önállóan cselekszik.
*   **Veszély:** Ha több aktív objektum van, megjelennek a **konkurencia problémák** (holtpont, versenyhelyzet).
*   **Miért modellezzük?** Mert ezeket a hibákat teszteléssel nagyon nehéz megtalálni (időzítésfüggőek), de modellezéssel és verifikációval még a tervezőasztalon kiderülhetnek.

---

### Összefoglaló a vizsgához:
1.  **Három alapdiagram:** Állapotgép (állapotok), Aktivitás (folyamat), Szekvencia (forgatókönyv).
2.  **UML korlátja:** Csak diszkrét viselkedést modellez.
3.  **Interakció vs. Teljes modell:** A szekvenciadiagram csak egy trace-t (lefutást) mutat be, az állapotgép az egész rendszert.
4.  **Aktív objektum:** Saját végrehajtási szála van, párhuzamossági hibákat okozhat.

Ha készen állsz, folytathatjuk a konkrét diagramtípusok (Aktivitás vagy Állapotgép) részletesebb feldolgozásával!