Ez a diasor a szoftvertechnológia egyik legfontosabb "humán" és mérnöki határterületét, a **követelménykezelést (Requirement Engineering)** dolgozza fel. A szoftverhibák jelentős része nem kódolási hiba, hanem félreértett vagy hiányzó követelmény.

Íme a részletes, vizsgára fókuszáló feldolgozás:

---

# 1. Alapvetések: Miért nehéz ez? (1-7. dia)

A követelménykezelés célja az **igények azonosítása** és pontos megfogalmazása.

*   **A legnagyobb kihívás (5. dia):** A megrendelő gyakran **nem tudja pontosan, mit akar**, vagy nem informatikai nyelven fogalmaz. Üzleti problémája van, amire megoldást vár.
*   **Tree Swing ábra (6. dia):** Ez egy klasszikus szakmai vicc. Bemutatja, hogy a lánc minden szeme (ügyfél, elemző, programozó, üzemeltető) mást értett meg, és a végén a termék köszönőviszonyban sincs azzal, amire az ügyfélnek valójában szüksége lett volna.
*   **GenAI szerepe (7. dia):** A mesterséges intelligencia (pl. kódgenerálás) korában a **pontos specifikáció felértékelődik**. Ha rossz az utasítás, az MI gyorsan fog generálni egy tökéletesen rossz kódot.

---

# 2. Mi a követelmény? (8-13. dia)

**Definíció (9. dia):** Olyan feltétel vagy képesség, ami a felhasználónak kell egy probléma megoldásához, vagy amit a rendszernek teljesítenie kell egy szerződés/szabvány szerint.

### Aranyszabály: MIÉRT és nem a HOGYAN (10. dia)
A követelménynek azt kell leírnia, hogy **mit** kell tudnia a rendszernek és **miért**, de **nem a technikai megoldást** (hogyan) kell megadnia.
*   *Rossz példa:* "Legyen egy SQL tábla a rendeléseknek." (Ez hogyan).
*   *Jó példa:* "A felhasználónak azonnal értesülnie kell az új rendelésekről." (Ez miért/mit).

### IREB alapelvek (12-13. dia)
Az IREB a nemzetközi követelménykezelő szervezet. Főbb elveik:
*   **Érintettek (Stakeholders):** Az igények forrásai (nem csak a vevő, hanem az üzemeltető, a hatóság is!).
*   **Környezet (Context):** A rendszert csak a környezetével együtt lehet megérteni.
*   **Evolúció:** A követelmények folyamatosan változnak, ez normális.

---

# 3. Követelmények fajtái (14-18. dia)

1.  **Funkcionális követelmény:** Mit csinál a rendszer? (pl. "A rendszer tudjon számlát generálni.")
2.  **Extra-funkcionális (nem-funkcionális) követelmény:** Hogyan/milyen minőségben működik? (pl. teljesítmény, biztonság, megbízhatóság).

### FURPS+ modell (18. dia) – *Fontos vizsgapont!*
Ez egy mozaikszó a minőségi jellemzőkre:
*   **F**unctionality (Funkcionalitás)
*   **U**sability (Használhatóság)
*   **R**eliability (Megbízhatóság)
*   **P**erformance (Teljesítmény)
*   **S**upportability (Támogathatóság)
*   **+** (Egyéb: jogi kényszerek, fizikai korlátok).

---

# 4. Dokumentációs módszerek (19-30. dia)

A követelménykezelés folyamata (19. dia): **Felmérés (Elicitation) → Dokumentálás → Validáció (Ellenőrzés) → Menedzsment.**

### Precizitás vs. Költség (23-24. dia)
Van egy alapvető **trade-off** (kompromisszum):
*   Minél precízebb a leírás, annál kevesebb a hiba, de annál több időbe és pénzbe kerül megírni.
*   *Példa:* Egy mobiljátékhoz elég egy vázlatos leírás, de egy atomerőműhöz matematikai precizitás kell.

### User Story (27-30. dia) – *Agilis módszer*
Formátuma: **„Én, mint <felhasználó típus>, <valamit akarok>, azért, hogy <cél/indok>.”**
*   *Példa:* „Én, mint könyvtártag, online meg akarom hosszabbítani a könyveket, hogy ne kelljen bemennem személyesen.”

**INVEST kritériumok (30. dia) – *Kiemelt vizsgakérdés!***
Egy jó User Story:
*   **I**ndependent (Független)
*   **N**egotiable (Alkuképes – nem kőbe vésett szerződés)
*   **V**aluable (Értéket ad)
*   **E**stimable (Becsülhető a mérete)
*   **S**mall (Kicsi – belefér egy iterációba)
*   **T**estable (Tesztelhető)

---

# 5. Kritikus rendszerek és Követhetőség (31-40. dia)

### Követhetőség (Traceability) (31-32. dia)
*   **Előrefelé (Forward):** Megmutatja, hogy egy követelményt melyik kódrészlet valósít meg és melyik teszt ellenőriz.
*   **Hátrafelé (Backward):** Egy kódrészletről megmondja, melyik követelmény miatt létezik. Ha nincs hozzá követelmény, akkor felesleges a kód!
*   **NASA példa (34. dia):** Egy Mars-szonda azért zuhant le, mert egy rendszerkövetelmény (szoftveres védelem a szenzorhibára) nem került át a szoftverfejlesztőkhöz.

### Strukturált szöveg és Segédigék (36-37. dia)
Kritikus rendszereknél (pl. vasúti ETCS - 39. dia) sablonokat használnak: **Alany + Segédige + Ige + Tárgy + Feltétel.**
A segédigék jelentése szabványosított:
*   **Shall/Must:** Kötelező.
*   **Should:** Ajánlott.
*   **May:** Opcionális.

---

# 6. Követelmények ellenőrzése (Review) (46-61. dia)

**Miért fontos? (48. dia):** Minél később veszünk észre egy hibát, annál drágább javítani. Ha a tervezéskor (Concept) találjuk meg, olcsó. Ha már az üzemeltetéskor (Production), az költség-katasztrófa.

### Felülvizsgálat (Review) szintjei (50. dia)
1.  **Ad-hoc / Informális:** Csapattárs ránéz.
2.  **Walkthrough (Átvizsgálás):** A szerző vezeti végig a többieket a dokumentumon.
3.  **Technical review:** Szakértők bevonása.
4.  **Inspection (Vizsgálat):** A legformálisabb. Moderátor vezeti, ellenőrző listák (checklists) alapján pontról pontra nézik át.

### Specification by Example (Gherkin nyelv) (58-59. dia)
Absztrakt szövegek helyett példákkal írjuk le a működést:
*   **Given** (Adott egy állapot - pl. van 3 könyv a listában)
*   **When** (Történik valami - pl. rákeresek egy címre)
*   **Then** (Ez az elvárt eredmény - pl. csak 1 találat marad)

### Prototípusok (60-61. dia)
A prototípus segít a közös megértésben, de **nem termék**. Hiányzik belőle a hibakezelés, a biztonság és a skálázódás. Az LLM-ek (pl. ChatGPT) ma már órák alatt képesek eldobható prototípusokat generálni.

---

### Összefoglaló (63. dia)
A vizsgához tudd:
1.  A követelmény a **MIT/MIÉRT** és nem a HOGYAN.
2.  **FURPS+** és **INVEST** jelentése.
3.  **Traceability** (előre-hátra követés) haszna.
4.  A hiba javításának költséggörbéje az idő függvényében.
5.  A **Review** típusai (Inspection a legszigorúbb).