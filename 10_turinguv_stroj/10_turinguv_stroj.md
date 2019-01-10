# 10. - Turingův stroj
>Turingův stroj, problém zastavení, totální a parciální rozhodnutelnost tříd problémů, rekurzivní a rekurzivně spočetné množiny, jejich vztah.

## Turingův stroj
- Teoretický model počítače popsaný matematikem Alanem Turingem
- Lze pomocí něj implementovat libovolný algoritmus (algoritmus a TS často chápáno jako synonymum)
- V porovnání s KA je to silnější nástroj
- Rozpoznává jazyky typu 0
- Stejně složité úlohy jsou schopny řešit i Postovy stroje nebo Konečné stroje se dvěma a více zásobníky

**Základní části:**

  1. **Páska**
    - Slouží jako paměť
    - Nekonečná (doprava)
  2. **Čtecí hlava**
    - Určuje pozici na pásce
    - Umožňuje čtení/zápis libovolného znaku na pásku
    - Pohybuje se vždy o jeden krok doleva (L) nebo doprava (R)
  3. **Program**
    - Zapisovali jsme jako konečný, ohodnocený a orientovaný graf (lze zapsat i pomocí insturkcí)
    - Definuje počáteční stav
    - Definuje množinu koncových stavů
    - Graf znázorňuje přechody mezi jednotlivými stavy a činnost čtecí hlavy (čtení, zápis, posun)
    - Jednotlivé hrany grafu jsou ohodnoceny (čtený symbol, přepisuje na, pohyb hlavy vlevo/vpravo)
    - Na začátku pásky je zapsáno vstupní slovo, čtecí hlava je na začátku

![Ukázka Turingova stroje](10_ts.png)

*Ukázka Turingova stroje*

![Graf Turingova stroje](10_graf.png)

*Graf Turingova stroje*

**Výsledek činnosti Turingova stroje:**

  - **Akceptování slova w** (AKC) - dosáhne li stroj konečného přijímacího stavu
  - **Zamítnutí slova w** (ZAM) - dosáhne li stroj konečného zamítacího stavu nebo není definován stav pro daný přechod
  - **Cyklování** (CYK) - znamená, že se stroj dostal do cyklu, kdy se periodicky opakuje jeho činnost bez možnosti zastavení.

Turingovy stroje lze považovat za **ekvivaletní**, pokud **akceptují stejná slova**.

**Formální definice:**

