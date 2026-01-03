Persze, ez egy gyakori probléma: az UML-ben rengeteg diagram van, és könnyű őket összekeverni. A vizsgán a legfontosabb, hogy tudd, **melyik diagramot mire használjuk** (mi a célja), és mi a **legfontosabb jelölése**.

Csoportosítsuk őket a két nagy UML főág szerint: **Struktúra** (mi van benne?) és **Viselkedés** (hogyan működik?).

---

### 1. A Rendszerhatár (A "külső" nézet)
#### **Use Case Diagram (Használati eset)**
*   **Mire jó?** A funkcionális követelmények összegyűjtésére. Mit akar a felhasználó elérni?
*   **Fő elemek:** Aktor (pálcikaember), Use Case (ovális), Rendszerhatár (téglalap).
*   **Példa:** A "Vásárló" (Aktor) "Terméket rendel" (Use Case).
*   **Kulcsszó:** *Felhasználói célok, Interakció a külvilággal.*

---

### 2. Struktúra diagramok (Statikus nézet – "Miből áll?")
#### **Class Diagram (Osztálydiagram)**
*   **Mire jó?** A rendszer belső szerkezetének, adatainak leírására. Ez a "kód váza".
*   **Fő elemek:** Osztályok (név, attribútumok, metódusok), Asszociáció (vonal), Öröklődés (üres háromszög), Kompozíció (tele rombusz).
*   **Példa:** Egy `Autó` osztálynak van `sebesség` adata és `gyorsít()` metódusa. Kapcsolódik hozzá egy `Motor`.
*   **Kulcsszó:** *Blueprint, Adatszerkezet, Típusok.*

#### **Component Diagram (Komponensdiagram)**
*   **Mire jó?** Magas szintű architektúra. Hogyan áll össze a rendszer nagy, cserélhető blokkokból?
*   **Fő elemek:** Komponens (téglalap kis ikonnal), Port, Interfész (nyalóka és foglalat).
*   **Példa:** Egy "Webshop" komponens és egy "Banki Fizetés" komponens összekapcsolódik egy interfészen keresztül.
*   **Kulcsszó:** *Architektúra, Modulok, Interfészek (API).*

---

### 3. Viselkedési diagramok (Dinamikus nézet – "Hogyan mozog?")
#### **Activity Diagram (Aktivitásdiagram)**
*   **Mire jó?** Folyamatok, algoritmusok leírása. Olyan, mint egy turbózott folyamatábra.
*   **Fő elemek:** Akció (lekerekített téglalap), Decision/Merge (üres rombusz), Fork/Join (vastag fekete vonal párhuzamosításhoz).
*   **Példa:** "Bejelentkezés" -> "Adatok ellenőrzése" -> [ha ok] "Belépés" / [ha nem] "Hibaüzenet".
*   **Kulcsszó:** *Munkamenet, Lépések sorrendje, Párhuzamosság.*

#### **State Machine Diagram (Állapotgép)**
*   **Mire jó?** Egyetlen objektum életútja. Hogyan reagál az eseményekre?
*   **Fő elemek:** Állapot (lekerekített téglalap), Átmenet (nyíl), Trigger/Esemény.
*   **Példa:** Egy lámpa állapota: `Felkapcsolva` --[gombnyomás]--> `Lekapcsolva`.
*   **Kulcsszó:** *Eseményvezérelt, Életciklus, Reaktív viselkedés.*

#### **Sequence Diagram (Szekvenciadiagram)**
*   **Mire jó?** Egy konkrét forgatókönyv (scenario) bemutatása. Ki kinek és mikor küld üzenetet?
*   **Fő elemek:** Életvonal (függőleges szaggatott vonal), Üzenet (vízszintes nyíl), alt/opt keretek.
*   **Példa:** A `Vezérlő` meghívja az `Adatbázis` `mentés()` függvényét, majd vár a válaszra.
*   **Kulcsszó:** *Időrendi sorrend, Objektumok közötti üzenetváltás.*

---

### 💡 Gyors "Puskázó" az összekeverhető dolgokhoz:

| Kérdés | Válasz / Diagram |
| :--- | :--- |
| **"Mit akar a júzer?"** | Use Case diagram |
| **"Milyen adattípusaim vannak?"** | Osztálydiagram |
| **"Milyen sorrendben jönnek a lépések?"** | Aktivitásdiagram |
| **"Várakozik a gép valamilyen gombnyomásra?"** | Állapotgép |
| **"Hogyan beszélget az A és a B objektum egymással?"** | Szekvenciadiagram |
| **"Hogyan kötöm össze a fizetési modult a webshoppal?"** | Komponensdiagram |

### Fontos vizsgás trükk: A "Rombusz" jelentése
*   **Osztálydiagramon:** Kapcsolat erőssége (Aggregáció/Kompozíció).
*   **Aktivitásdiagramon:** Választás vagy összevonás (Decision/Merge).
*   **Állapotgépen:** Ritkán használják, ott is választást jelenthet (Choice).

Ez az összefoglaló segít elhelyezni a fejedben a diagramokat. Melyik az, amelyiknél még mindig érzel bizonytalanságot a jelölésekben?