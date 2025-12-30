Ez a diasor a szoftvertechnológia egyik legfontosabb mérnöki területét, a **tervezést és az architektúrát** mutatja be. A cél itt nem csak a kód megírása, hanem a rendszer szerkezetének és alapvető döntéseinek a meghatározása.

Itt a részletes feldolgozás a vizsgára való felkészüléshez:

---

# 1. Mi a tervezés és az architektúra? (1-11. dia)

### Tervezés (Design) (5. dia)
A tervezés egy **folyamat**, aminek az eredménye a **terv**. 
*   **Célja:** Felmérni a lehetőségeket, és meghozni a fontos mérnöki döntéseket (pl. milyen adatbázist használjunk, hogyan épüljön fel a kezelőfelület).
*   **Fontos elem:** Nem csak a végeredményt kell leírni, hanem azt is, hogy **miért** úgy döntöttünk (tervezői döntések dokumentálása). Ez segít, ha később módosítani kell a rendszert.

### Szoftverarchitektúra (10. dia) – *Kiemelt vizsgapont!*
Az architektúra a rendszer legmagasabb szintű szerkezete. 
*   **Definíció:** "Azok a döntések, amiket bárcsak jól eltalálnál a projekt elején." (Hard to change - Nehéz később megváltoztatni).
*   **Szerepe:** Meghatározza a rendszer alapvető képességeit (úgynevezett **-ility** tulajdonságok):
    *   *Scalability* (skálázhatóság)
    *   *Reliability* (megbízhatóság)
    *   *Maintainability* (karbantarthatóság)
*   *Példa:* Ha monolitként indulsz el, és hirtelen 10 millió felhasználód lesz, az architektúra megváltoztatása (pl. mikroszolgáltatásokra bontás) hatalmas munka lesz.

---

# 2. Tervezési alapelvek (12-21. dia)

### A jó architektúra két fő célja (13. dia):
1.  **Komplexitás kezelése:** Hogy átlátható legyen a rendszer.
2.  **Változtathatóság:** Hogy könnyen lehessen új funkciókat hozzáadni.

### Három alapvető módszer (14. dia):
1.  **Absztrakció:** A lényeg kiemelése, a részletek elhagyása.
2.  **Dekompozíció/Modularizáció:** Részekre bontás.
3.  **Laza csatolás (Loose coupling):** Az elemek ne függjenek szorosan egymástól.

---

### Absztrakció (15-18. dia)
Az absztrakció során elhagyjuk a pillanatnyilag nem fontos részleteket. 
*   **Szintek (16-17. dia):** A gépi kódtól (részletes) haladunk a modellek felé (absztrakt). Ha két szint között nincs különbség, akkor az nem tervezés, csak átfordítás.
*   **GenAI és absztrakció (18. dia):** Az MI új típusú absztrakciót hoz be. Itt a "prompt" (utasítás) az absztrakció, ami nem-determinisztikus (ugyanarra az utasításra más kódot adhat). Ez kihívás a verziókezelésben és a reprodukálhatóságban.

---

### Modularizáció és Információrejtés (19-20. dia)
A rendszert modulokra (komponensekre, osztályokra) bontjuk.
*   **Információrejtés (Information Hiding):** Egy modul belseje titkos. Csak egy jól definiált **interfészen (API)** keresztül lehet vele beszélni.
*   *Példa:* Egy "Rendeléskezelő" modulnál mindegy, hogy SQL adatbázist vagy JSON fájlt használ belül (ez rejtve van). A lényeg az interfész: `addOrder()`, `cancelOrder()`. Ha belül kicseréljük az adatbázist, a többi modulnak semmit nem kell változnia.

---

### Csatolás (Coupling) és Kohézió (Cohesion) (21. dia) – *Klasszikus vizsgakérdés!*
*   **Csatolás (Coupling):** Mennyire függnek egymástól a modulok. Cél: **ALACSONY (Low coupling)**. Ha az egyiket módosítod, ne kelljen az összes többit is.
*   **Kohézió (Cohesion):** Egy modulon belül a feladatok mennyire tartoznak össze. Cél: **MAGAS (High cohesion)**. Egy modul csak egy dologgal foglalkozzon (pl. csak számlázás, ne számlázás + e-mail küldés + statisztika).

---

# 3. Architekturális stílusok és kihívások (22-33. dia)

### Kliens-Szerver architektúra (24. dia)
A legalapvetőbb felosztás:
*   **Kliens:** Megjelenítés (Web frontend, mobil app).
*   **Szerver:** Üzleti logika és adatok (Adatbázis, fájltár).

### Elosztott rendszerek kihívásai (25-27. dia)
Ha több gépünk van, az bonyolult.
*   **Skálázhatóság (Scalability):**
    *   **Scale Up (Felfelé):** Erősebb gép (több RAM/CPU). Van egy fizikai határa.
    *   **Scale Out (Oldalra):** Több gép. Szükség van egy **Terheléselosztóra (Load Balancer)**, ami szétosztja a kéréseket a gépek között.
*   **Hibatűrés (Fault Tolerance) (28-29. dia):** Mi van, ha leég az egyik szerver? 
    *   Megoldás: **Replikáció**. Az adatokat több példányban tároljuk (elsődleges és másodlagos adatbázis).

---

### Monolit vs. Mikroszolgáltatás (30-32. dia)
*   **Monolit:** Egyetlen óriási program. Egyszerűbb fejleszteni az elején, de nehéz skálázni és karbantartani.
*   **Microservice:** Sok kicsi, független szolgáltatás. Ha a "Fizetés" modul elromlik, a "Termékkereső" még működhet. Nagyon komplex az üzemeltetése (kell Load Balancer, Cache, API Gateway - lásd 32. dia).

---

# 4. Részletes tervek és elvek (34-38. dia)

Amikor már osztályok szintjén tervezünk, jönnek a szoftveres "szentírások":

### SOLID elvek (36. dia) – *Minden vizsgán előkerül!*
1.  **S (Single Responsibility):** Egy osztálynak csak egy feladata legyen.
2.  **O (Open/Closed):** Legyen nyitott a kiterjesztésre, de zárt a módosításra.
3.  **L (Liskov Substitution):** Az alosztályok legyenek behelyettesíthetők az ősosztályok helyére.
4.  **I (Interface Segregation):** Inkább több specifikus interfész, mint egy óriási általános.
5.  **D (Dependency Inversion):** Absztrakcióktól függjünk, ne konkrét megvalósításoktól.

### Tervezési minták (Design Patterns) (37. dia)
Gyakori problémákra adott kész megoldási receptek.
*   *Példa:* **Factory Method**. Ha nem akarjuk az objektum létrehozását "beégetni" a kódba, egy külön metódust bízunk meg vele, amit a leszármazottak felülírhatnak.

---

# Összefoglaló a vizsgához:
*   **Tervezés vs Architektúra:** A tervezés folyamat, az architektúra a legfontosabb, nehezen változtatható alapdöntések halmaza.
*   **Célok:** Alacsony csatolás, magas kohézió, jó skálázhatóság.
*   **Skálázás:** Scale Up (erősebb gép) vs Scale Out (több gép + load balancer).
*   **Információrejtés:** Az API legyen stabil, a belső logika változhasson.
*   **SOLID:** Tudd feloldani a mozaikszót és röviden elmagyarázni az elveket.

Sok sikert a felkészüléshez! Ha valamelyik SOLID elv vagy a Load Balancer működése nem tiszta, írj és hozok rá életszerű példát!