TS ![T](https://latex.codecogs.com/gif.latex?T) se definuje nad vstupní abecedou ![\Sigma](https://latex.codecogs.com/gif.latex?%5CSigma).

![T = (Q, \pi, \delta, q_0, F)](https://latex.codecogs.com/gif.latex?T%20%3D%20%28Q%2C%20%5Cpi%2C%20%5Cdelta%2C%20q_0%2C%20F%29), kde

- ![Q](https://latex.codecogs.com/gif.latex?Q) je množina stavů stroje (neprázdná)
- ![\pi](https://latex.codecogs.com/gif.latex?%5Cpi) je abeceda stroje (neprázdná), ![\pi = \Sigma \cup V \cup \{\Delta\}](https://latex.codecogs.com/gif.latex?%5Cpi%20%3D%20%5CSigma%20%5Ccup%20V%20%5Ccup%20%5C%7B%5CDelta%5C%7D) (abeceda stroje se skládá ze vstupní abecedy, pomocných znaků a prázdného symbolu)
- ![\delta](https://latex.codecogs.com/gif.latex?%5Cdelta) je parciální zobrazení, které přiřazuje nekoncovému stavu stroje a vstupnímu symbolu následný stav stroje, symbol z abecedy stroje (pro zápis) a směr posunu čtecí hlavy
  ![\delta : (Q - F) \times \pi \rightarrow Q \times \pi \times \{L, R\}](https://latex.codecogs.com/gif.latex?%5Cdelta%20%3A%20%28Q%20-%20F%29%20%5Ctimes%20%5Cpi%20%5Crightarrow%20Q%20%5Ctimes%20%5Cpi%20%5Ctimes%20%5C%7BL%2C%20R%5C%7D)
- ![q_0](https://latex.codecogs.com/gif.latex?q_0) je počáteční stav
- ![F](https://latex.codecogs.com/gif.latex?F) je množina koncových stavů

## Totální a parciální rozhodnutelnost problémů
Máme třídu problémů na které lze odpovědět ANO/NE a k nim odpovídající algoritmus (TS), který všechny tyto problémy řeší.

### Totálně rozhodnutelné problémy

Třída problému je **totálně rozhodnutelná** právě tehdy, když existuje TS, který pro všechny problémy z dané třídy zastaví svoji činnost a vydá odpověď (AKC/ZAM), tedy **nikdy necykluje**.

Příklad:
  - Problém ekvivalence automatů
  - Problém odvození v kontextových gramatikách

Pokud je třída problémů *totálně rozhodnutelná*, tak je i *parciálně rozhodnutelná* (neplatí naopak!)

### Parciálně rozhodnutelné problémy

- Třída problémů je **parciálně rozhodnutelná** právě tehdy, když existuje TS, který:

  - je-li odpověď na daný problém ANO, tak zastaví **akceptováním** AKC,
  - je-li odpověď na daný problém NE, tak buď zastaví **zamítnutím** ZAM nebo **cykluje** CYK

Příklad:
   - *problém zastavení* TS je parciálně rozhodnutelný

Pokud jsou obě třídy problémů ![\mathcal{P}, \overline{{\mathcal{P}}}](https://latex.codecogs.com/gif.latex?%5Cmathcal%7BP%7D%2C%20%5Coverline%7B%7B%5Cmathcal%7BP%7D%7D%7D) (chápeme jako doplňěk, tvořený z negací všech problémů původní třídy) *parciálně rozhodnutelné*, pak je třída problémů ![\mathcal{P}](https://latex.codecogs.com/gif.latex?%5Cmathcal%7BP%7D) *totálně rozhodnutelná* (tím pádem je i ![\overline{\mathcal{P}}](https://latex.codecogs.com/gif.latex?%5Coverline%7B%5Cmathcal%7BP%7D%7D) totáně rozhodnutelná).

*Poznámka:* Existují i problémy, které nejsou ani parciálně rozhodnutelné, např. problém **ne**zastavení TS.

## Problém zastavení
>Existuje takový Turingův stroj, který by dokázal rozhodnout, zda pro libovolný TS M a vstupní slovo w stroj M zastaví?

**Takový TS neexistuje**, problém zastavení pro Turingovy stroje je nerozhodnutelný.

[Wikipedia](https://cs.wikipedia.org/wiki/Probl%C3%A9m_zastaven%C3%AD)

**Důkaz sporem:**

Uvažujeme, že existuje výše popsaný TS, který označíme **A**.

![Halting problem A](10_halting_problem_A.jpg)

Na vstupu je **kód stroje TS M a slovo w**. Tento **TS A** ukončí činnost akceptováním, pokud **TS M zastaví pro slovo w**. 
 - **TS A** Svoji činnost ukončí zamítnutím, pokud stroj M pro dané slovo cykluje.

**TS A** rozšíříme na **TS B** tak, že:
- vstupem bude pouze kód stroje **TS M** a ten bude zároveň i vstupním slovem,
- stroj **B** bude **cyklovat** právě tehdy, když stroj **TS A skončí akceptováním (když stroj M zastaví)**,
- stroj **B** zastaví, pokud stroj **TS A skončí zamítnutím (a tedy stroj M cykluje)**.

![Halting problem B](10_halting_problem_B.jpg)

Vytvořený stroj **TS B** je ovšem také TS. Pokud na vstup stroje **TS B** dáme jeho vlastní kód, dochází ke sporu, protože:
- stroj B cykluje právě tehdy, pokud stroj B zastaví,
- stroj B zastaví právě tehdy, pokud stroj B cykluje.

![Halting problem B spor](10_halting_problem_B_paradox.jpg)

Jedná se o paradox, což dokazuje, že nelze sestavit TS, který by o libovolném TS rozhodl, zda zastaví pro slovo w. Halting problém je tedy nerozhodnutelný (resp. parciálně rozhodnutelný).

## Rekurzivní a rekurzivně spočetné množiny

### Rekurzivní množina

Množina ![S \subset \Sigma^*](https://latex.codecogs.com/gif.latex?S%20%5Csubset%20%5CSigma%5E*) se nazývá **rekurzivní** právě tehdy, když existuje TS, který

1. **akceptuje** všechna slova ![w \in S](https://latex.codecogs.com/gif.latex?w%20%5Cin%20S),
2. **zamítne** všechna ostatní slova ![w \in \Sigma^* - S](https://latex.codecogs.com/gif.latex?w%20%5Cin%20%5CSigma%5E*%20-%20S) (a tedy *nikdy necykluje*)

### Rekurzivně spočetná množina

Množina ![S \subset \Sigma^*](https://latex.codecogs.com/gif.latex?S%20%5Csubset%20%5CSigma%5E*) se nazývá **rekurzivně spočetná** právě tehdy, když existuje TS, který

1. **akceptuje** každé slovo ![w \in S](https://latex.codecogs.com/gif.latex?w%20%5Cin%20S)
2. buď **zamítne** nebo **cykluje** pro slova ![w \in \Sigma^* - S](https://latex.codecogs.com/gif.latex?w%20%5Cin%20%5CSigma%5E*%20-%20S)

Množina ![S \subset \Sigma^*](https://latex.codecogs.com/gif.latex?S%20%5Csubset%20%5CSigma%5E*) je *rekurzivní* právě tehdy, když obě množiny ![S, \Sigma^* - S](https://latex.codecogs.com/gif.latex?S%2C%20%5CSigma%5E*%20-%20S) jsou *rekurzivně spočetné*.

### Vztah mezi RSM a RM

![RM \subsetneqq RSM](https://latex.codecogs.com/gif.latex?RM%20%5Csubsetneqq%20RSM) ... rekurzivní množiny jsou podmnožinami rekurzivně spočetných množin

![Vztah RM a RSM](10_vztah_rm_rsm.png)

Existuje i množina, která **není ani RSM**. Daný jazyk tím pádem **není rozpoznatelný Turingovým strojem**.
