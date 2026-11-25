# Standard Silver vrstvy – rozhodnutí Silver guildy

## Datový model

- Silver bude integrovaný relační model ve 3NF.
- Každá entita bude mít vlastní tabulku s ověřeným klíčem.
- Atributy budou záviset pouze na klíči.
- Číselníky budou uložené v samostatných tabulkách.

## Pojmenování

- Tabulky budou mít prefix `silver_`.
- Názvy budou malými písmeny a slova oddělená podtržítkem.

## Entity

- Interní agenda bude rozdělená podle entit, například na cestující, revizory, kontroly, pohledávky a platby.
- GTFS bude zahrnovat linky, dopravce, vazby linka–dopravce, zastávky, spoje a časy zastavení.
- Osobní údaje se v Silver pseudonymizují.

## Historie změn

- Linky a vazby linka–dopravce se historizují metodou SCD2 podle denních snímků.
- Stavy interních entit, například pohledávek a reklamací, se historizují metodou SCD2 porovnáním denních snímků z Bronze.
- U událostí se historizují změny textu.

## Časová pozorování

- **Polohy:** jeden řádek představuje vozidlo nebo spoj v konkrétním čase pozorování. Stejné vozidlo v jiném čase není duplicita.
- **Odjezdy:** granularita je spoj, provozní datum a pořadí zastávky. Plánovaný a skutečný odjezd se evidují odděleně.
- **Průjezdy:** jeden řádek na spoj a zastávku; opakované snímky nesmějí vytvářet duplicity. Predikovaný odjezd se nepovažuje za skutečný průjezd.
- **Události:** eviduje se začátek, konec, typ a dotčené linky a zastávky.

## Vazby mezi zdroji

- Zdroje se propojují pouze pomocí ověřených klíčů a mapovacích tabulek.
- Interní zastávky se mapují na GTFS; evidují se i nejednoznačné a nenalezené případy.

## Kvalita

- Tabulky mají správné datové typy, deduplikaci, sjednocené číselníky a časové zóny.
- Vadné záznamy se podle pravidel DQ ukládají do karantény.
- Vede se lineage od zdroje do Silver a metrika úplnosti sběru za den.

## Ověření modelu

- Na modelu se připraví ukázka, jak zodpovědět otázky DPP č. 5 a 11 pomocí čitelného SQL dotazu.
