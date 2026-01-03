Ez a diasor az **UML struktúra modelleket**, azon belül a **komponens- és osztálymodellezést** tárgyalja. Ez a szoftvertechnológia „statikus” nézete: azt írjuk le, miből áll a rendszer, nem azt, hogy hogyan mozog.

A vizsgához ezeket a fogalmakat precízen kell tudni. Íme a részletes feldolgozás:

---

# 1. Strukturális modellezés célja (1–7. dia)

A szoftver bonyolult, ezért részekre kell bontanunk. Ezt hívjuk **dekompozíciónak** (vagy „faktoringnak”).

*   **Fizikai dekompozíció:** Milyen kézzelfogható alkatrészekből áll? (Pl. egy robotporszívónál: motor, szenzor, fedél).
*   **Logikai dekompozíció:** Milyen funkciókat lát el? (Pl. navigáló alrendszer, tisztító alrendszer).
*   **Szintek:** Az UML több szinten kínál elemeket: **Komponens** (legnagyobb egység), **Port/Interfész** (kapcsolódási pontok) és **Osztály** (belső finomszerkezet).

---

# 2. UML Komponens modellek (8–19. dia)

### Mi a komponens? (10. dia)
A komponens a rendszer egy önálló, egységbe zárt (encapsulated) része.
*   **Lecserélhető:** Ha egy komponens elromlik vagy fejleszteni kell, a környezete zavarása nélkül kicserélhető egy másikra, ami ugyanazt az interfészt tudja.
*   **Szerződés alapú:** Interfészeken keresztül kommunikál.

### Interfészek (12–13. dia) – *Kiemelt vizsgapont!*
A komponensek nem egymáshoz „drótozódnak”, hanem interfészekhez:
1.  **Biztosított interfész (Provided):** Amit a komponens nyújt másoknak. Jelölése: **„Nyalóka”** (kör a pálcikán).
2.  **Elvárt interfész (Required):** Amire a komponensnek szüksége van a működéshez. Jelölése: **„Foglalat”** (félkör).

### Portok és Összeköttetések (14–17. dia)
A **Port** a komponens nevesített kapcsolódási pontja. Ezen keresztül érkeznek a kérések.
*   **Assembly Connector (Összeállítási):** Két belső szerepet köt össze (nyalóka és foglalat találkozása). Ez a rendszer „összelegózása”.
*   **Delegation Connector (Delegációs):** A komponens külső portjára érkező kérést továbbítja egy belső elemnek. (Olyan, mint a recepción a portás: ő fogadja a levelet, de továbbadja az illetékes irodának).

---

# 3. UML Osztálymodellek (20–41. dia)

Az osztálydiagram a leggyakrabban használt UML eszköz. Nem csak kódot, hanem **fogalmi modelleket** is leírhatunk vele.

### Részletességi szintek (23. dia)
1.  **Fogalmi modell:** Brainstorming, csak a fő dobozok és nevek.
2.  **Analízis modell:** Megadjuk a felelősségeket, fontosabb adatokat, műveleteket.
3.  **Implementációs modell:** Nagyon részletes (láthatóság, típusok, getter/setterek). **Vigyázat:** Ezt gyakran felesleges megrajzolni, mert a kódban gyorsabb megírni!

### Osztály (Class) és Tulajdonság (Property) (24–26. dia)
*   **Osztály:** A valóság egy fogalma (pl. `Customer`). Mindig egyes számú főnév.
*   **Tulajdonság (Attribútum):** Az osztály állapotváltozója.
    *   **Szintaktika:** `[láthatóság] név : típus [multiplicitás] = alapérték {módosítók}`.
*   **Primitív típusok:** Integer, Boolean, String, Real. Ezek matematikai fogalmak, nincs bitméretük (pl. nem `int32`).

### Absztrakt osztály és Általánosítás (27–28. dia)
*   **Abstract:** Nem lehet példánya (pl. `Alakzat`). Jelölése: **Dőlt betű** vagy `{abstract}`.
*   **Generalization (Öröklődés):** „Is-a” kapcsolat. A gyerek megörökli a szülő minden tagját, de kibővítheti vagy felüldefiniálhatja (`redefinition`) azokat.

### Asszociáció (29–33. dia) – *Ahol a legtöbb hiba történik!*
Az asszociáció egy tartós kapcsolat példányok között (pl. a `Vevőnek` van `Rendelése`).
*   **ARANYSZABÁLY (30-31. dia):** Ha van asszociáció a két osztály között, **TILOS** külön attribútumként (pl. `orders: List`) is felvenni! Az asszociáció vonala már jelenti a tárolást.
*   **Asszociációs osztály:** Akkor kell, ha a kapcsolathoz is tartozik adat (pl. a `Személy` és a `Cég` közötti kapcsolat a `Munkaviszony`, aminek van `fizetés` adata).

---

# 4. Speciális elemek és Haladó fogalmak (35–45. dia)

### InstanceSpecification (Példányok) (35. dia)
Nem osztályokat, hanem konkrét példákat modellezünk (pl. „Kovács János” mint `Person`). Ez segít megérteni a bonyolult eseteket.

### Kényszer (Constraint) (39. dia)
Logikai szabályok, amiket a modellnek be kell tartania. Jelölése: **kapcsos zárójelben `{ }`**.
*   *Példa:* `{kor >= 18}` vagy a Stack osztályban a `{méret >= 0}`.

### DataType és Enumeration (40. dia)
*   **DataType:** Olyan típus, aminek nincs egyedi azonossága, csak az értéke számít (pl. egy `Cím` vagy `Dátum`). Ha két Dátum ugyanazt az évet/hónapot/napot mutatja, akkor azok „ugyanazok”.
*   **Enumeration:** Felsorolás (pl. `Láthatóság: public, private`).

### Aggregáció és Kompozíció (41. dia) – *Vizsgakedvenc!*
1.  **Aggregáció (Shared):** Gyenge rész-egész kapcsolat. A rész létezhet az egész nélkül is. (Pl. Tanterem és Szék). Jelölése: **üres rombusz**.
2.  **Kompozíció:** Erős kapcsolat. A rész élete az egésztől függ. Ha az egészet törlöm, a rész is megsemmisül. (Pl. Ablak és Gomb az ablakon). Jelölése: **tele rombusz**.

---

### 5. Viselkedés az osztályokban (46–50. dia)

*   **BehavioralFeature (Művelet):** Amire az osztály képes (Operation).
    *   **Metódus:** A művelet konkrét megvalósítása (a kód).
    *   **Láthatóság (52. dia):** `+` (public), `-` (private), `#` (protected), `~` (package).
*   **Signal (Jelzés) (48. dia):** Aszinkron üzenet (nem vár választ). Pl. „Tűzriadó!”

---

### Összefoglaló a vizsgához:
1.  **Interfész:** Tudd a provided (nyalóka) és required (foglalat) közti különbséget.
2.  **Connector:** Értsd a delegációs és assembly összekötők szerepét.
3.  **Asszociáció:** Soha ne írj „List” típusú attribútumot, ha be van húzva a vonal!
4.  **Kompozíció:** Tele rombusz = élet-halál közösség.
5.  **Kényszer:** `{ }` jelekkel adjuk meg a szabályokat.

Ha egy konkrét ábrát (pl. a 15. dián lévő belső felépítést) szeretnél részletesebben kielemezni, írj!