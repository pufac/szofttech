Ez a diasor a **szoftvermetrikákról** és az **adatelemzésről** szól. A szoftverfejlesztésben nem elég "érzésre" dolgozni; mérni kell a kód bonyolultságát, a folyamatok hatékonyságát és a csapat teljesítményét.

A vizsgán a legfontosabb részek a **ciklomatikus komplexitás számítása**, a **DORA metrikák** és a **Boxplot (dobozábra) értelmezése**.

---

# 1. Mi a metrika? (1–8. dia)

A metrika egy **objektíven mérhető, számszerű mennyiség**. Nem vélemény, hanem adat.

### Goodhart törvénye (6. dia) – !!! FONTOS !!!
*"Ha egy mérés eredményét választjuk célnak, akkor a mérés megszűnik jól mérni."*
*   **Példa:** Ha a főnök azt mondja, hogy a bónusz a **leírt kódsorok számától (LOC)** függ, a fejlesztők elkezdenek "szószájú" kódot írni, ami tele van felesleges sorokkal. A mérés megmarad, de a cél (a hatékonyság) elvész.

### Metrikák csoportosítása (7–8. dia):
1.  **Termék metrikák:** 
    *   *Üzleti:* Bevétel (MRR), aktív felhasználók (MAU).
    *   *Technikai:* Bonyolultság (CC), tesztlefedettség.
2.  **Szervezeti metrikák:**
    *   *Projekt:* Költségvetés (EVA), határidők.
    *   *Folyamat:* Kiadások gyakorisága, érettségi szint (CMMI).
    *   *Csapat:* Produktivitás, kiégési index.

---

# 2. Strukturális metrikák (9–19. dia)

Itt a kód belső szerkezetét mérjük a **Vezérlési folyam gráf (CFG)** alapján.

### Ciklomatikus Komplexitás (CC) (15–16. dia) – !!! VIZSGAPONT !!!
Thomas McCabe módszere a programmodulok bonyolultságának mérésére. Azt adja meg, hány **lineárisan független út** van a kódban.
*   **Képlet:** $M = E - N + 2$
    *   $E$: élek száma (nyilak).
    *   $N$: csomópontok száma (utasítások).
*   **Ökölszabály:** Minél alacsonyabb, annál jobb. A magas CC-jű kód nehezen tesztelhető és érthető.

### Egyéb metrikák (17. dia):
*   **Max nesting:** Milyen mélyen vannak egymásba ágyazva az `if`-ek és `loop`-ok.
*   **Comment to Code ratio:** Mennyi magyarázat van a kódhoz képest. (A túl kevés és a túl sok is baj lehet).

---

# 3. Kapcsolatok és Kódminőség (20–24. dia)

A modulok közötti viszonyt két fogalommal jellemezzük (21. dia):
1.  **Csatolás (Coupling):** Mennyire függnek egymástól a modulok. Cél: **ALACSONY**.
2.  **Kohézió (Cohesion):** Mennyire tartoznak össze a feladatok egy modulon belül. Cél: **MAGAS**.

### ISO 9126 szabvány (23. dia):
A szoftverminőség 6 fő oszlopa:
*   Funkcionalitás, Használhatóság, Megbízhatóság, Hatékonyság, Karbantarthatóság, Hordozhatóság.

---

# 4. Folyamatok és Szervezet mérése (25–34. dia)

Hogyan mérjük, hogy egy cég "profi"-e?

### Érettségi modellek (27–30. dia):
*   **CMMI:** 5 szintű modell. Az 1. szint a "kaotikus", az 5. szint az "optimalizáló" (ahol folyamatosan javítják a folyamatokat az adatok alapján).
*   **Automotive SPICE (ASPICE):** Kifejezetten az autóiparnak szánt folyamatmodell.

### DORA metrikák (32–34. dia) – !!! MODERNEK !!!
A Google DORA csapata azonosította azt a 4 metrikát, ami megkülönbözteti az elit csapatokat a gyengéktől:
1.  **Deployment Frequency:** Milyen gyakran élesítünk?
2.  **Lead Time for Changes:** Mennyi idő a commit-tól az élesítésig?
3.  **Time to Restore Service:** Mennyi idő alatt javítunk ki egy leállást?
4.  **Change Failure Rate:** Milyen gyakran rontunk el valamit élesítéskor?

---

# 5. Fejlesztői élmény (DevEx) és MI (36–38. dia)

A mérés tárgya itt a fejlesztő: mennyire tudja tartani a **"flow"** állapotot, mekkora a **kognitív terhelése** (mennyire bonyolult a környezet).
*   **MI hatása (35. dia):** A fejlesztők 90%-a használ MI-t (pl. Copilot). Ez 3-7% produktivitás-növekedést hoz, de 39% nem bízik az MI kódjában.

---

# 6. Statisztika és Vizualizáció (39–62. dia)

Ha sok adatunk van, tudnunk kell elemezni őket.

### Változók típusai (47–49. dia):
*   **Numerikus:** Számok (Aritmetikai műveletek végezhetők).
    *   *Folytonos:* Mérhető (pl. válaszidő: 3.42 ms).
    *   *Diszkrét:* Számolható (pl. a teremben ülők száma: 20 fő).
*   **Kategorikus:** Csoportok.
    *   *Nominális:* Csak név (pl. Nem: Férfi/Nő).
    *   *Ordinális:* Van sorrend (pl. Szállodai csillagok).

### Átlag vs. Medián (50, 61. dia):
*   **Medián:** A sorba rendezett adatok középső értéke.
*   **Miért jobb?** Mert **robusztus**. 
    *   *Példa:* Van 10 mérésünk, mind 3ms. De jön egy hibás mérés, ami 20.000ms. Az **átlag** elszáll (2000ms lesz), de a **medián** marad 3ms körül. A medián nem érzékeny a kiugró értékekre (outlierekre).

### Boxplot (Dobozábra) (53–57. dia) – !!! VIZSGAPONT !!!
Ez a diagram sűríti a legtöbb infót:
*   **A doboz közepe:** A **Medián**.
*   **A doboz alja és teteje:** Q1 (25%) és Q3 (75%). A kettő közötti rész az **IQR** (ahol az adatok fele van).
*   **A bajuszok:** A várható szórás széle.
*   **A pöttyök a bajuszon kívül:** Az **outlierek** (kiugró, gyanús értékek).

**Anscombe-kvartett (43. dia):** Négy adathalmaz, amiknek a statisztikai mutatói (átlag, szórás) tök ugyanazok, de ha lerajzoljuk őket, teljesen máshogy néznek ki. **Tanulság:** Mindig nézzük meg a grafikont is, ne csak a számokat!

---

### Összefoglaló a vizsgához:
1.  Tudd kiszámolni a **Ciklomatikus Komplexitást** ($E - N + 2$).
2.  Tudd a **DORA metrikák** 4 nevét.
3.  Értsd, miért **robusztusabb a medián**, mint az átlag.
4.  Tudd leolvasni egy **Boxplotról**, hol a medián, és mik a pöttyök (outlierek).

Sok sikert a vizsgához! Ha a CC számításról vagy a Boxplot határok kiszámításáról (1.5 * IQR) szeretnél gyakorló példát, írj!