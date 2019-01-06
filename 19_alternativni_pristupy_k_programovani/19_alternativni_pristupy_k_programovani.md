# 19. - Alternativní přístupy k programování
>Alternativní přístupy k programování – funkcionální programování a Lambda kalkulus, náhrada cyklu rekurzí, logické programování, rezoluční mechanismus a jazyk Prolog.

Hlavní dva přístupy k programování jsou:

- **Imperativní** 
  - Imperativní programování je jedno z programovacích paradigmat, neboli způsobů, jak jsou v programovacím jazyku formulována řešení problémů. Imperativní programování popisuje výpočet pomocí posloupnosti příkazů a určuje přesný postup (algoritmus), jak danou úlohu řešit. Program je sadou proměnných, jež v závislosti na vyhodnocení podmínek mění pomocí příkazů svůj stav. Základní metodou imperativního programování je procedurální programování, tyto termíny bývají proto často zaměňovány.
  - V přímém kontrastu s imperativním programováním je deklarativní programování, jež je založeno na popisu cíle – přesný algoritmus provedení specifikuje až interpret příslušného jazyka a programátor se jím nezabývá. Díky tomu lze ušetřit mnoho chyb vznikajících zejména tím, že do jedné globální proměnné zapisuje najednou mnoho funkcí a metod. V deklarativním programování se totiž většinou místo proměnných používají k předání hodnot návratové hodnoty funkcí.
  - Na druhou stranu programátorovi při imperativním přístupu zůstává možnost program široce a přesně optimalizovat takovým způsobem, jaký právě potřebuje. Při přístupu deklarativním musí spoléhat na překladač, jež nemusí zvolit algoritmus, který by byl v dané chvíli výhodnější. Navíc při deklarativním přístupu je velmi často využíváno rekurze, což klade vyšší nároky na programátora. Ten si totiž musí představit, jak celý program bude fungovat, místo toho, aby viděl, jako u přístupu imperativního, přesně zapsaný algoritmus před sebou.
  - Typy příkazů: Přiřazení, cykly, větvění (podmínky)
  - [Wikipedia](https://cs.wikipedia.org/wiki/Imperativn%C3%AD_programov%C3%A1n%C3%AD)
- **Deklarativní** 
  - Deklarativní programování je založeno na myšlence programování aplikací pomocí definic co se má udělat a ne jak se to má udělat. Opakem tohoto principu je imperativní programování popisující jednotlivé úkony pomocí algoritmů. Zjednodušeně to lze popsat tak, že imperativní programy obsahují algoritmy, kterými se dosáhne chtěný cíl, zatímco deklarativní jazyky specifikují cíl a algoritmizace je ponechána programu (interpretu) daného jazyka
  - Deklarativní programování se snaží programátora ušetřit vytváření chyb, které běžně vznikají při tvorbě v imperativních jazycích. V imperativních jazycích je běžné mít proměnné globálního charakteru, do kterých zapisují ostatní funkce a metody. Toto je zdrojem mnoha chyb. Deklarativní jazyky se tento problém snaží řešit. Proměnné jsou v nich používány velmi střídmě, protože hodnoty se nejčastěji předávají ve formě návratové hodnoty určité funkce. Deklarativní jazyky také neobsahují prostředky, jak provést cyklus známý jako do-while nebo for. Vše je řešeno pomocí rekurze.
  - [Wikipedia](https://cs.wikipedia.org/wiki/Deklarativn%C3%AD_programov%C3%A1n%C3%AD)
  

Vyšší programovací jazyky se dále dělí takto:

- **Procedurální (imperativní)**
  - Strukturované (např. C)
  - Objektově orientované (např. Java)
- **Neprocedurální (deklarativní)**
  - Funkcionální (např. Lisp (Scheme) )
  - Logické (např. Prolog)

Toto rozdělení není absolutní a moderní  programovací jazyky jsou obvykle **multiparadigmatické**. To znamená, že různá paradigmata nějakým způsobem podporují a kombinují. Například Python podporuje *procedurální*, *objektově orientované* i *funkcionální* paradigma.

[Wikipedia](https://cs.wikipedia.org/wiki/Programovac%C3%AD_jazyk)

## Funcionální programování

- funkcionální paradigma patří mezi deklarativní programovací principy
- postaveno na formálním výpočtovém modelu nazvané λ-kalkul, kde jsou všechny konstrukce funkcemi
- funkce jsou objektem první třídy, mohou být předávány jako parametry jiným funkcím (tzv. funkcím vyšších řádů) nebo naopak vraceny jinými funkcemi jako výsledky
- obvykle se vyhýbá změnám stavů a proměnlivým datům, fuknce pracuje pouze se svým vstupem a vrací výstup
- funkce nemění stav kolem sebe, dobře se testuje
- změn stavu realizována jako vytvoření nového stavu (zachován původní)
- pro opakování/cykly se používá rekurze
- výpočtem funkcionálního programu je posloupnost vzájemně ekvivalentních výrazů, které se postupně zjednodušují 
- výsledkem výpočtu je výraz v normální formě, tedy dále nezjednodušitelný
- program je chápán jako jedna funkce obsahující vstupní parametry mající jediný výstup, tato funkce pak může být dále rozložitelná na podfunkce

### Scheme
- jeden ze dvou hlavních dialektů funkcionálního programovacího jazyka Lisp.
- deklarativní multiparadigmatický jazyk, převládá funcionální přístup
- vše je definováno jako seznam (mnoho závorek)
 - **promenná:** (define var1 value)  
 - **funkce:** (define x2 (lambda (x) (* x x)))
 - **seznam:** (list 1 2 3)

**Příklad** (nalezení nejmenšího prvku v seznamu)

Pro seznam máme dvě základní procedury:

- **(car seznam)** vydá první prvek seznamu - (**head**)
- **(cdr seznam)** vydá zbytek seznamu (bez 1. prvku) - (**tail**)

```scheme
(define (minim lst)
    (cond ((null? (cdr lst)) (car lst))
          ((< (car lst) (minim (cdr lst))) (car lst))
          (else (minim (cdr lst)))) )

(minim '(3 4 2 9 3 8)) 
```

### Lambda kalkul
Lambda kalkulus je formální systém pro deklaraci funkcí s pravidly pro jejich vyhodnocování. Lambda kalkulus lze chápat jako jednoduchý, univerzální, netypovaný a striktně formální programovací jazyk. Je výpočetně ekvivalentní s Turingovým strojem. Základní stavební jednotkou lambda kalkulu je tzv. lambda výraz. Množinu lambda výrazů lze chápat jako soubor pravidel pro výpočet.

Formálně lze každý lambda výraz vyjádřit takto:

```
<expression> := <name> | <function> | <application> 
<function> := ( λ <name> . <expression> )
<application> := ( <expression> <expression> )
```

Funkce s více parametry sice v lambda kalkulu neexistují, ale každou takovou funkci lze převést na funkci s parametrem jedním tak, že vnější funkce vrací vnitřní funkci, které předá parametr. Tento převodní proces se nazývá Currying.

Příklad:
```
(λx.x*x) 5 = 5*5
(λx.x*x)(λy.y+3) = (λy.(y+3)*(y+3))
(λx.x*x)(λy.y+3) 5  = 8*8 = 64
```

### Náhrada cyklu rekurzí
Každý algoritmus využívající rekurzi lze přepsat do nerekurzivního tvaru struktury a naopak.

Start with this code.
```
unsigned foo (...)
{
  ...

  unsigned a = f();
  unsigned b = g();

  ...

  while (a != b)
  {
    if (a > b)
    {
      a -= b;
    }
    else if (b > a)
    {
      b -= a;
    }
  }

  unsigned c = a;

  ...
}
```
  
This code has a pretty horrible loop: fortunately, we know what it does:
```
unsigned foo (...)
{
  ...

  unsigned a = f();
  unsigned b = g();

  ...

  unsigned c = greatest_common_divisor(a, b);

  ...
}

unsigned greatest_common_divisor (unsigned a, unsigned b)
{
  while (a != b)
  {
    if (a > b)
    {
      a -= b;
    }
    else if (b > a)
    {
      b -= a;
    }
  }
  return a;
}
```

Now that I've extracted the loop (which may, itself, be a sufficient refactoring), I can change it to a recursive form:
```
unsigned greatest_common_divisor (unsigned a, unsigned b)
{
  if (a != b)
  {
    if (a > b)
    {
      a -= b;
    }
    else if (b > a)
    {
      b -= a;
    }
    return greatest_common_divisor(a, b);
  }
  else
  {
    return a;
  }
}
```

This form isn't much better yet. There are 2 further simplifications: we fir st avoid modifying the parameters,
```
unsigned greatest_common_divisor (const unsigned a, const unsigned b)
{
  if (a != b)
  {
    if (a > b)
    {
      return greatest_common_divisor(a-b, b);
    }
    else if (b > a)
    {
      return greatest_common_divisor(a, b-a);
    }
   }
  else
  {
    return a;
  }
}
```

and, finally, we simplify the conditionals:
```
unsigned greatest_common_divisor (const unsigned a, const unsigned b)
{
  if (a > b)
  {
    return greatest_common_divisor(a-b, b);
  }
  else if (b > a)
  {
    return greatest_common_divisor(a, b-a);
  }
  else // a == b
  {
    return a;
  }
}
```

## Logické programování

- aplikace matematické logiky v programování
- interpretem je rezoluční stroj, který z faktů a pravidel odvozuje/ověřuje další fakta
- především deklarativní přístup (popis logických vztahů), procedurální složka potlačena

### Prolog

- využivá se v oboru umělé inteligence a počítačové lingvistiky
- 2 režimy :
  - **konzultační** (zadávají se fakta a pravidla)
  - **dotazovací** (kladou se otázky)
- základní částí:
  - definice faktů o objektech a vztazích mezi nimi
  - definice pravidel pro odvozování dalších faktů
  - kladení otázek
- program rozdělen na termy (term je buď atom, číslo, proměnná, nebo složený term)
  - atom => ‘nazdar’
  -  číslo => 23
  - proměnná => X
  - složený term => prarodic(X, Y):- rodic(X, Z), rodic(Z, Y).

**Příklad**

```prolog
rodic(jana,petr).
rodic(emil,petr).
rodic(ivana,jana).
rodic(alfons,jana).
rodic(otylie,emil).
prarodic(X,Y) :- rodic(X,Z), rodic(Z,Y).
?- prarodic(ivana,petr). %Yes
?- prarodic(otylie,emil). %No
?- prarodic(X,petr). X=ivana; X=alfons; X=otylie; %No
```

### Rezoluční mechanismus v prologu (jediné co jsem našel a moc tomu nerozumím)
Způsob vyhdonocování na základě predikátů => tvorba derivačního stromu.

Ve zjednodušeném případě, kdy pracujeme s výrokovou logikou a logický program ani hlavní cíl atomický neobsahují proměnné, zpětné usuzování (backward reasoning) určí logický a-nebo strom, který stanovuje prostor řešení cíle.

Hlavní cíl je vrchol stromu. Za předpokladu, že nějaký uzel ve stromu odpovídá hlavě klauzule, pak existuje množina potomků tohoto uzlu, která odpovídá mezi-cílům v těle této klauzuli. Potomci uzlu jsou spojení logickou spojkou a. Alternativní množina potomků odpovídající alternativní cestě řešení uzlu je spojeni pomocí logického nebo.

K prohledání prostoru řešení mohou být použity různé strategie. Prolog využívá sekvenční, LIFO a backtracking strategii, při které najednou zpracovává pouze jeden mezi-cíl a alternativní cestu. K hledání řešení je možné využívat i jiné strategie jako paralelní vyhledávání, inteligentní backtracking a nebo hledání metodou nejlepší-první (best-first).
