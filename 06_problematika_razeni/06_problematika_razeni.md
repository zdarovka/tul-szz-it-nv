# 6. Problematika řazení

> Problematika řazení – základní algoritmy a jejich složitost.

## Formální definice

![A](https://latex.codecogs.com/svg.latex?%5Clarge%20A) ... abeceda, nad kterou je dáno řazení

![a_{i_1}, a_{i_2}, \ldots , a_{i_n}](https://latex.codecogs.com/svg.latex?%5Clarge%20a_%7Bi_1%7D%2C%20a_%7Bi_2%7D%2C%20%5Cldots%20%2C%20a_%7Bi_n%7D) ... posloupnost (slovo) nad abecedou ![A](https://latex.codecogs.com/svg.latex?%5Clarge%20A)

Cílem je nalézt permutaci ![\pi \in S_n](https://latex.codecogs.com/svg.latex?%5Clarge%20%5Cpi%20%5Cin%20S_n) takovou, že posloupnost ![a_{\pi(i_1)} a_{\pi(i_2)} \ldots a_{\pi(i_n)}](https://latex.codecogs.com/svg.latex?%5Clarge%20a_%7B%5Cpi%28i_1%29%7D%20a_%7B%5Cpi%28i_2%29%7D%20%5Cldots%20a_%7B%5Cpi%28i_n%29%7D) je setříděná, tj. ![a_{\pi(i_j)} \leq a_{\pi(i_{j+1})}](https://latex.codecogs.com/svg.latex?%5Clarge%20a_%7B%5Cpi%28i_j%29%7D%20%5Cleq%20a_%7B%5Cpi%28i_%7Bj&plus;1%7D%29%7D)

## Vlastnosti

- *na místě* - pro řazení se nepoužívá žádná další datová struktura (např. další pole)
- *stabilní* - v seřazené posloupnosti je zachováno pořadí rovnocenných prvků
- *přirozený* - rychleji zpracuje (částečně) seřazenou množinu, u nepřirozeného to nehraje roli
- [*interní*](https://en.wikipedia.org/wiki/Internal_sort) - všechna data jsou k dispozici v paměti
- [*externí*](https://en.wikipedia.org/wiki/External_sorting) - další prvky přichází v průběhu řazení
- složitost 
 - [*časová složitost*](https://cs.wikipedia.org/wiki/Asymptotick%C3%A1_slo%C5%BEitost) (dále jako ![f(n)](https://latex.codecogs.com/svg.latex?%20f%28n%29)) viz okruh [7 - Časová náročnost algoritmů](https://github.com/tomaskrizek/tul-szz-it-nv/blob/master/07_casova_narocnost_algoritmu/07_casova_narocnost_algoritmu.md)
 - *paměťová složitost*

## Rozlišujeme

a. Postupné rozšiřování setříděné části
- Selection sort ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)
- Insertion sort ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

b. Záměnu dvojic po sobě jdoucích prvků
- Bubble sort ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)
- Sinking sort ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)
- Shaker ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

c. Divide and Conquer
- Merge sort ![f(n) \in \mathcal{O}(n \cdot \log_2 n)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog_2%20n%29)
- Quick sort ![f(n) \in \mathcal{O}(n \cdot \log_2 n)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog_2%20n%29)

| Anglicky       | Česky             | Nejlepší   | Průměrně   | Nejhorší   | Dodatečná pamět | Stabilní  | Přirozené | Metoda    |
|----------------|-------------------|------------|------------|------------|-----------------|-----------|-----------|-----------|
| Selection sort | Řazení výběrem    | O(n²)      | O(n²)      | O(n²)      | O(1)            | zprav. ne | ne        | výběr     |
| Insertion sort | Řazení vkládáním  | O(n)       | O(n²)      | O(n²)      | O(1)            | ano       | ano       | vkládání  |
| Bubble sort    | Bublinkové řazení | O(n)       | O(n²)      | O(n²)      | O(1)            | ano       | ano       | záměna    |
| Merge sort     | Řazení slučováním | O(n log n) | O(n log n) | O(n log n) | O(log n)        | ano       | ne       | slučování |
| Quicksort      | Rychlé řazení     | O(n log n) | O(n log n) | O(n²)      | O(log n)        | ne        | ne        | záměna    |

## a) Rozšiřování setříděné části

### Selection Sort

V každém kroku vybere z nesetříděné části nejmenší prvek a vloží nakonec setříděné části.
Není stabilní jelikož dochazí k prohazování prvků, a tudíž se mohou stejné hodnoty v poli přeházet.

![](SelectionSortNguyen.gif)

![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

### Insertion Sort

Vyberu první prvek z nesetříděné části a zařadím ho na správné místo v setříděné části.

![](insertion-sort-o.gif)

v nejhorším případě ... ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

pro téměř seřazenou posloupnost ... ![f(n) \in \mathcal{O}(n)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%29)

## b) Záměna dvojic mimo pořadí

### Bubble Sort

Nesetříděnou posloupnost procházím shora dolů a porovnávám dvojice po sobě jdoucích prvků; dvojice mimo pořadí zaměním. Tím se na přední pozici dostane vždy nejmenší prvek.

![Bubble sort](Sorting_bubblesort_anim.gif)

![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

### Sinking Sort

For example, in Donald Knuth's The Art of Computer Programming, Volume 3: Sorting and Searching he states in section 5.2.1 'Sorting by Insertion', that [the value] "settles to its proper level" and that this method of sorting has sometimes been called the sifting or sinking technique.[clarification needed]

This debate is perpetuated by the ease with which one may consider this algorithm from two different but equally valid perspectives:

The larger values might be regarded as heavier and therefore be seen to progressively sink to the bottom of the list
The smaller values might be regarded as lighter and therefore be seen to progressively bubble up to the top of the list.

### Shaker Sort

Kombinace Bubble Sort a Sinking Sort. Střídá se procházecí pořadí.

![](Sorting_shaker_sort_anim.gif)

## c) Divide and conquer

### Merge sort

Vstupní posloupnost se rekurzivně dělí na dvě poloviny až jsou poslopnosti délky jedna. Následuje zpětný chod, tj. sestavení setříděné posloupnosti. Při zpětném chodu se sloučí dvě fronty do jedné (nejmenší prvek je vždy na začátku jedné ze dvou front).

![Ukázka merge sort](06_merge_sort.jpg)

![f(n) \in \mathcal{O}(n \cdot \log_2 n)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog_2%20n%29)

### Quick sort

Zvolíme tzv. pivota a posloupnost rozdělíme na dvě části. Jedna z nich obsahuje prvky menší nebo rovny pivotu a druhá obsahuje prvky větší než pivot. Na tyto dvě posloupnosti se rekurzivně aplikuje stejná operace.

![Ukázka algoritmu quick sort](06_quick_sort.jpg)

![](Quicksort.gif)

složitost v nejhorším případě ... ![f(n) \in \mathcal{O}(n^2)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%5E2%29)

průměrná složitost ... ![f(n) \in \mathcal{O}(n \cdot \log_2 n)](https://latex.codecogs.com/svg.latex?%20f%28n%29%20%5Cin%20%5Cmathcal%7BO%7D%28n%20%5Ccdot%20%5Clog_2%20n%29)
