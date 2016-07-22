# specifikace XML feedu ptolemaia

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
|-|-|-|-|-|
|id|✔|int|ignorvání celého produktu|ignorvání celého produktu|
|title|✔|string 255|Oříznutí na 255 znaků|ignorvání celého produktu|
|url|✔|string 1024|ignorvání celého produktu|ignorvání celého produktu|
|price|✔|float\int|ignorvání celého produktu|ignorvání celého produktu|
|author||Příjmení, Jméno|pokud obsahje více než jedno slovo, je poslední slovo posunuto na první pozici a je za něj přidána čárka|ignorování elementu|
|illustrator||Příjmení, Jméno|pokud obsahje více než jedno slovo, je poslední slovo posunuto na první pozici a je za něj přidána čárka|ignorování elementu|
|publisher||string|ignorování elementu|ignorování elementu|
|year||int|ignorování elementu|ignorování elementu|
|pages||int|ignorování elementu|ignorování elementu|
|imgurl||string 1024|ignorování elementu|ignorování elementu|
|inserted||YYYY-MM-DD HH:MM:SS|ignorování element|ignorování element|
|ordered||YYYY-MM-DD HH:MM:SS|ignorování element|ignorování element|
|sold||YYYY-MM-DD HH:MM:SS|ignorování element|ignorování element|

aliasy názvů elementů:

|element|aliasy|
|-|-|
|title|name; nazev|
|url|link; adresa|
|price|cena|
|author|autor; contributor|
|illustrator|ilustrator; contributor|
|publisher|nakladetel|
|year|issue; rok|
|pages|stran|
|imgurl|img; imglink; imghref|
|inserted|start|
|sold|end|

## Odstranění produktu z vyhledávání

Produkt je možné z vyhledávání odebrat tak, že jej z xml feedu odstraníte. Doporučujeme, ale odeslat v xml záznam s elementem **ordered** (objednané položky) nebo **sold** (prodané položky) (s časovím záznamem ve formátu YYYY-MM-DD HH:MM:SS) a **id** produktu, ostatní elementy již není potřeba do toho záznamu přidávat.

```xml
<book>
  <id>134381</id>
  <ordered>2016-01-01 11:55:00</ordered>
</book>

<book>
  <id>134381</id>
  <sold>2016-01-01 11:55:00</sold>
</book>
```
