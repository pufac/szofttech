Ez a diasor a **Teszttervezési technikákról** szól, ami a szoftvertesztelés egyik legfontosabb mérnöki része. Nem elég "nyomkodni" a szoftvert; tudatosan kell kiválasztani azt a néhány tesztesetet, amivel a legtöbb hibát találhatjuk meg.

Íme a részletes, vizsgaközpontú feldolgozás:

---

### 1. Bevezetés és Motiváció (1–5. dia)

**Miért tervezünk teszteket? (5. dia)**
Boris Beizer híres idézete szerint: *"A tesztek tervezése az egyik legjobb hiba-megelőző módszer."*
*   **A lényeg:** Amikor leülsz megtervezni a tesztet, rájössz, hogy a követelmény nem egyértelmű. Ha végiggondolod, hogyan fogod ellenőrizni a funkciót, még a kód megírása előtt kiderülhetnek a logikai hiányosságok. Ez sokkal olcsóbb, mint a kész kódban bugokat keresni.

---

### 2. Alapfogalmak és Metrikák (6–10. dia)

**Ismétlés (6. dia):**
*   **SUT (System Under Test):** Amit tesztelünk.
*   **Test Case (Teszteset):** Bemenet + elvárt eredmény.
*   **Oracle (Orákulum):** Ami alapján eldöntjük, hogy a kapott kimenet jó-e (pl. a specifikáció).

**A két fő irány (7. dia):**
1.  **Specifikáció alapú (Black Box):** Nem látjuk a kódot. Csak azt nézzük, mit kellene csinálnia a leírás alapján.
2.  **Struktúra alapú (White Box):** Látjuk a kódot (függvényeket, elágazásokat), és a cél, hogy minden soron "átmenjen" a teszt.

**Lefedettségi metrikák (8–9. dia):**
*   Azt mérik, hogy a tesztelhető elemek hány százalékát fedtük le.
*   **FONTOS VIZSGAPONT:** A lefedettség **nem egyenlő a hibafedéssel**. Ha 100%-os az utasításlefedettséged, az nem jelenti azt, hogy 100%-ban megtaláltad a hibákat! Csak azt jelenti, hogy minden sor lefutott egyszer.

---

### 3. Specifikáció alapú (Black Box) technikák (11–24. dia)

Itt a cél a "mit teszteljünk?" kérdés megválaszolása a kód ismerete nélkül.

#### A. Ekvivalencia-particionálás (13–17. dia)
*   **Elv:** A bemeneti adatokat osztályokba soroljuk. Feltételezzük, hogy egy osztályon belül minden adat ugyanúgy viselkedik (ha egy elbukik, a többi is).
*   **Példa (15. dia):** Csomag súlya.
    *   I1: Érvénytelen (≤ 0 kg)
    *   V1: XS kategória (0 < x < 5 kg)
    *   V2: S kategória (5 ≤ x < 10 kg)
    *   **Teszteset:** Elég minden osztályból **egyet** választani (pl. -1, 3, 7). Nem kell az összes súlyt kipróbálni.

#### B. Határérték-analízis (18–21. dia)
*   **Elv:** A hibák legtöbbször a tartományok szélein (határainál) vannak (pl. `<` helyett `<=` írt a fejlesztő).
*   **Szabály (20. dia):** Egy határnál 3 értéket érdemes nézni: magát a határt, egyet alatta, egyet felette.
*   **Példa (21. dia):** Ha 5 sikertelen kérésnél jön az email:
    *   Tesztelni kell: 4 (még nincs email), 5 (pont jön az email), 6 (már jött email).

#### C. Használati eset (Use Case) tesztelés (22–24. dia)
*   Egy teljes üzleti folyamatot tesztelünk (pl. vásárlás folyamata).
*   **Fő ág (Happy path):** Minden simán megy.
*   **Alternatív ágak:** Mi van, ha nincs fedezet a kártyán? Mi van, ha elfogyott a könyv?

---

### 4. Struktúra alapú (White Box) technikák (25–38. dia)

Itt a forráskódot elemezzük a **CFG (Vezérlésifolyam-gráf)** segítségével.

**Alapfogalmak (28–29. dia):**
*   **Utasítás:** Egy parancs.
*   **Döntés (Decision):** Az elágazás (IF, SWITCH).
*   **Ág (Branch):** A döntés kimenete (pl. az IF igaz vagy hamis ága).

#### 1. Utasítás-lefedettség (Statement Coverage) (30–31. dia)
*   **Cél:** A kód minden sora fusson le legalább egyszer.
*   **Hiba:** Nem veszi észre a hiányzó ágakat. Ha nincs `else` ág, és egy változó nincs inicializálva, az utasítás-lefedettség 100% lehet, miközben a program bizonyos esetekben elszáll.

#### 2. Döntési lefedettség (Decision/Branch Coverage) (32–33. dia)
*   **Cél:** Minden elágazás minden lehetséges kimenetét (igaz és hamis) ki kell próbálni.
*   **Erősebb, mint az utasítás-lefedettség.** Ha ez 100%, akkor az utasítás-lefedettség is 100%.

**Példa feladat (35. dia):** `pow(n, k)` függvény.
*   A CFG-t felrajzolva látjuk, hogy kell egy teszt, ahol a feltétel `true` (negatív számok), és egy, ahol `false` (normál működés). Kell teszt a ciklusra is (0-szor fut le, 1-szer fut le, többször fut le).

---

### 5. Gyakorlati megvalósítás (36–42. dia)

**Hogyan mérjük? (36. dia):**
Az eszközök **instrumentálják** a kódot: apró "számlálókat" szúrnak be minden sorba, és a futás végén megnézik, melyik számláló nem nulla.

**Mire jó a lefedettség? (37–41. dia)**
*   **Jó:** Megmutatja, mi az, amit **egyáltalán nem** teszteltünk. Segít a tesztkészlet bővítésében.
*   **Rossz:** Ha 100%, az sem garancia a minőségre. A Microsoft tapasztalata (38. dia) szerint a lefedettség önmagában kevés, kell hozzá a jó minőségű **assertion** (ellenőrzés) is.

**Összegzés (42. dia):**
A leghatékonyabb a technikák **kombinációja**.
*   Specifikáció alapú: 83% lefedettség.
*   Felderítő teszt: +3% javulás.
*   Struktúra alapú (fehér doboz): +5% javulás.
*   **Összesen: 91%.**

---

### 🎓 Vizsgatippek:
1.  **Számolás:** Készülj fel, hogy egy rövid kódrészlethez (mint a 35. dián) ki kell számolnod, hány teszteset kell a 100% utasítás- vagy döntési lefedettséghez.
2.  **Definíció:** Mi a különbség a határ és az ekvivalencia osztály között? (Osztály: tartomány közepe; Határ: a szélei).
3.  **Kérdés:** Ha 100% a döntési lefedettségem, találtam-e minden hibát? **Válasz: NEM.** (A specifikációból hiányzó funkciókat vagy a logikai hibákat nem mutatja ki).