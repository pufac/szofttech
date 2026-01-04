Ez a diasor az **Agilis fejlesztési módszerek** világába kalauzol el, ami a modern szoftverfejlesztés alapköve. A vizsgán kiemelten fontos a **Scrum** és a **Kanban** közötti különbségtétel, a szerepkörök és az alapelvek ismerete.

Íme a részletes feldolgozás:

---

# 1. Agilis alapelvek (1–4. dia)

Az agilitás nem egy konkrét recept, hanem egy **szemléletmód (mindset)**. Az Agilis Kiáltvány (Agile Manifesto) négy fő értéket határoz meg, ahol a bal oldali dolgokat többre értékeljük a jobb oldaliaknál:
1.  **Személyek és interakciók** > folyamatok és eszközök.
2.  **Működő szoftver** > átfogó dokumentáció.
3.  **Együttműködés az ügyféllel** > szerződéses alkudozás.
4.  **Válaszkészség a változásra** > terv követése.

*Példa:* Ha a fejlesztés közben rájövünk, hogy a gomb színe helyett a funkciója a rossz, nem a 200 oldalas tervet nézzük, hanem azonnal változtatunk, hogy az ügyfélnek értéket adjunk.

---

# 2. Lean Thinking – A "karcsú" gondolkodás (5–6. dia)

A Lean a pazarlásmentes gyártásból (Toyota) ered. 5 alapelve van:
*   **Value (Érték):** Csak azzal foglalkozzunk, ami a vevőnek tényleg fontos.
*   **Value Streams:** Azonosítsuk a lépéseket, amik az értéket előállítják, és vágjuk ki a felesleget (waste).
*   **Flow (Áramlás):** Akadálytalanul haladjon a munka (ne álljon a feladat hetekig jóváhagyásra várva).
*   **Pull (Húzás):** Just-In-Time – csak akkor fejlesszünk, ha igény van rá.
*   **Perfection (Tökéletesség):** Folyamatos apró javítások (**Kaizen**).

---

# 3. Kanban módszer (7–16. dia)

A Kanban a munka **vizualizációjára** és az áramlásra fókuszál.

### Fő elemei:
*   **Kanban tábla:** Oszlopok jelzik a munka fázisait (pl. Backlog, Doing, Testing, Done).
*   **WIP limit (Work In Progress):** Korlátozzuk, hány feladat lehet egyszerre egy oszlopban. Ez kényszeríti ki a csapatot a befejezésre ahelyett, hogy mindenbe belekapnának.
*   **Mérések (Flow):**
    *   **Lead time:** A feladat felmerülésétől a kész állapotig tartó idő.
    *   **Cycle time:** Amíg ténylegesen dolgoztunk rajta.

*Példa:* Ha a "Testing" oszlopban elértük a limitet, senki nem kezdhet új fejlesztésbe ("Doing"), amíg a tesztelők nem végeznek, vagy a fejlesztők nem segítenek nekik befejezni.

---

# 4. SCRUM keretrendszer (17–27. dia)

A Scrum egy kötöttebb, eseményalapú keretrendszer. 3 fő tartópillére: **Átláthatóság, Adaptáció, Megfigyelés**.

### Szerepkörök (19, 21-23. dia):
1.  **Product Owner (PO - Termékgazda):** Ő képviseli az üzletet. Meghatározza a prioritásokat (mit csináljunk), kezeli a Backlogot. Ő a "végső felelős".
2.  **Scrum Master (SM):** Nem főnök, hanem "szolga-vezető". Segíti a folyamatot, elhárítja az akadályokat, tanítja a csapatot.
3.  **Fejlesztői Csapat:** 6-9 fő, multidiszciplináris (mindenki ért valamihez, ami a szállításhoz kell).

### Események (25–27. dia):
*   **Sprint:** 1-4 hetes fix idejű fejlesztési ciklus.
*   **Sprint Planning:** Megtervezik, mi fér bele a következő Sprintbe.
*   **Daily Standup:** Napi 15 perces álló meeting (Mit csináltam? Mit fogok? Mi akadályoz?).
*   **Sprint Review:** Bemutató az érintetteknek a Sprint végén.
*   **Sprint Retrospective:** A csapat megbeszéli, hogyan tudnának jobban együttműködni.

---

# 5. Becslés és Prioritás (28–33. dia)

### Story Point (28. dia):
Nem órában becsülünk, hanem relatív **bonyolultságban**. Erre gyakran a **Fibonacci-sort** (1, 2, 3, 5, 8, 13, 20...) használják.
*   *Miért?* Mert egy 8-as és egy 13-as feladat közötti különbséget könnyebb érezni, mint 40 és 41 óra közöttit.

### INVEST – Mitől jó egy feladat (Backlog item)? (33. dia):
*   **I**ndependent: Független.
*   **N**egotiable: Megvitatható.
*   **V**aluable: Értéket ad.
*   **E**stimable: Becsülhető.
*   **S**mall: Kicsi.
*   **T**estable: Tesztelhető.

---

# 6. Készre jelentés: DoD (34–35. dia)

**Definition of Done (DoD - Kész definíciója):**
Egy ellenőrző lista, ami közös megállapodás a csapat és a PO között. Csak akkor "kész" valami, ha minden pont teljesül (pl. kód review megvolt, tesztek futnak, dokumentálva van). Ez védi meg a csapatot a "majdnem kész" állapot csapdájától.

---

# 7. Projekt indítás és Összegzés (36–49. dia)

**Agile Inception Deck (37. dia):** Segít a projekt elején tisztázni a célokat (pl. "Miért vagyunk itt?", "Elevator pitch" – 30 másodperces összefoglaló a termékről).

### Kanban vs. Scrum (40. dia):
*   **Kanban:** Folyamatos áramlás, állapotokra koncentrál, nincs fix időtartam (Sprint).
*   **Scrum:** Időalapú ciklusok (Sprotek), szigorú szerepkörök és események.
*   **Kombinálva (Scrumban):** Scrum események, de a feladatok Kanban táblán mozognak.

**Agilis metróhálózat (48–49. dia):** Ez az ábra azt mutatja, hogy az agilitás nem csak menedzsment, hanem rengeteg **mérnöki gyakorlat** (TDD – tesztvezérelt fejlesztés, CI – folytonos integráció, Refactoring) összessége.

---

### 🎓 Vizsgatippek:
*   **WIP limit jelentősége:** Megakadályozza a párhuzamos munkavégzésből adódó hatékonyságvesztést.
*   **PO vs SM:** A PO a "mit", az SM a "hogyan/folyamat" felelőse.
*   **Fibonacci becslés:** Miért jobb, mint az óra? (Mert a bizonytalanságot is tükrözi).
*   **DoD:** Miért kell? (Hogy ne maradjon technikai adósság a projekt végére).

Sok sikert a vizsgához! Ha bármelyik ceremónia (pl. Retrospektív) vagy fogalom (pl. Story Point matrix) mélyebb magyarázatot igényel, írj bátran!