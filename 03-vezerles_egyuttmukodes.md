Ez a diasor a szoftverfejlesztés egyik legkritikusabb részét, a **verziókezelést és a csapatmunkát** dolgozza fel. A vizsgán ezek az alapfogalmak és a különböző integrációs minták (mint a CI vagy a Trunk-based development) kiemelt fontosságúak.

---

# 1. Bevezetés és a probléma (1-5. dia)

A szoftverfejlesztés során ritkán dolgozik egy ember egyedül. Amint ketten vagy többen kezdenek el ugyanazon a kódbázison dolgozni, megjelenik a **kód integrációjának problémája**.
*   **A kihívás:** Ki melyik fájlt módosítja? Hogyan kerülnek össze a módosítások anélkül, hogy felülírnánk egymás munkáját? Mi van, ha két ember ugyanazt a sort írja át?

---

# 2. Verziókezelő rendszerek (VCS) alapjai (6-12. dia)

### Központosított (Centralized) vs. Elosztott (Distributed) (9-10. dia)
Ez egy alapvető vizsgakérdés. Két fő megközelítés létezik:

1.  **Központosított (pl. SVN, Perforce):**
    *   Van egy központi szerver, ott van a teljes történet.
    *   A fejlesztő gépén csak az aktuális verzió fájljai vannak meg.
    *   **Hátrány:** Ha nincs net, nem tudsz commitolni vagy előzményeket nézni. Az ütközések elkerülésére gyakran **zárolást (locking)** használnak (pesszimista stratégia: "lefoglalom a fájlt, amíg írom").

2.  **Elosztott (pl. Git, Mercurial):**
    *   Minden fejlesztő gépén ott van a **teljes tárhely (repository)**, az összes verzióval és metaadattal.
    *   A lokális munka villámgyors (nem kell hálózat).
    *   Nincs kitüntetett központi példány technikai értelemben, de a gyakorlatban kijelölnek egyet (pl. GitHub), amihez mindenki igazodik.
    *   **Optimista stratégia:** Mindenki dolgozik, és csak akkor kezeljük az ütközést, ha tényleg kialakul.

### Alapfogalmak (11. dia)
*   **Commit:** Egy összetartozó módosításcsomag metaadatokkal (ki, mikor, miért).
*   **Codeline:** Commitok rendezett sorozata.
*   **Branch (Ág):** Egy elágazás a fejlesztésben (pl. egy új funkción dolgozunk egy külön ágon).
*   **Trunk / Mainline / Master / Main:** A fő ág, amit a termék "hivatalos" állapotának tekintünk.
*   **Merge (Összefésülés):** Két ág módosításainak egyesítése.
*   **Conflict (Ütközés):**
    *   *Szöveges:* Két ember ugyanazt a sort módosította.
    *   *Szemantikai (Veszélyesebb!):* A kód szövege összefésülhető, de a program nem fog működni. *Példa: Én átnevezek egy függvényt az egyik fájlban, te pedig meghívod az eredeti néven egy másikban. A verziókezelő nem lát hibát, de a kód nem fog lefordulni.*

---

# 3. A Git működése (13-20. dia)

### Hogyan tárol a Git? (16. dia)
A legtöbb rendszer különbségeket (diff) tárol. A Git ezzel szemben **állapotképeket (snapshot)** ment el minden commitnál. Ha egy fájl nem változott, csak egy hivatkozást tárol az előző állapotra (nem másolja le feleslegesen).

### A helyi tárhely részei (17-18. dia)
A Gitben három területet különítünk el:
1.  **Working Directory (Munkakönyvtár):** A fájlok, amiket épp szerkesztesz.
2.  **Staging Area (Index / Érkeztető terület):** A "váróterem". Ide rakod be a fájlokat (`git add`), amiket a következő mentésbe (commit) be akarsz venni.
3.  **Local Repo (.git könyvtár):** Itt van a teljes helyi adatbázis.

