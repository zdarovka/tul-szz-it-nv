# Číslicové signály, DTFT/DFT/STFT
> Deterministické číslicové signály – popis v časové oblasti, periodicita, DTFT/DFT spektrum, krátkodobá spektrální analýza (STFT) + využití okénkových funkcí, vzorkovací teorém, kvantizace.

## Deterministický číslicový signál

Signál je (matematická) funkce, která reprezentuje informaci o vývoji nějaké fyzikální veličiny.
Takový signál je v reálném světě obvykle spojitý (analogový) - akustika, elektrický signál, teplota, tlak, etc. Vzorkováním (výběr vzorku v daných intervalech) a kvantováním (přiřazením jedné z konečného množství hodnot) vzniká číslicový signál.
Deterministický číslicový signál je pak každý číslicový signál, u kterého lze v jakémkoliv okamžiku zjistit hodnotu s absolutní jistotou (lze je popsat exaktním matematickým vzorcem, např. ![x[n] = sin(\omega n)](https://latex.codecogs.com/svg.latex?x%5Bn%5D%20%3D%20sin%28%5Comega%20n%29) - opakem jsou stochastické signály, kde jsou funkce popsány statistickým vzorcem.

**Diskrétní systém** - matematický operátor transformující vstupní diskrétní signál X[n] na výstupní diskrétní signál y[n]

## Popis signálu v časové oblasti

Signál ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) - indexovaná nekonečná posloupnost čísel z ![R](https://latex.codecogs.com/svg.latex?%5Cmathbb%7BR%7D) nebo ![C](https://latex.codecogs.com/svg.latex?%5Cmathbb%7BC%7D).
Vzniká buď vzorkováním spojitého signálu ![x(t)](https://latex.codecogs.com/svg.latex?x%28t%29) v ekvidistantních okamžicích (![T_s](https://latex.codecogs.com/svg.latex?T_s), vzorkovací perioda -> ![1/T_s = F_s](https://latex.codecogs.com/svg.latex?1/T_s%20%3D%20F_s), vzorkovací frekvence)

![x[n] = x(nT_s)](https://latex.codecogs.com/svg.latex?x%5Bn%5D%20%3D%20x%28nT_s%29)

nebo přirozeně diskrétní sekvencí (denní vývoj cenových akcií). 

Signál lze v časové oblasti rozložit do jednodušších funkcí, např.

jednotkový puls

![\delta[n] = 1 pokud n = 0, 0 otherwise](https://latex.codecogs.com/svg.latex?%5Cdelta%28n%29%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Cquad%20%5Ctext%7Bpokud%20%7D%20n%20%3D%200%5C%5C%200%20%26%20%5Cquad%20%5Ctext%7Bjinak%20%7D%5C%5C%20%5Cend%7Bcases%7D)

jednotkový skok

![u[n] = 1 pokud n >= 0, 0 otherwise](https://latex.codecogs.com/svg.latex?u%28n%29%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Cquad%20%5Ctext%7Bpokud%20%7D%20n%20%5Cgeq%200%5C%5C%200%20%26%20%5Cquad%20%5Ctext%7Bjinak%20%7D%5C%5C%20%5Cend%7Bcases%7D)

![vztah.png](vztah.png)

jednotkový skok je nekonečná posloupnost jednotkvých skoků

## Periodicita signálu

Pokud

![x[n] = x[n + N], \forall n, N \in \mathbb{Z}, N > 0](https://latex.codecogs.com/svg.latex?x%5Bn%5D%20%3D%20x%5Bn%20&plus;%20N%5D%2C%20%5Cforall%20n%2C%20N%20%5Cin%20%5Cmathbb%7BZ%7D%2C%20N%20%3E%200)

pak signál ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) je ![N](https://latex.codecogs.com/svg.latex?N)-periodický, hodnoty se opakují s periodou ![N](https://latex.codecogs.com/svg.latex?N).


## DTFT (Discrete Time Fourier Transform)

### Účel Fourierovy transformace

Ze signálu, který nese informaci, jak se veličina vyvíjí **v čase** (případně v prostoru - pro obraz), přecházím pomocí Fourierovy transformace do **frekvenční oblasti**, ve které vidím, jak jsou v signálu zastoupené jednotlivé frekvence.

### DTFT

Zobrazení z množiny posloupnosti prvků (časová oblast) do množiny spojitých komplexních funkcí reálné proměnné (frekvenční oblast)

![X(e^{j\omega}) = \sum\limits_{n=-\infty}^{\infty}{x[n] e^{-j n \omega}}](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29%20%3D%20%5Csum%5Climits_%7Bn%3D-%5Cinfty%7D%5E%7B%5Cinfty%7D%7Bx%5Bn%5D%20e%5E%7B-j%20n%20%5Comega%7D%7D)

kde ![\omega \in \mathbb{R}](https://latex.codecogs.com/svg.latex?%5Comega%20%5Cin%20%5Cmathbb%7BR%7D) je číslicová frekvence (f/Fs)

![X(e^{j\omega})](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29) je spojitá komplexní funkce reálného parametru ![\omega](https://latex.codecogs.com/svg.latex?%5Comega). DTFT si můžeme představit jako rozklad posloupnosti x[n] do množiny komplexních exponenciál. Aplikací DTFT na diskrétní signál x[n] získáme spojité DTFT spektrum ![X(e^{j\omega})](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29)

### DTFT spektrum

Komplexní funkce reálné proměnné ![\omega](https://latex.codecogs.com/svg.latex?%5Comega), vyjadřující míru korelace komplexních exponenciál na frekvencích ![\omega](https://latex.codecogs.com/svg.latex?%5Comega) a signálu x[n]  (v podstatě jak moc se signál podobá kosinusovce dané frekvence). Ve výsledku se jedná o rozložení signálu ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) na součet nekonečně mnoha funkcí ![\cos(\omega n + \Phi(\omega))](https://latex.codecogs.com/svg.latex?%5Ccos%28%5Comega%20n%20&plus;%20%5CPhi%28%5Comega%29%29) - harmonických signálů.

![X(e^{j n \omega_0}) = |X(e^{j n \omega_0})| e^{j \Phi \omega_0}](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%20n%20%5Comega_0%7D%29%20%3D%20%7CX%28e%5E%7Bj%20n%20%5Comega_0%7D%29%7C%20e%5E%7Bj%20%5CPhi%20%5Comega_0%7D)

DTFT spektrum se rozděluje na **magnitudové spektrum** (míra podobnosti ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) a ![e^{j n \omega_0}](https://latex.codecogs.com/svg.latex?e%5E%7Bj%20n%20%5Comega_0%7D))

![|X(e^{j n \omega_0})|](https://latex.codecogs.com/svg.latex?%7CX%28e%5E%7Bj%20n%20%5Comega_0%7D%29%7C)

a **fázové spektrum** (fázový posun mezi ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) a ![e^{j n \omega_0}](https://latex.codecogs.com/svg.latex?e%5E%7Bj%20n%20%5Comega_0%7D))

![\Phi(\omega_0)](https://latex.codecogs.com/svg.latex?%5CPhi%28%5Comega_0%29)

![](Obr41.jpg)

### Vlastnosti

- Periodicita - DTFT je periodická s periodou ![2\pi](https://latex.codecogs.com/svg.latex?2%5Cpi)

- Linearita
 
  ![ax_1[n] + bx_2[n] \Leftrightarrow aX_1(e^{j \omega}) + bX_2(e^{j \omega})](https://latex.codecogs.com/svg.latex?ax_1%5Bn%5D%20&plus;%20bx_2%5Bn%5D%20%5CLeftrightarrow%20aX_1%28e%5E%7Bj%20%5Comega%7D%29%20&plus;%20bX_2%28e%5E%7Bj%20%5Comega%7D%29)


- Otočení - otočení ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) v čase vede k otočení ![X(e^{j\omega})](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29) ve frekvenci, tedy

  ![x[-n] = X(e^{-j n \omega})](https://latex.codecogs.com/svg.latex?x%5B-n%5D%20%3D%20X%28e%5E%7B-j%20n%20%5Comega%7D%29)
  
- Posunutí - posunutí řady v čase vede k vynásobení ![X(e^{j\omega})](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29) komplexní exponenciálou, tedy:

  ![x[-n] = X(e^{-j n \omega})](https://latex.codecogs.com/gif.latex?x%5Bn-n_%7B0%7D%5D%20%3D%20e%5E%7B-j%5Comega%20n_%7B0%7D%7DX%28e%5E%7Bj%5Comega%20%7D%29)

- Konvoluční teorém - konvoluce dvou signálů v časové oblasti vede k vynásobení ve frekvenční oblasti

  ![h[n]*x[n] \Leftrightarrow H(e^{j n \omega})X(e^{j n \omega})](https://latex.codecogs.com/svg.latex?h%5Bn%5D*x%5Bn%5D%20%5CLeftrightarrow%20H%28e%5E%7Bj%20n%20%5Comega%7D%29X%28e%5E%7Bj%20n%20%5Comega%7D%29)

![DTFT](DTFT.png)

## DFT (Discrete Fourier Transform)

DTFT převádí nekonečnou diskrétní řadu ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) na spojitou funkci číslicové frekvence ![X(e^{j\omega})](https://latex.codecogs.com/svg.latex?X%28e%5E%7Bj%5Comega%7D%29). Zpětná rekonstrukce signálu ze spektra je možná, pokud známe hodnoty spektra pro všechny číslicové frekvence ![\omega](https://latex.codecogs.com/svg.latex?%5Comega). Pokud je trvání řady konečné, pak je možná perfektní rekonstrukce známe-li N vhodně zvolených frekvenčních bodů. 

V podstatě se jedná o vhodné ekvidistantní navzorkování spojitého DTFT spektra N vzorky tak, že

![\omega[k] = \frac{2 \pi k}{N}, 0 \leq k \leq N-1](https://latex.codecogs.com/svg.latex?%5Comega%5Bk%5D%20%3D%20%5Cfrac%7B2%20%5Cpi%20k%7D%7BN%7D%2C%200%20%5Cleq%20k%20%5Cleq%20N-1)

Vzorec DFT je tedy

![X[k] = \sum\limits_{n=0}^{N-1}{x[n] e^{-j 2 \pi n k / N}}, 0 \leq k < N-1](https://latex.codecogs.com/svg.latex?X%5Bk%5D%20%3D%20%5Csum%5Climits_%7Bn%3D0%7D%5E%7BN-1%7D%7Bx%5Bn%5D%20e%5E%7B-j%202%20%5Cpi%20n%20k%20/%20N%7D%7D%2C%200%20%5Cleq%20k%20%3C%20N-1)

nazýváme ![N](https://latex.codecogs.com/svg.latex?N)-bodová DFT.

- Vybráním ![N](https://latex.codecogs.com/svg.latex?N) bodů signálu se v podstatě provádí operace násobení signálu obdélníkovým okénkem (viz část o okénkách).

- DFT spektrum je ze základu oboustranné (od poloviny do konce je spektrum symetrické). Hodnoty od 0 do ![\pi](https://latex.codecogs.com/gif.latex?%5Cpi) budou stejné jako jako hodnoty od ![2\pi](https://latex.codecogs.com/gif.latex?2%5Cpi) do ![\pi](https://latex.codecogs.com/gif.latex?%5Cpi), pouze s opačným znaménkem. V praxi se proto pracuje obvykle s jednostranným spektrem (od 0 do ![\pi](https://latex.codecogs.com/gif.latex?%5Cpi)), které redundantní hodnoty vynechává (zanedbání jejich výpočtu také přispívá ke zrychlení výpočtu FFT).

![DFT](TimeWaveToDFT2.jpg)

## STFT (Short Time Fourier Transform)

Pokud aplikuji DFT na hodně dynamický signál (např. řeč), tak mi jeho spektrum nebude moc říkat (hodně dynamický signál bude vykazovat aktivitu velkého množství frekvencí).

Řešením tohoto problému je krátkodobá Fourierova transformace - STFT. Signál je nejprve rozdělen do rámců vhodné velikosti (tak aby spektrum v daném rámci bylo co nejvíce stacionární - dle úlohy, např. pro zpracování řeči je vhodné volit délku rámce mezi 10 - 40 ms), obvykle s překryvem okolo 50 %. 

Signál v každém rámci je vynásobem vhodnou okénkovací funkcí (Hamming, Hann, Blackmann...), výběr opět závisí na úloze. Na každý rámec je aplikována DFT.

Jednotlivé rámce jsou pak naskládány za sebe, čímž vzniká graf ukazující vývoj aktivity spektra v čase - spektrogram (obvykle jenom pro magnitudu).

![spektrogram](http://newt.phys.unsw.edu.au/jw/graphics/didj_spectrogram.JPG)

STFT je výhodné hlavně pro analýzu signálů se silně dynamickou povahou (např. řeč, hudba).

## Okénkovací funkce a prosakování spektra

Okénkovací funkce je funkce umožňující vybrat ze signálu konečně dlouhou sekvenci prvků. Signál je jednoduše v časové oblasti znásoben koeficienty daného okénka (např. obdélníkové okénko = 1 tam kde chci signál zachovat, 0 jinde).

Násobení v časové oblasti však odpovídá kruhové konvoluci v oblasti frekvenční. Výsledkem je tedy kruhová konvoluce spektra signálu a spektra okénkovací funkce, viz obrázek, tzv. prosakování spektra (spectral leakage).

![porovnání DTFT a okénkované DTFT](https://upload.wikimedia.org/wikipedia/commons/7/72/Spectral_leakage_Sine.svg)

U spektra okénkových funkcí se uvádějí dva hlavní parametry - šířka hlavního laloku a útlum postranních laloků. Ideální je co nejmenší šířku hlavního laloku a co největší útlum laloků postranních, reálně je to vždycky kompromis.
Při vysoké šířce hlavního laloku může dojít ke slévání blízkých frekvenčních komponent, při nízkém útlumu postranních laloků může docházet k maskování slabých frekvenčních komponent, viz obrázek - kosinusovky na frekvencích 1 kHz, 1,1 kHz a 3 kHz(slabá).

![obrázek laloky dvou okének](http://media.wiley.com/Lux/36/379636.image1.jpg)

Další problém nastává při navzorkování DTFT pomocí DFT - Pokud není okénko zvoleno ve správné délce, tak bude DTFT navzorkováno nevhodně, viz obrázek - perfektně navzorkované DTFT

![perfect DTFT sampling](http://blogs.mathworks.com/images/steve/2014/frequency_bins_for_sinusoid_v2_05.png)

a nevhodně navzorkované DTFT

![imperfect DTFT sampling](http://blogs.mathworks.com/images/steve/2014/frequency_bins_for_sinusoid_v2_07.png)

## Vzorkovací teorém

### Definice
Je-li ![\Omega_0](https://latex.codecogs.com/svg.latex?%5COmega_0) nejvyšší frekvencí obsaženou v analogovém signálu ![x_a(t)](https://latex.codecogs.com/svg.latex?x_a%28t%29) (signál je pásmově omezen), pak ![x_a(t)](https://latex.codecogs.com/svg.latex?x_a%28t%29) je možné jednoznačně rekonstruovat z jeho vzorků ![x_a(nT_s)](https://latex.codecogs.com/svg.latex?x_a%28nT_s%29) pokud

![\Omega_s = \frac{2\pi}{T_s} > 2\Omega_0](https://latex.codecogs.com/svg.latex?%5COmega_s%20%3D%20%5Cfrac%7B2%5Cpi%7D%7BT_s%7D%20%3E%202%5COmega_0)

![\Omega_0](https://latex.codecogs.com/svg.latex?%5COmega_0) se nazývá Nyquistova frekvence

### Prakticky
Nejvyšší frekvence obsažená v signálu nesmí být větší než polovina vzorkovací frekvence.

### Aliasing

Při nedodržení vzorkovacího teorému dochází k aliasingu - překládání frekvencí ve spektru - a tím k nejednoznačnosti rekonstrukce signálu, viz obrázek.

![1_alias.gif](1_alias.gif)

## Kvantizace

### Definice

Jedná se o transformaci spojitých amplitud diskrétní (navzorkované) řady ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) na diskrétní konečnou množinu amplitud

![\hat{x}[n] = Q(x[n])](https://latex.codecogs.com/svg.latex?%5Chat%7Bx%7D%5Bn%5D%20%3D%20Q%28x%5Bn%5D%29)

Spojitá amplituda je rozdělena na ![L](https://latex.codecogs.com/svg.latex?L) nepřekrývajících se intervalů ![l_k](https://latex.codecogs.com/svg.latex?l_k) pomocí ![L+1](https://latex.codecogs.com/svg.latex?L&plus;1) rozhodovacích hladin ![x_1, x_2,...,x_{L+1}](https://latex.codecogs.com/svg.latex?x_1%2C%20x_2%2C...%2Cx_%7BL&plus;1%7D)

![l_k = [x_k, x_{k+1}], k = 1, 2,..., L](https://latex.codecogs.com/svg.latex?l_k%20%3D%20%5Bx_k%2C%20x_%7Bk&plus;1%7D%5D%2C%20k%20%3D%201%2C%202%2C...%2C%20L)

Pokud ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) patří do intervalu ![l_k](https://latex.codecogs.com/svg.latex?l_k), kvantizace přiřadí ![\hat{x}[n]](https://latex.codecogs.com/svg.latex?%5Chat%7Bx%7D%5Bn%5D) hodnotu ![\hat{x}_k](https://latex.codecogs.com/svg.latex?%5Chat%7Bx%7D_k)


Otázkou tedy je, jak nastavit kvantizační hladiny. Toto nastavení je většinou závislé na citlivosti snímacího zařízení (ve fotografii třeba snímací senzor CCD). Podle něho nastavíme dolní a horní práh a pak rozdělíme hodnoty mezi nimi.
- Lineární (ekvidistantní) 
  – kvantizační hladiny jsou od sebe stejně vzdálené, většinou se používá tento způsob
- Nelineární 
  – úrovně kvantizačních hladin jsou přizpůsobené určitému účelu – tedy pokud nás zajímá určitá oblast intenzit. Používají se třeba logaritmické nebo exponenciální rozdělení.
- Další možnost je třeba taková, aby každá barva byla zastoupena na obrázku stejným počtem pixelů


