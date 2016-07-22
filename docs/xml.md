# Specifikace XML feedu ptolemaia

*tato specifikace není konečná a může se měnit, zaručujeme ale její zpětnou kompatilitu*

## Přidání položky do vyhledávání

povinné elementy jsou **id**, **title**, **url** a **price**

Minimalistická verze xml feedu:

```xml
<?xml version='1.0' encoding='utf-8'?>
<books>

  <book>
    <id>134382</id>
    <title>Lid a literatura ve středověku zvláště v románských zemích</title>
    <url>http://www.dantikvariat.cz/cerny-vaclav/lid-a-literatura-ve-stredoveku-zvlaste-v-romanskych-zemi-134382</url>
    <price>200</price>
  </book>

</books>
```

Plná verze xml feedu:

```xml
<?xml version='1.0' encoding='utf-8'?>
<books>

  <book>
    <id>134382</id>
    <title>Lid a literatura ve středověku zvláště v románských zemích</title>
    <url>http://www.dantikvariat.cz/cerny-vaclav/lid-a-literatura-ve-stredoveku-zvlaste-v romanskych-zemi-134382</url>
    <price>200</price>
    <author>Černý, Václav</author>
    <illustrator></illustrator>
    <publisher>Nakladatelství Československé akademie věd</publisher>
    <year>1958</year>
    <pages>344</pages>
    <description>pevná vazba s obálkou</description>
    <category>společenské vědy</category>
    <imgurl>http://www.dantikvariat.cz/nahled/obr/obr_134382.jpg</imgurl>
    <inserted>2016-01-01 11:55:00</inserted>
  </book>

</books>
```

## Specifikace jednotlivých elementů

|element|povinný|formát|v případě nesplnění formátu|v případě prázdného nebo nezadaného|
|---|---|---|---|---|
|[id](#id)|✔|int|ignorvání celého produktu|ignorvání celého produktu|
|[title](#title)|✔|string 255|Oříznutí na 255 znaků|ignorvání celého produktu|
|[url](#url)|✔|string 1024|ignorvání celého produktu|ignorvání celého produktu|
|[price](#price)|✔|float\int|ignorvání celého produktu|ignorvání celého produktu|
|[contributor](#contributor)| |Příjmení, Jméno|pokud obsahje více než jedno slovo, je poslední slovo posunuto na první pozici a je za něj přidána čárka|ignorování elementu|
|[publisher](#publisher)| |string|ignorování elementu|ignorování elementu|
|[year](#year)| |int|ignorování elementu|ignorování elementu|
|[pages](#pages)| |int|ignorování elementu|ignorování elementu|
|[imgurl](#imgurl)| |string 1024|ignorování elementu|ignorování elementu|
|[inserted](#inserted)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[ordered](#ordered)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[sold](#sold)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[deleted](#deleted)| |YYYY-MM-DD HH:MM:SS|ignorování elementu|ignorování elementu|
|[state](#state)| |string|ignorování elementu|ignorování elementu|
|[note](#note)| |text|ignorování elementu|ignorování elementu|
|[place](#place)| |string|ignorování elementu|ignorování elementu|
|[issue](#issue)| |string|ignorování elementu|ignorování elementu|
|[tag](#tag)| |string|ignorování elementu|ignorování elementu|
|[isbn](#isbn)| |string|ignorování elementu|ignorování elementu|


#### <a name='id'></a>id
#### <a name='title'></a>title
#### <a name='url'></a>url
#### <a name='price'></a>price
#### <a name='contributor'></a>contributor
#### <a name='publisher'></a>publisher
#### <a name='year'></a>year
#### <a name='pages'></a>pages
#### <a name='imgurl'></a>imgurl
#### <a name='inserted'></a>inserted
#### <a name='ordered'></a>ordered
#### <a name='sold'></a>sold
#### <a name='deleted'></a>deleted
#### <a name='state'></a>state
#### <a name='note'></a>note
#### <a name='place'></a>place
#### <a name='issue'></a>issue
#### <a name='tag'></a>tag
#### <a name='isbn'></a>isbn


aliasy názvů elementů:

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

## Odstranění produktu z vyhledávání

Produkt je možné z vyhledávání odebrat tak, že jej z xml feedu odstraníte. Doporučujeme, ale odeslat v xml záznam s elementem **ordered** (objednané položky), **sold** (prodané položky) nebo **deleted** (s časovím záznamem ve formátu YYYY-MM-DD HH:MM:SS) a **id** produktu, ostatní elementy již není potřeba do toho záznamu přidávat.

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

# Realtime XML feed

Realtime XMl feed je stejný jako klasický XML feed jen obsahuje aktualní data (přidání, úpravy, prodej, mazání) za poslední hodinu, narozdíl od klasického xml feedu je nutné pro smazání používat elementy ordered, sold, deleted.
