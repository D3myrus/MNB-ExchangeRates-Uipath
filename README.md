Rövid leírás
A folyamat az MNB SOAP szolgáltatásából lekéri az aktuális devizaárfolyamokat, kinyeri a választ, majd Excelbe írja a következő oszlopokkal:

Currency – devizakód (pl. EUR, USD, JPY)
Rate – az MNB által közölt árfolyam az eredeti egységben
(Fontos: nincs 1 egységre normalizálás; a JPY/KRW/IDR esetén az MNB által megadott unit szerint értendő.)
Date – árfolyam napja
Duplikátumok szűrése: Excel Remove Duplicates (Currency alapján).

Futtatás lépései
Nyisd meg a projektet UiPath Studio Community-ben (Main.xaml).
Futtasd (F5).
Kimeneti fájl: Output/MNB_ExchangeRates_<YYYY-MM-DD>.xlsx
Ha már létezik a célfájl, javasolt előtte törölni (a folyamatban If File Exists → Delete File lépés is beállítható).
Használt csomagok / aktivitások
UiPath.WebAPI.Activities – HTTP Request (SOAP)
UiPath.System.Activities – Assign, If, For Each, Build Data Table, Add Data Row, Try/Catch
UiPath.Excel.Activities – Excel Process Scope, Use Excel File, Write DataTable to Excel, Remove Duplicates
Megoldás röviden
HTTP Request (POST) → MNB SOAP endpoint
SOAP Envelope feldolgozás: TextContent → belső XML HtmlDecode → XDocument
<Rate> elemek → DataTable (Currency, Rate, Date)
Excel Process Scope → Write DataTable to Excel a Rates lapra
Remove Duplicates (Has headers ✓, oszlop: Currency)
Minta output
Lásd: sample_output/MNB_ExchangeRates_<YYYY-MM-DD>.xlsx# MNB-ExchangeRates-Uipath
