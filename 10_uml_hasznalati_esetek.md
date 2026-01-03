Ez a diasor az **UML használati esetek (Use Case)** témakörét járja körül. A szoftverfejlesztésben ez az eszköz segít áthidalni a szakadékot az ügyfél igényei és a technikai megvalósítás között. A vizsgán a legfontosabb rész a kapcsolatok (`«include»`, `«extend»`) pontos ismerete és a diagram szabályainak betartása.

Íme a részletes kidolgozás:

---

# 1. Mi az a Használati eset (Use Case)? (1-6. dia)

A használati esetek a **funkcionális követelmények** összegyűjtésére és dokumentálására szolgálnak.

*   **Definíció (6. dia):** A használati eset leírja a tipikus interakciókat a **rendszer** és annak **felhasználói** (aktorok) között. Egy narratívát (történetet) ad arról, hogyan használják a rendszert.
*   **Közös cél:** Egy use case több forgatókönyvet (szcenáriót) fog össze, amiknek **közös a felhasználói célja**.
    *   *Példa:* „Vásárlás”. A cél a termék megszerzése. Ebbe beletartozik a sikeres fizetés, de az is, ha elutasítják a kártyát (hibaág).
*   **Elnevezés:** Javasolt forma: **Ige + Főnév** (pl. *„Számla befizetése”*, *„Személyes adatok módosítása”*).
*   **Kívülről látható viselkedés:** Csak azt írjuk le, amit a felhasználó lát. A belső adatbázis-műveletek vagy algoritmusok nem részei a use case-nek.

---

# 2. Aktorok (Actor) (8, 11. dia)

Az aktor nem egy konkrét személy, hanem egy **szerepkör**, amit valaki (vagy valami) betölt a rendszerrel való kapcsolat során.

*   **Rendszerhatár:** Az aktor mindig a rendszeren **kívül** van.
*   **Típusai:**
    1.  **Elsődleges aktor:** Ő indítja el a folyamatot, ő akar elérni egy célt a rendszerrel (pl. *Ügyfél*). Tipikusan a diagram bal oldalán rajzoljuk.
    2.  **Másodlagos aktor:** A rendszernek van szüksége rá a folyamat közben (pl. *Banki hitelesítő rendszer*, *Email szerver*). Tipikusan a jobb oldalon rajzoljuk.
*   **Fontos szabály:** Egy személy több aktor is lehet (pl. délelőtt *Oktató*, délután *Hallgató* ugyanabban a rendszerben). Az aktor lehet egy másik szoftver vagy hardver eszköz is.

---

# 3. A használati esetek leírása (7, 9. dia)

A diagram csak egy "tartalomjegyzék". A valódi információ a **szöveges leírásban** van.

*   **Preconditions (Előfeltételek):** Minek kell teljesülnie, mielőtt elindulhat (pl. *„A felhasználó be van jelentkezve”*).
*   **Postconditions (Utófeltételek):** Mi változik meg a végére (pl. *„A pénz levonva, a rendelés rögzítve”*).
*   **Primary flow (Fő ág / Happy Path):** A leggyakoribb, hiba nélküli lefutás.
*   **Alternate flow (Alternatív ágak):** Variánsok vagy hibaágak (pl. *„Nincs elég fedezet a kártyán”*).

---

# 4. Kapcsolatok típusai (12-14. dia) – *Kiemelt vizsgatéma!*

Ez a rész a legkritikusabb a pontos modellezéshez.

### A. «include» (Beágyazás)
*   **Jelentése:** A forrás use case **mindenképpen** végrehajtja a cél use case-t.
*   **Célja:** Közös részek kiemelése (újrafelhasználás) vagy egy túl bonyolult folyamat szétbontása (dekompozíció).
*   **Nyíl iránya:** Az alap use case-től mutat a beágyazott felé.
    *   *Példa:* „Készpénzfelvétel” **«include»** „Azonosítás”. Nem tudsz pénzt felvenni azonosítás nélkül.

### B. «extend» (Kiterjesztés)
*   **Jelentése:** A kiterjesztő use case **csak bizonyos feltételek mellett** (opcionálisan) fut le. Az alap use case önmagában is értelmes és teljes.
*   **Célja:** Kivételes esetek, extrák leírása.
*   **Nyíl iránya:** A kiegészítő (extra) use case-től mutat az alap felé. **(Vigyázat, ez gyakran fordítva tűnik logikusnak, de a szabvány szerint így van!)**
    *   *Példa:* „Vásárlás” **«extend»** „Házhozszállítás kérése”. A vásárlás akkor is kész, ha nem kérsz szállítást.

### C. Generalization (Általánosítás)
*   **Jelentése:** "Is-a" (egyfajta) kapcsolat.
*   **Célja:** Speciális esetek kezelése.
    *   *Példa:* „Fizetés” az ős, „Fizetés kártyával” és „Fizetés készpénzzel” a leszármazottak.

### D. Association (diából másolva):
* „An association between an actor and a use case indicates that the actor and the use case somehow interact or communicate with each other.”

---

# 5. Szabályok és tiltások (15-16. dia)

A vizsgán pontlevonás jár, ha rossz helyre húzol vonalat:

| Kapcsolat | Aktor $\to$ Aktor | Aktor $\to$ Use Case | Use Case $\to$ Use Case |
| :--- | :---: | :---: | :---: |
| **Asszociáció** (sima vonal) | NEM | **IGEN** | NEM |
| **Generalization** (háromszög végű) | **IGEN** | NEM | **IGEN** |
| **«include» / «extend»** | NEM | NEM | **IGEN** |

*   **Tilos:** Két use case-t sima vonallal összekötni.
*   **Tilos:** Use case-t beletenni egy aktorba.
*   **Tilos:** «include» vagy «extend» kapcsolatot húzni aktor és use case közé.

---

# 6. Kidolgozott példa: SoftEng HF portál (18. dia)

Nézzük meg a leírás alapján, mik lehetnek a use case-ek:
1.  **Hallgató:** „Feladat megtekintése”, „Haladás követése”, „Azonosító regisztrálása”.
2.  **Oktató:** „Hallgatói állapot megtekintése”, „Ellenőrzés indítása manuálisan”.
3.  **Tárgyfelelős:** „Státusz felülírása” (ő egy speciális Oktató $\to$ Generalization).
4.  **Rendszerhatár:** Az ellenőrzést a „GitHub” és a „Sonar” végzi $\to$ ők **másodlagos aktorok**.

### Összefoglaló a vizsgához:
1.  Aktor = Szerepkör (Rendszerhatáron kívül).
2.  Use case = Felhasználói cél (Ige + Főnév).
3.  `«include»`: Kötelező részfeladat (Nyíl az alapból a részbe).
4.  `«extend»`: Opcionális/Hibaág (Nyíl a kiegészítésből az alapba).
5.  Diagram $\neq$ Modell (A diagram csak egy nézet).

Ha szeretnél egy konkrét feladatot (pl. a 18. dián lévőt) közösen lerajzolni szövegesen, jelezd!