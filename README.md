# MNB Exchange Rates – UiPath projekt

## Rövid leírás
Ez a folyamat az MNB SOAP webszolgáltatásából lekéri az aktuális devizaárfolyamokat, feldolgozza a választ, és Excel fájlba menti az adatokat.

Az Excel tartalmazza:
- **Currency** – devizanem kódja (pl. EUR, USD, JPY)
- **Rate** – az MNB által közölt árfolyam az **eredeti egységben**
  *(pl. JPY 100 egységre vonatkozik, nincs 1 egységre normalizálás)*
- **Date** – az árfolyam napja

A folyamat az Excel „Remove Duplicates” funkcióját használja, hogy minden deviza csak egyszer szerepeljen.

---

## Futtatás lépései
1. Nyisd meg a projektet UiPath Studio Community-ben (`Main.xaml`).
2. Nyomj **Run (F5)**.
3. A kimeneti fájl automatikusan létrejön az `Output/` mappában:  
   `Output/MNB_ExchangeRates_<YYYY-MM-DD>.xlsx`.

---

## Használt csomagok / aktivitások
- **UiPath.WebAPI.Activities** – HTTP Request (SOAP hívás)
- **UiPath.System.Activities** – Assign, If, For Each, Build Data Table, Add Data Row, Try/Catch
- **UiPath.Excel.Activities** – Excel Process Scope, Use Excel File, Write DataTable to Excel, Remove Duplicates

---

## Megoldás röviden
- HTTP Request elküldi a SOAP kérést az MNB felé.  
- A választ `HtmlDecode` után XML-ként feldolgozzuk (`XDocument`).  
- Az összes `<Rate>` elemből egy DataTable épül (`Currency`, `Rate`, `Date`).  
- Az Excel Process Scope-ban a DataTable a `Rates` munkalapra íródik.  
- Ezután a Remove Duplicates biztosítja, hogy minden deviza csak egyszer szerepeljen.

---

## Minta output
A `sample_output/` mappában található egy futtatás eredménye:  
`MNB_ExchangeRates_<YYYY-MM-DD>.xlsx`