**Fájl állapotok:** `Untracked` (új fájl) → `Staged` (hozzáadva) → `Unmodified` (elmentve) → `Modified` (megváltoztatva).

### Commit és Branch felépítése (19-20. dia)
*   Minden commit kap egy egyedi **SHA-1 hash** azonosítót (pl. `f30ab...`).
*   **HEAD:** Egy mutató, ami megmutatja, hogy éppen melyik commiton/ágon állsz.
*   A **Branch** valójában csak egy könnyűsúlyú, mozgatható mutató egy commitra.

---

# 4. Gyakorlati parancsok és tanácsok (21-27. dia)

### Legfontosabb parancsok (22-25. dia)
*   `git init`: Új tárhely létrehozása.
*   `git clone`: Távoli tárhely lemásolása.
*   `git status`: Hol állok, mi változott?
*   `git add`: Fájl betétele a Staging Area-ba.
*   `git commit -m "üzenet"`: Mentés a helyi tárhelybe.
*   `git log`: Előzmények megtekintése.
*   `git push`: Helyi commitok feltöltése a szerverre.
*   `git fetch / pull`: Változások lekérése a szerverről.

### Jó tanácsok (26. dia)
*   **Inkább sok kicsi commit, mint egy óriási.** Könnyebb visszakeresni a hibát.
*   **Jó commit üzenet:** Rövid összefoglaló (max 50 karakter), majd üres sor után részletes leírás. Ne legyen "fix", "bugfix", "valami" az üzenet.

---

# 5. Integrációs minták (Patterns) (28-37. dia)

Ez a rész a legfontosabb a szoftvertechnológia elméleti vizsgán!

### Alapminta: Mainline (29. dia)
Minden projektnek kell egy közös ág (**Single Source of Truth**), ahová a jóváhagyott kódok kerülnek.

### Integrációs minták:
1.  **Mainline Integration (31. dia):**
    *   A fejlesztők közvetlenül a fő ágra dolgoznak (vagy nagyon gyorsan oda integrálnak). Folyamatosan le kérik a többiek munkáját (pull), összefésülik a sajátjukkal, majd feltöltik (push).

2.  **Feature Branching (32. dia):**
    *   Minden új funkció saját ágat kap. Csak akkor kerül vissza a Mainline-ra, ha teljesen kész.
    *   *Előnye:* Nem rontjuk el a fő ágat félkész kóddal.
    *   *Hátránya:* Ha sokáig él az ág, a végén a **Merge fájdalmas lesz** (túl sok ütközés).

3.  **Continuous Integration (CI) (33. dia):**
    *   **Gyakori integráció:** Mindenki legalább naponta egyszer integrálja a munkáját a fő ágba. Így az ütközések kicsik maradnak és hamar kiderülnek.

### Kiadási (Release) minták (34-35. dia)
1.  **Release Branch:** Amikor közeledik a kiadás, leágaztatjuk a kódot. Ezen az ágon **már nincs új funkció**, csak hibajavítás és stabilizálás.
2.  **Release-Ready Mainline:** A fő ág mindig olyan jó állapotban van, hogy bármikor kiadható. Ehhez nagyon erős automatizált tesztelés kell.

### Munkafolyamatok (36-37. dia)
*   **GitHub Flow:** Feature ágak + **Pull Request**. A Pull Request a review (átnézés) és az integráció kombinációja.
*   **Trunk-based Development:** Nincsenek hosszú életű ágak. Mindenki a "trunk"-ra (fő ág) dolgozik, kis adagokban. Ez a modern DevOps alapja.

---

### Összefoglalás (40. dia)
A vizsgára tudd:
- Az elosztott és központosított közti különbséget.
- A Git három területét (Working dir, Staging, Repo).
- Miért jobb a gyakori integráció (CI), mint a ritka.
- Mi a különbség a szöveges és a szemantikai konfliktus között.

Ha van konkrét kérdésed egy parancsról vagy ábráról, szívesen kifejtem!