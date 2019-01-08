# 30\. - Vyhledávání

> Vyhledávání lineární a binární, datové struktury optimalizované pro vyhledávání a práce s nimi, binární vyhledávací strom, 2-3 strom, B strom, hashování.

## Lineární vyhledávání

Postupné sekvenční procházení prvků seznamu od začátku do konce, známe také jako **sekvenční vyhledávaní**.

- Složitost vyhledávání je **O(N)**.

  - Nejlepší je O(1), je-li prvek na první pozici.
  - Průměrně pak O(N/2).
  - Nejhorší O(N), je-li prvek na poslední pozici.

- Narozdíl od binárního vyhledávání lze použít na **neuspořádaný** (neseřazený) seznam.

- V některých případech jde o jediný možný způsob prohledávání (spojový seznam).

## Binární vyhledávání

Vyhledávací algoritmus na pricipu **půlení intervalu**.

- Složitost procházení je ![](https://latex.codecogs.com/gif.latex?O%28log_%7B2%7DN%29), tedy lepší (rychlejší) než u lineárního vyhledávání.
- Funguje pouze na **uspořádáném** (seřazeném) seznamu.
- Možný je rekurzivní i iterativní zápis. (iteratívní nevolá funkce a je nepatrně rychlejší)

**Princip:** (máme pole **p** a prvek **h**)

- Porovnáme prostřední prvek pole p s prvkem h.
- Pokud se rovnají vrátíme ho jako výsledek.
- V případě, že je h menší, musí se hledaný prvek v vyskytovat ve zbytku pole nalevo. (a naopak)
- Tento postup opakujeme (rekurzivně) na zbytkovém poli. (v kódu níže reprezentováno jako zarážky)
- Zbyde-li nám pouze dílčí pole s jedním prvkem a jeho hodnota neodpovídá h, hodnota h se v poli nevyskytuje.

```java
    /**
     * Binarni vyhledavani (rekurzivni zapis)
     * @param array prohledavane pole (setridene od nejvyssiho)
     * @param leftIndex prvni index, na ktery smime sahnout
     * @param rightIndex posledni index, na ktery smime sahnout
     * @param value hodnota k nalezeni
     * @return index hodnoty, -1 v pripade nenalezeni
     */
    public static int binarySearch(int[]  array, int leftIndex, int rightIndex, int value){
        if(leftIndex == rightIndex && array[leftIndex] != value) return -1;

        int middleIndex = leftIndex + (rightIndex - leftIndex)/2;
        if(array[middleIndex] == value) return middleIndex;
        else if(array[middleIndex] > value)
            return binarySearch(array, middleIndex + 1, rightIndex, value);
        else return binarySearch(array, leftIndex, Math.max(leftIndex, middleIndex - 1), value);
}
```

## Datové struktury optimalizované pro vyhledávání

### Binární vyhledávací strom (BST)

Datová struktura založená na binárním stromu, v němž jsou jednotlivé prvky (uzly) uspořádány tak, aby v tomto stromu bylo možné rychle vyhledávat danou hodnotu.

- Postaveno na principu binárního vyhledávání. (vyvážený BST strom má složitost vyhledávání ![](https://latex.codecogs.com/gif.latex?O%28log_%7B2%7DN%29))
- Jedná se o binární strom, každý uzel tedy má nanejvýš dva potomky − levého a pravého.
- Každému uzlu je přiřazen určitý klíč. Podle hodnot těchto klíčů jsou uzly uspořádány.
- Levý podstrom uzlu obsahuje pouze klíče menší než je klíč tohoto uzlu.
- Pravý podstrom uzlu obsahuje pouze klíče větší než je klíč tohoto uzlu.

![Binární vyhledávací strom](30_bst.png)

_Binární vyhledávací strom_

**Operace**

Operacemi vzniká problém s vyvážením, proto byl tvořen samovyvažovací strom (**AVL**), který tyto problémy řeší automaticky.

_Vyhledávání_

Vyhledání konkrétní hodnoty v binárním vyhledávacím stromu typicky probíhá rekurzivně. Začíná zpravidla v kořeni. V každém kroku porovná hledanou hodnotu s klíčem zkoumaného uzlu. Pokud jsou si rovny, hodnota byla nalezena. Je-li hledaná hodnota menší, pokračuje hledání v levém podstromu. Je-li větší, bude hledání pokračovat v pravém podstromu. Díky uspořádání stromu je cesta k hledané hodnotě jednoznačně určena.

_Přidání uzlu_

Vložení nového uzlu začíná hledáním jeho pozice ve stromu – postupuje se stejně jako při vyhledávání, jako hledaná hodnota se použije klíč vkládaného uzlu. Tato fáze může vést ke dvěma různým výsledkům:

- Klíč byl nalezen, strom tedy dotyčnou hodnotu již obsahuje a není třeba ji vkládat (komplikovanější varianty připouštějící vícenásobný výskyt stejného klíče by pokračovaly dál do podstromu připouštějícího rovnost).
- Algoritmus narazil na neexistující uzel, nový uzel bude vložen na toto místo, protože sem podle hodnoty svého klíče patří.

[YouTube](https://youtu.be/ygZMI2YIcvk?t=105)

_Odstranění uzlu_

Zde nastává několik případů ke zvážení.

- _Odstranění listu_: Odstranění uzlu bez potomků se jednoduše provede odstraněním uzlu ze stromu.
- _Odstranění uzlu s jedním potomkem_: Provede se nahrazením uzlu uzlem potomka.
- _Odstranění uzlu se dvěma potomky_: Nechť se odstraněný uzel nazývá N. Pak je hodnota uzlu N nahrazena nejbližší vyšší (nejlevější uzel pravého podstromu), nebo nižší hodnotou (nejpravější uzel levého podstromu). Takový uzel má nanejvýš jednoho potomka, lze jej tedy ze stromu vyjmout podle jednoho z předchozích pravidel.

![](bstrom1.png)
![](bstrom2.png)

_Procházení_

Průchod binárním vyhledávacím stromem nijak nevyužívá jeho speciální vlastnosti a odpovídá průchodu běžným stromem. Viz strom v otázce [29\. Abstraktní datové struktury](https://github.com/tomaskrizek/tul-szz-it-nv/blob/master/29_abstraktni_datove_typy/29_abstraktni_datove_typy.md).

### B strom

Druh stromu, který zavádí limity na maximální (konstantou n), i minimální (n/2) počet potomků vrcholu. B-strom je díky této vlastnosti vyvážený, operace přidání, vyjmutí i vyhledávání tedy probíhají v logaritmickém čase. Tato struktura je často používána v aplikacích, kdy není celá struktura uložena v paměti RAM, ale v nějaké sekundární paměti, jako je pevný disk (například databáze). Protože přístup do tohoto typu paměti je náročný na čas (hlavně vyhledání náhodné položky), snažíme se minimalizovat počet přístupů do této paměti.

**B+ Strom** - všechny hodnoty musí být v listech.

![B strom odebírání](30_b_strom.png)

_B strom_

- Všechny listy (tj.uzly které nemají žádné potomky) jsou na stejné úrovni (ve stejné hloubce).
- Všechny vnitřní uzly kromě kořene mají maximálně n a minimálně n/2 potomků.
- Kořen má nejvýše n potomků, spodní hranice není omezena.

Strom je vyvažován požadavkem, aby byly všechny listy na stejné úrovni. Tato hloubka pozvolna roste s tím, jak do stromu přidáváme další data, nebo klesá spolu s vymazáváním dat ze stromu.

### 2-3 strom

**2-3 strom** je druh stromu, který se označuje v počítačové terminologii jako **B-strom** obsahující pouze uzly s dvěma nebo třemi potomky. Všechny listy ve stejné hloubce, proto se 2‑3 strom řadí mezi vyvážené stromy.

![2-3 strom](30_23_strom.png)

Vnitřní uzly neobsahují uvnitř data, ale obsahují některé informace o tom, co je uloženo v jejich potomcích (podstromech).

- Všechny cesty od kořene k listům jsou stejně dlouhé.
- Data jsou zapsána v listech v poslední úrovni stromu.
- Listy jsou seřazeny podle klíče z leva (minimum) doprava (maximum).
- Jestliže vnitřní část uzlu obsahuje jeden klíč, uzel má dva potomky. Pokud vnitřní část uzlu má dva klíče, uzel má tři potomky. V případě listu uzel nemá žádné potomky.

**Operace**

2-3 stromy se využívají v datových strukturách, jako jsou seznamy nebo databáze, kde se pracuje se základními operacemi vyhledávání, vkládání a mazání prvků. Usnadňují tak daleko více práci s daty, než kdybychom měli data uspořádána libovolně v paměti (obtížné vyhledávání) nebo naopak uložená jako seznam v řadě za sebou (obtížné vkládání).

_Vyhledávání_

Při vyhledávání dat podle klíče začínáme u kořene stromu a postupujeme podle klíčových atributů shora dolů.

- Procházíme uzel se dvěma potomky:

  - Pokud hledaný klíč K je menší než klíčový atribut uzlu K1, hledáme dále v levém podstromu.
  - Jestliže hledaný klíč K je větší nebo roven K1, pak hledáme dál v pravém podstromu.

![2-3 strom 2 listy](30_23_strom_2.png)

- Procházíme uzel se třemi potomky:

  - Pokud hledaný klíč K je menší než klíčový atribut uzlu K1, hledáme dále v levém podstromu.
  - Jestliže je hledaný klíč K větší nebo roven K1 a zároveň pokud je ve vnitřní části uzlu klíčový atribut K2 větší než K pak hledáme v prostředním podstromu.
  - Pokud K je větší nebo rovno K2, hledáme dále v pravém podstromu.

![2-3 strom 3 listy](30_23_strom_3.png)

Tímto způsobem pokračujeme, až do poslední úrovně stromu, kde se nachází listy s daty.

_Přidání uzlu_

Při vkládání nové větve do 2-3 stromu je nutné vyhledat pozici, kam novou větev vložíme. Poté co je nalezena pozice, vložíme větev do příslušného rodiče r.

- Jestliže počet potomků rodiče r se rozšíří ze dvou na tři u 2-3 stromu můžeme daný prvek rovnou vložit.
- Pokud počet potomků r po vložení se zvýší ze tří na čtyři, r se rozdělí na dva uzly po dvou potomcích a tím se zvýší počet potomků předka r o jeden viz obrázek.

![2-3 strom vkládání](30_23_strom_vkladani.png)

[Video](https://www.youtube.com/watch?v=bhKixY-cZHE)

_Odstranění uzlu_

Nejprve je nutné vyhledat větev, kterou budeme odebírat. Poté se odebere větev z jejího rodiče r.

- Pokud se sníží počet potomků r ze tří na dva u 2-3 stromu provedou se jednoduché změny viz obrázek 11.
- Jestliže počet potomků r se sníží ze dvou na jeden

  - r se sloučí se svými dvěma sourozenci a vzniknou tak dvě větve, které si rozdělí potomky.
  - r převezme jednu větev z jednoho ze svých sourozenců, který leží vedle.
  - Pokud po odebrání r má dohromady se svým sourozencem jen tři potomky vezme si r jednu větev ze svého rodiče.

![2-3 strom odebírání](30_23_strom_odebirani.png)

### Hashovaní

Hashování se používá pro efektivní vyhledávání.
- adresu v paměti vypočteme z hledaného klíče

Hashování je vhodné použít, pokud |K|<<|U|

![](universum.PNG)

**Princip hashování (2 fáze):**
1. Výpočet hašovací funkce h(k) (h(k) vypočte adresu z hodnoty klíče)
2. Vyřešení kolizí

![](kolize.PNG)

**Definice:**

Hashovací funkce h(k) je zobrazení z množiny klíčů K do množiny adres A = \<amin, amax\>

**Ideální hashovací funkce:**
- výpočetně co nejjednodušší
- aproximuje náhodnou funkci
- využívá rovnoměrně adresní prostor
- generuje minimum kolizí

**Řešení kolizí**
- Adresy v hašovací tabulce obsahují lineární seznamy (v případě kolize se se prvek vloží na konec seznamu)
- Otevřeným hašovaním
    - Tabulka adres uložena do pole
    - V případě kolize prohledáváme určitou metodou prvky pole, dokud nenajdeme prázdnou pozici
    - Při vyhledávání postupujeme stejně - pokud nenajdeme volnou pozici znamená to, že prvek není indexován
    1. Lineární prohledávání
    
    ![](linear.PNG)
    ![](linear2.PNG)
    
    2. Dvojí hašování (používá se druhá hashovací funkce)
    
    ![](double.PNG)

Na tomto principu jsou postaveny různé datové typy nebo databázové indexi, které pracují na principu klíč hodnota. Například tedy **asociační tabulka**, **hashmap** nebo **hashtable**, tyto struktury mohou být indexovány libovolným datovým typem.

Vlastnosti:

- složitost prohledávání O(1).
- Je potřeba celý klíč.
- Nejsou možné intervalové dotazy.
- Nebezpečí kolize (dva klíče ukazují na stejná data)
