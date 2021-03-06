# 07. - Časová náročnost algoritmů

>Časová náročnost algoritmů. Průměrné a nejhorší chování. Úlohy P, NP a NP-úplné.

- Máme funkci ![f(n)](https://latex.codecogs.com/svg.latex?f%28n%29) a snažíme se popsat její asymptotické chování.
- Časová složitost se také označuje jako asymptotická složitost.
- Kromě časové složitosti se někdy určuje i paměťová náročnost.
- Používá se symbolika:
  - ![\mathcal{O}](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D) ... velké O
  - ![\Omega](https://latex.codecogs.com/svg.latex?%5COmega) ... velké omega
  - ![\Theta](https://latex.codecogs.com/svg.latex?%5CTheta) ... velké theta
- ![f: \mathbb{N} \rightarrow \mathbb{R}^+](https://latex.codecogs.com/svg.latex?f%3A%20%5Cmathbb%7BN%7D%20%5Crightarrow%20%5Cmathbb%7BR%7D%5E&plus;)
- ![g: \mathbb{N} \rightarrow \mathbb{R}^+](https://latex.codecogs.com/svg.latex?g%3A%20%5Cmathbb%7BN%7D%20%5Crightarrow%20%5Cmathbb%7BR%7D%5E&plus;)

**Asymptotická složitost**
Asymptotická složitost je způsob klasifikace počítačových algoritmů. Určuje operační náročnost algoritmu tak, že zjišťuje, jakým způsobem se bude chování algoritmu měnit v závislosti na změně velikosti (počtu) vstupních dat.
[Wikipedia](https://cs.wikipedia.org/wiki/Asymptotick%C3%A1_slo%C5%BEitost)

## Porovnání složitostí

V tabulce seřazeno od nejrychlejší po nejnáročnější.

| Notace  | Název | Příklad algoritmu |
| ------- | ----- | ----------------- |
| ![\mathcal{O}(1)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%281%29) | konstantní | nalezení prvku v hashovací tabulce |
| ![\mathcal{O}(\log n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28%5Clog%20n%29) | logaritmická | vyhledání prvku metodou půlení intervalu v seřazeném poli |
| ![\mathcal{O}(n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%29) | lineární | vyhledání prvku v neseřazeném poli |
| ![\mathcal{O}(n \cdot \log n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog%20n%29) | linearitmická | merge sort |
| ![\mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%5E2%29) | kvadratická | řazení pole výběrem |
| ![\mathcal{O}(n^3)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%5E3%29) | kubická | násobení matic |
| ![\mathcal{O}(2^n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%282%5En%29) | exponenciální |  |
| ![\mathcal{O}(n!)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%21%29) | faktoriálová | problém obchodního cestujícího hrubou silou |
| ![\mathcal{O}(n^n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%5En%29) | | |

## ![\mathcal{O}](https://latex.codecogs.com/svg.latex?%5CLARGE%20%5Cmathcal%7BO%7D) (Velké O)

- Omezuje růst funkce shora
- Používá se nejčastěji pro udávání asymptotické složitosti algoritmů (oproti ostatním dvěma notacím)
- Říká, že funkce ![f](https://latex.codecogs.com/svg.latex?f) **neroste rychleji** než kladný násobek funkce ![g](https://latex.codecogs.com/svg.latex?g)
- Omicron(f(x)) – algoritmus probíhá asymptoticky stejně rychle nebo rychleji než f(x).

**Zápis**

![f(n) \in \mathcal{O}(g(n))](https://latex.codecogs.com/svg.latex?f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28g%28n%29%29) právě tehdy, když:

![\exists K > 0 ~ \exists n_0~\forall n > n_0 ~ f(n) \leq K \cdot g(n)](https://latex.codecogs.com/svg.latex?%5Cexists%20K%20%3E%200%20%7E%20%5Cexists%20n_0%7E%5Cforall%20n%20%3E%20n_0%20%7E%20f%28n%29%20%5Cleq%20K%20%5Ccdot%20g%28n%29)

## ![\Omega](https://latex.codecogs.com/svg.latex?%5CLARGE%20%5COmega) (Velké omega)

- Omezuje růst funkce zdola
- Říká, že funkce ![f](https://latex.codecogs.com/svg.latex?f) **roste alespoň tak rychle** jako ![g](https://latex.codecogs.com/svg.latex?g) (až na multiplikativní konstantu)
- Omega(f(x)) – algoritmus probíhá asymptoticky stejně rychle nebo pomaleji než f(x).

**Zápis**

![f(n) \in \Omega(g(n)) \leftrightarrow \exists K > 0 ~ \exists n_0 ~ \forall n > n_0 ~ f(n) \geq K \cdot g(n)](https://latex.codecogs.com/svg.latex?f%28n%29%20%5Cin%20%5COmega%28g%28n%29%29%20%5Cleftrightarrow%20%5Cexists%20K%20%3E%200%20%7E%20%5Cexists%20n_0%20%7E%20%5Cforall%20n%20%3E%20n_0%20%7E%20f%28n%29%20%5Cgeq%20K%20%5Ccdot%20g%28n%29)

## ![\Theta](https://latex.codecogs.com/svg.latex?%5CLARGE%20%5CTheta) (Velké theta)

- Omezuje růst funkce shora i zdola
- Říká, že funkce ![f](https://latex.codecogs.com/svg.latex?f) **roste stejně rychle** jako funkce ![g](https://latex.codecogs.com/svg.latex?g) (až na multiplikativní konstanty)
- Theta(f(x)) – algoritmus probíhá asymptoticky stejně rychle jako f(x). Tj. je zároveň v O(f(x)) a v \\Omega(f(x)).

**Zápis**

![f(n) \in \Theta(g(n)) \leftrightarrow \exists K_1, K_2 > 0 ~ \exists n_0 ~ \forall n > n_0 ~ K_1 \cdot g(n) \leq f(n) \leq K_2 \cdot g(n)](https://latex.codecogs.com/svg.latex?f%28n%29%20%5Cin%20%5CTheta%28g%28n%29%29%20%5Cleftrightarrow%20%5Cexists%20K_1%2C%20K_2%20%3E%200%20%7E%20%5Cexists%20n_0%20%7E%20%5Cforall%20n%20%3E%20n_0%20%7E%20K_1%20%5Ccdot%20g%28n%29%20%5Cleq%20f%28n%29%20%5Cleq%20K_2%20%5Ccdot%20g%28n%29)

## Asymptotická složitost

 - Určuje operační náročnost algoritmu tak, že zjišťuje, jakým způsobem se bude chování algoritmu měnit v závislosti na změně velikosti (počtu) vstupních dat. Zapisuje se pomocí Omikron notace jako O(f(N)).
 - Používaný zápis znamená, že náročnost algoritmu je menší než A + B * f(N), kde A a B jsou vhodně zvolené konstanty a N je veličina popisující velikost vstupních dat.
 - Zandebáváme tedy multiplikativní i aditivní konstantu.

## Průměrná a nejhorší složitost

- V praxi se často udává
  - Nejhorší složitost ... složitost, v nejhorším možném případě
  - Průměrná složitost ... složitost úlohy v průměrném případě
- Tyto hodnoty nemusí být stejné
- Zatímco složitost v nejhorším případě lze analyticky spočítat, průměrnou složitost je u řady algoritmů nutno zjistit statisticky.

**Příklad**

- Quick sort
  - Nejhorší složitost ![\mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%5E2%29)
  - Průměrná složitost ![\mathcal{O}(n \cdot \log n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog%20n%29)
  - Závisí na vhodné volbě pivota
  - V praxi se algoritmus používá, protože ve většině případů funguje rychle a je jednoduchý na implementaci

- Vyhledávání prvku v nesetříděném poli
  - Nejhorší složitost ![\mathcal{O}(n)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28n%29)
  - Průměrná složitost ![\mathcal{O}(\frac{n}{2})](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28%5Cfrac%7Bn%7D%7B2%7D%29)
  - *Pozn. autora*: Zde to asi nemá význam příliš rozlišovat, jelikož se jedná o stejnou složitost, která se liší pouze konstantou.

## Úlohy P, NP, NP-úplné

![Porovnání P, NP, NP-úplných úloh](07_p_np_np_complete.png)

1. Úlohy P (polynomial time)
    - Úlohy řešitelné v polynomiálním čase ![\mathcal{O}(f(n)) \subset \mathcal{O}(n^k)](https://latex.codecogs.com/svg.latex?%5Cmathcal%7BO%7D%28f%28n%29%29%20%5Csubset%20%5Cmathcal%7BO%7D%28n%5Ek%29)
    - Příklady:
      - Násobení
      - Řazení
    - V teorii složitosti je P jednou z nejzákladnějších tříd složitosti. Obsahuje všechny problémy řešitelné pomocí deterministického Turingova stroje v polynomiálním čase.

2. Úlohy NP (non-deterministic polynomial time)
    - Úlohy, jejichž *řešení lze ověřit v polynomiálním čase*
    - Patří sem všechny úlohy z P, ale kromě toho i další, které už nepatří do P, např.:
      - Faktorizace - rozklad na prvočísla (asymetrická kryptografie)
      - Návrh desek plošných spojů
    - NP (zkratka nedeterministicky polynomiální) je množina problémů, které lze řešit v polynomiálně omezeném čase na nedeterministickém Turingově stroji - na počítači, který umožňuje v každém kroku rozvětvit výpočet na n větví, v nichž se posléze řešení hledá současně. Ekvivalentně se hovoří o stroji, který na místě rozhodování uhodne správnou cestu výpočtu. Alternativně lze tyto problémy definovat tak, že je to množina problémů, u kterých lze pro dodaný výsledek v polynomiálním čase ověřit jeho správnost (ale obecně nikoliv nalézt řešení v polynomiálním čase).

3. Úlohy NP-úplné
    - Jsou úlohy, které jsou NP, nejsou P a *lze na ně převést všechny ostatní NP úlohy
    - Problém obchodního cestujícího
    - Pokud by se našlo řešení NP-úplné úlohy, které by bylo schopné řešit danou úlohu v polynomiálním čase, znamenalo by to, že ![P = NP](https://latex.codecogs.com/svg.latex?P%20%3D%20NP) (všechny NP úlohy bychom dokázali vyřešit v polynomiálním čase)
    - Konsenzus je, že ![P \neq NP](https://latex.codecogs.com/svg.latex?P%20%5Cneq%20NP), ale zatím to nebylo dokázáno (jedná se o jeden z [Millenium Prize Problems](https://en.wikipedia.org/wiki/Millennium_Prize_Problems))
    - NP-úplné (NP-complete, NPC) problémy jsou takové nedeterministicky polynomiální problémy, na které jsou polynomiálně redukovatelné všechny ostatní problémy z NP. To znamená, že třídu NP-úplných úloh tvoří v jistém smyslu ty nejtěžší úlohy z NP. Pokud by byl nalezen polynomiální deterministický algoritmus pro nějakou NP-úplnou úlohu, znamenalo by to, že všechny nedeterministicky polynomiální problémy jsou řešitelné v polynomiálním čase, tedy že třída NP se „zhroutí“ do třídy P (NP = P). Otázka, zda nějaký takový algoritmus existuje, zatím nebyla rozhodnuta, předpokládá se však, že NP ≠ P (je však zřejmé, že P ⊆ NP)
    - Hlavní důvod, proč jsou NP-úplné úlohy tak zajímavé, je právě jejich velmi obtížná řešitelnost. Díky ní nacházejí uplatnění v moderní kryptografii, kde musíme být schopni rychle ověřovat správnost řešení, ale jeho nalezení musí trvat dlouho.
    
Polynomiální složitost: funkce složitosti je polynomiální, tedy ve tvaru "a\*n^k + méně_významné_členy", kde "k" je pevně dané přirozené číslo, a méně_významné_členy znamená výraz obsahující pouze násobky n v mocnině nejvýše k-1...
    
    
Exponenciální složitost: 2 jednotky pro data velikost 1, 4 pro 2, 8 pro 3, 16 pro 4, ..., 65536 pro 16, atd. - tedy funkce 2^n, resp. a\*k^n kde k je nějaký pevně daný základ a a je nějaká konstanta. 

Zatímco polynomiální složitost je ještě jakžtakž vypočitatelná hrubou silou, exponenciální složitost se považuje za prakticky nevypočitatelný algoritmus pro již velmi malá data.
