# Obecné informace
Ptolemaia je schopná v zásadě z pracovat jakýkoliv XML feed (např. pro heureka.cz nebo zbozi.cz), ale velmi doporučujeme vytvořit feed podle následující specifikace. Ve vyhledávání se zobrazí více informací a zvýší se konverze (více zákazníků přijde na Váš web).
## Navigace
- [Specifikace XML feedu ptolemaia](#specifikace)
 - [Přidání položky do vyhledávání](#pridani)
 - [Specifikace jednotlivých elementů](#elementy)
 - [Aliasy názvů elementů](#aliasy)
 - [Odstranění produktu z vyhledávání](#odstraneni)
- [Realtime XML feed](#realtime)

# Specifikace XML feedu ptolemaia<a name="specifikace"></a>

*tato specifikace není konečná a může se měnit, ale ručíme za její zpětnou kompatilitu*

## <a name="pridani"></a>Přidání položky do vyhledávání

povinné elementy jsou **id**, **title**, **url** a **price**

Minimalistická verze xml feedu:

```xml
<?xml version='1.0' encoding='utf-8'?>
<books>

  <book>
    <id>12345</id>
    <title>Název knihy</title>
    <url>https://www.adresa.cz/kniha/nazev-knihy</url>
    <price>200</price>
  </book>

</books>
```

Plná verze xml feedu:

```xml
<?xml version='1.0' encoding='utf-8'?>
<books>

  <book>
    <id>12345</id>
    <title>Název knihy</title>
    <url>>https://www.adresa.cz/kniha/nazev-knihy</url>
    <price>200</price>
    <contributor>Příjmení, Jméno</contributor>
    <contributor>Příjmení, Jméno druheho autora, ilustrátora, překladatele a pod.</contributor>
    <contributor>...počet není omezen...</contributor>
    <publisher>Jméno nakladatelství</publisher>
    <year>1918</year>
    <pages>123</pages>
    <note>Bratři Strugačtí jsou dnes nejvýznamnější zástupci sovětské science fiction, uznávaní a vydávaní v celém světě. Za Piknik u cesty dostali švédskou cenu Julese Verna, za jinou knihu významnou sovětskou cenu Aelita, určenou pro nejlepší vědeckofantastická díla. Mnoho jejich knih vyšlo i česky. </note>
    <tag>společenské vědy</tag>
    <tag>filosofie </tag>
    <tag>...</tag>
    <imgurl>https://www.adresa.cz/images/12345.jpg</imgurl>
    <binding>pevná vazba s obálkou</binding>
    <state>Horší, natržená obálka</state>
    <place>Praha</place>
    <issue>1</issue>
    <isbn>80-7254-259-1</isbn>
    <inserted>2016-01-01 11:55:00</inserted>
  </book>

</books>
```

## <a name="elementy"></a>Specifikace jednotlivých elementů

|element|povinný|formát|v případě nesplnění formátu|v případě prázdného nebo nezadaného|
|---|---|---|---|---|
|[id](#id)|✔|int\string|ignorvání celého produktu|ignorvání celého produktu|
|[title](#title)|✔|string|ignorvání celého produktu|ignorvání celého produktu|
|[url](#url)|✔|string|ignorvání celého produktu|ignorvání celého produktu|
|[price](#price)|✔|float\int|ignorvání celého produktu|ignorvání celého produktu|
|[contributor](#contributor)| |Příjmení, Jméno|pokud obsahje více než jedno slovo, je poslední slovo posunuto na první pozici a je za něj přidána čárka|ignorování elementu|
|[publisher](#publisher)| |string|ignorování elementu|ignorování elementu|
|[year](#year)| |int|ignorování elementu|ignorování elementu|
|[pages](#pages)| |int|ignorování elementu|ignorování elementu|
|[imgurl](#imgurl)| |string|ignorování elementu|ignorování elementu|
|[inserted](#inserted)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[ordered](#ordered)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[sold](#sold)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[deleted](#deleted)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[state](#state)| |string|ignorování elementu|ignorování elementu|
|[binding](#binding)| |string|ignorování elementu|ignorování elementu|
|[note](#note)| |text|ignorování elementu|ignorování elementu|
|[place](#place)| |string|ignorování elementu|ignorování elementu|
|[issue](#issue)| |string|ignorování elementu|ignorování elementu|
|[tag](#tag)| |string|ignorování elementu|ignorování elementu|
|[isbn](#isbn)| |string|ignorování elementu|ignorování elementu|


#### <a name='id'></a>id
identifikator produktu
#### <a name='title'></a>title
název knihy
#### <a name='url'></a>url
adresa knihy na vašem eshopu
#### <a name='price'></a>price
cena knihy
#### <a name='contributor'></a>contributor
autor / ilustrátor, pokud jich je víc, tento element se opakuje
#### <a name='publisher'></a>publisher
vydavatel
#### <a name='year'></a>year
rok vydání
#### <a name='pages'></a>pages
počet stran
#### <a name='imgurl'></a>imgurl
obrázek, pokud jich je víc, tento element se opakuje
#### <a name='inserted'></a>inserted
datum vystavení
#### <a name='ordered'></a>ordered
datum objednání (zruší produkt z vyhledávání)
#### <a name='sold'></a>sold
datum prodání (zruší produkt z vyhledávání)
#### <a name='deleted'></a>deleted
datum smazání (zruší produkt z vyhledávání)
#### <a name='state'></a>state
stav knihy
#### <a name='binding'></a>binding
vazba knihy
#### <a name='note'></a>note
poznámka / popis
#### <a name='place'></a>place
místo vydání
#### <a name='issue'></a>issue
vydání
#### <a name='tag'></a>tag
tag / Kategorie. Pokud jich je víc, tento element se opakuje. Pokud se jedná o stromové kategorie, každá vrstva má samostatný element.
#### <a name='isbn'></a>isbn
ISBN/EAN prodkutu, pokud jich je víc, tento element se opakuje

## <a name="aliasy"></a>Aliasy názvů elementů

|element|aliasy|
|---|---|
|title|name; nazev|
|url|link; adresa|
|price|cena|
|contributor|autor; author; ilustrator; contributor|
|publisher|nakladetel|
|year|rok|
|pages|stran|
|imgurl|img; imglink; imghref; obrazek|
|inserted|start; vlozeno|
|sold|end; prodano|
|deleted|removed; smazano|
|state|condition; stav|
|note|poznamaka; popis; description|
|issue|vydani|
|place|misto|
|tag|category|
|isbn|ean|
|binding|vazba|

## <a name="odstraneni"></a>Odstranění produktu z vyhledávání

Produkt je možné z vyhledávání odebrat tak, že jej z xml feedu odstraníte. Ale z důvodu předcházení chybám doporučujeme odeslat v xml záznam s elementem **ordered** (objednané položky), **sold** (prodané položky) nebo **deleted** (s časovím záznamem ve formátu YYYY-MM-DD HH:MM:SS) a **id** produktu, ostatní elementy již není potřeba do toho záznamu přidávat.

```xml
<book>
  <id>134381</id>
  <ordered>2016-01-01 11:55:00</ordered>
</book>

<book>
  <id>134381</id>
  <sold>2016-01-01 11:55:00</sold>
</book>

<book>
  <id>134381</id>
  <deleted>2016-01-01 11:55:00</deleted>
</book>
```

# <a name="realtime"></a>Realtime XML feed

Realtime XMl feed je stejný jako klasický XML feed, ale obsahuje aktualní data (přidání, úpravy, prodej, mazání) za poslední hodinu. Narozdíl od klasického xml feedu je nutné pro smazání používat elementy ordered, sold, deleted. Tento feed feed není povinný, ale doporučujeme jej, aby se o nově přidaných knihách zákazníci dozvěděli co nejdříve.
