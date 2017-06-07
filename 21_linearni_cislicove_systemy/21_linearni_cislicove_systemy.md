# 21. - LTI číslicové systémy

> Vlastnosti (linearita, kauzalita, stabilita), impulsní odezva (FIR/IIR), 
frekvenční charakteristika, přenosová funkce, skupinové zpoždění, lineární diferenční rovnice 
s konstantními koeficienty, systém s lineární a minimální fází. 

**Systém** dokáže generovat, zpracovávat, modifikovat a přijímat signály. Signál je projevem činnosti systému.

Příklady:
- Hudební nástroj - lze považovat za systém generující zvuk
- Zesilovač, ekvalizér - systém, který modifikuje zvukový signál
- A/D a D/A převodník - transformují jeden typ signálu na jiný
- Reproduktor - převádí elektrický signál na akustický, atd.

**LTI (Linear Time Invariant)** systémy jsou takové systémy, které jsou lineární a časově nezávislé.

## Vlastnosti

### Linearita

Lineární systém je aditivní a homogenní

##### Aditivita (Additivity)

![T (x1[n] + x2[n]) = T (x1[n]) + T (x2[n])](https://latex.codecogs.com/svg.latex?T%28x_%7B1%7D%5Bn%5D%20&plus;%20x_%7B2%7D%5Bn%5D%29%20%3D%20T%28x_%7B1%7D%5Bn%5D%29%20&plus;%20T%28x_%7B2%7D%5Bn%5D%29)

##### Homogenita (Homogenity)

![T (cx[n]) = cT (x[n])](https://latex.codecogs.com/svg.latex?T%20%28cx%5Bn%5D%29%20%3D%20cT%20%28x%5Bn%5D%29)

**Pro linearitu tedy platí podmínka**

![F(ax_1 + bx_2) = aF(x_1) + bF(x_2)](https://latex.codecogs.com/svg.latex?F%28ax_%7B1%7D%20&plus;%20bx_%7B2%7D%29%20%3D%20aF%28x_%7B1%7D%29%20&plus;%20bF%28x_%7B2%7D%29)

- výstup systému pro lineární kombinaci budících signálů je roven lineární kombinaci výstupů na jednotlivé budící signály

- z linearity vyplývá princip superpozice (výstup systému lze složit z výstupu na dílčí buzení)

**Příklad lineárního systému**

![y(t) = kx(t)](https://latex.codecogs.com/svg.latex?y%28t%29%20%3D%20k%5Ccdot%20x%28t%29)

**Příklad nelineárního systému**

![y(t) = x^{2}(t)](https://latex.codecogs.com/svg.latex?y%28t%29%20%3D%20x%5E%7B2%7D%28t%29)

![y(t) = x(t) + 1](https://latex.codecogs.com/svg.latex?y%28t%29%20%3D%20x%28t%29%20&plus;%201)


### Kauzalita

Výstup kauzálního systému závisí pouze na současných a minulých hodnotách

- Kauzální systém : ![y(t) = x(t) + x(t-1)](https://latex.codecogs.com/svg.latex?y%28t%29%20%3D%20x%28t%29%20&plus;%20x%28t-1%29)
- Nekauzální systém : ![y(t) = x(t) + x(t+1)](https://latex.codecogs.com/svg.latex?y%28t%29%20%3D%20x%28t%29%20&plus;%20x%28t&plus;1%29)
- LTI systémy jsou kauzální poouze v případě, že h[n] = 0 pro n < 0

### Stabilita

- Pokud je vstup do systému omezený (např. na interval <-1;1>) tak jeho výstup bude také omezený (tzn. jeho rozsah se nebude rozpínat do nekonečna)
- Obecně lze říct že systém je stabilní, pokud amplituda jeho výstupu neroste nad všechny meze. (Nestabilní systém je např. s kladnou zpětnou vazbou)
- LTI szstémy jsou stabilní pouze v případě, že ![n_0](https://latex.codecogs.com/gif.latex?%5Csum_%7Bn%20%3D%20-%5Cinfty%7D%5E%7B%5Cinfty%7D%20%7Ch%5Bn%5D%7C%3C%20%5Cinfty)

### Invariantnost vůči (časovému) posunu

- Nechť ![y[n]](https://latex.codecogs.com/svg.latex?y%5Bn%5D) je výstup systému ![T(\cdot)](https://latex.codecogs.com/svg.latex?T%28%5Ccdot%29) na ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) 
- Pak ![T(\cdot)](https://latex.codecogs.com/svg.latex?T%28%5Ccdot%29) je invariantní vůči posunu, pokud pro libovolné zpoždění ![n_0](https://latex.codecogs.com/svg.latex?n_0) platí, že odezva na ![n_0](https://latex.codecogs.com/gif.latex?x%5Bn-n_%7B0%7D%5D) je ![n_0](https://latex.codecogs.com/gif.latex?y%5Bn-n_%7B0%7D%5D)

### Popis LTI systému

lze popsat pomocí:

- Impulzní odezva
	- výčtem prvků: ![h[n] = [2,-1]](https://latex.codecogs.com/svg.latex?h%5Bn%5D%20%3D%20%5B2%2C-1%5D)
- Diferenční rovnicí: ![y[n] = 2\delta[n] - \delta[n-1]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%202%5Cdelta%5Bn%5D%20-%20%5Cdelta%5Bn-1%5D)
- Frekvenční charakteristika
	- ![H(e^{j \omega}) = 2 \cdot x(e^{-j \cdot \omega \cdot 0}) - 1 \cdot x(e^{-j \cdot \omega \cdot 1})](https://latex.codecogs.com/svg.latex?H%28e%5E%7Bj%20%5Comega%7D%29%20%3D%202%20%5Ccdot%20x%28e%5E%7B-j%20%5Ccdot%20%5Comega%20%5Ccdot%200%7D%29%20-%201%20%5Ccdot%20x%28e%5E%7B-j%20%5Ccdot%20%5Comega%20%5Ccdot%201%7D%29)
- Přenosová funkce
	- ![H(z) = 2 - z^{-1}](https://latex.codecogs.com/svg.latex?H%28z%29%20%3D%202%20-%20z%5E%7B-1%7D)

## Impulsní odezva (FIR/IIR)

- je výstup LTI systémů na tzv. jednotkový impulz (značen písmenem ![\delta](https://latex.codecogs.com/svg.latex?%5Cdelta))
- značí se ![h[n]](https://latex.codecogs.com/svg.latex?h%5Bn%5D)

### Konvoluce

Vyjadřuje vztah mezi vstupem a výstupem LTI systému
daného impulsní odezvou

![y[n] = x[n] * h[n] = \sum_{k=0}^{N-1}x[k]\cdot h[n-k]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%20x%5Bn%5D%20*%20h%5Bn%5D%20%3D%20%5Csum_%7Bk%3D0%7D%5E%7BN-1%7Dx%5Bk%5D%5Ccdot%20h%5Bn-k%5D)

### FIR (Finite Impulse Response)

- jsou systémy s konečnou impulzní odezvou
- bez zpětné vazby
- např. ![y[n] = x[n] + x[n - 1]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%20x%5Bn%5D%20&plus;%20x%5Bn%20-%201%5D)

### IIR (Infinite Impulse Response)

- jsou systémy s nekonečnou impulzní odezvou
- obsahují zpětnou vazbu
- např. ![y[n] = x[n] + 0,5y[n - 2]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%20x%5Bn%5D%20&plus;%200%2C5y%5Bn%20-%202%5D)


## Frekvenční charakteristika

Funkci, která popisuje závislost vlastních hodnot na frekvenci ω značíme ![H(ejω)](https://latex.codecogs.com/svg.latex?H%28e%5E%7Bj%5Comega%7D%29)


Získáme ji aplikací DTFT na impulzní odezvu systému ![h[n]](https://latex.codecogs.com/svg.latex?h%5Bn%5D)

![ssss](frekv_char.png)

Obvykle se uvádí ve formě dvou reálných funkcí:

- magnitudová charakteristika ![|H(ejω)|](https://latex.codecogs.com/svg.latex?%7CH%28e%5E%7Bj%5Comega%7D%29%7C)
- fázová charakteristika ![\Phi(\omega)](https://latex.codecogs.com/svg.latex?%5CPhi%28%5Comega%29)

Dohromady: ![H(e^{j\omega}) = |H(e^{j\omega})| \cdot e^{j\Phi(\omega)}](https://latex.codecogs.com/svg.latex?H%28e%5E%7Bj%5Comega%7D%29%20%3D%20%7CH%28e%5E%7Bj%5Comega%7D%29%7C%20%5Ccdot%20e%5E%7Bj%5CPhi%28%5Comega%29%7D)

![ssss](frekvencniCharakteritika.PNG)

## Skupinové spoždění

- Místo fázové charakteristiky (u filtrů s lineární fázovou charakteristikou) se často uvádí skupinové zpoždění
- Udává zpoždění úzkopásmového signálu složeného ze skupiny harmonitckých komponent v okolí frekvence ω po průchodu LTI systémem (ve vzorcích)
- ![τ(ω) = −dφ(ω)/dω](https://latex.codecogs.com/svg.latex?%5Ctau%28%5Comega%29%20%3D%20-%5Cfrac%7Bd%20%5CPhi%28%5Comega%29%7D%7Bd%20%5Comega%7D) 

## Přenosová funkce

- Získáme ji pomocí Z-transformace impulsní odezvy

### Z-transformace

- Z-transformace diskrétní řady ![x[n]](https://latex.codecogs.com/svg.latex?x%5Bn%5D) je deﬁnována jako:
	- ![X(z) = \sum_{n = 0}^{N-1} x[n] \cdot z^{-n}](https://latex.codecogs.com/svg.latex?X%28z%29%20%3D%20%5Csum_%7Bn%20%3D%200%7D%5E%7BN-1%7D%20x%5Bn%5D%20%5Ccdot%20z%5E%7B-n%7D)
- Z-obraz je komplexní funkce komplexní proměnné. Jeho vlastnosti se nejčastěji popisují v z-rovině
- DTFT ze Z-obrazu získáme dosazením ![z = e^{j\omega}](https://latex.codecogs.com/svg.latex?z%20%3D%20e%5E%7Bj%5Comega%7D), tedy DTFT je tvořena body na jednotkové kružnici v Z rovině

#### Přenosová funkce

![](o21_frek_char.png)

- ![B(z)](https://latex.codecogs.com/svg.latex?B%28z%29) jsou koeficienty vstupu a ![A(z)](https://latex.codecogs.com/svg.latex?A%28z%29) jsou koeficienty zpětné vazby
- Příklad: 
	- ![y[n] - 5y[n-3] = 2x[n] - 3x[n-1]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20-%205y%5Bn-3%5D%20%3D%202x%5Bn%5D%20-%203x%5Bn-1%5D)
	- ![H(z) = \frac{2 - 3z^{-1}}{1-5z^{-3}}](https://latex.codecogs.com/svg.latex?H%28z%29%20%3D%20%5Cfrac%7B2%20-%203z%5E%7B-1%7D%7D%7B1-5z%5E%7B-3%7D%7D)
  
- Přenosová funkce je velmi důležitá z hlediska analýzy systémů (stabilita, kauzalita, systémy s lineární fází, minimální fází apod.)


## Lineární diferenční rovnice s konstantními koeficienty

- Linear constant coeﬃcient diﬀerence equation (LCCDE)
- Speciální případ diferenčních rovnic popisující LTI systémy

![y[n] = \sum_{k=0}^{q}b[k]x[n-k] - \sum_{k=1}^{p}a[k]y[n-k]](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%20%5Csum_%7Bk%3D0%7D%5E%7Bq%7Db%5Bk%5Dx%5Bn-k%5D%20-%20%5Csum_%7Bk%3D1%7D%5E%7Bp%7Da%5Bk%5Dy%5Bn-k%5D)

- Vztah rekurzivně deﬁnující výstup ze systému jako lineární kombinaci hodnot vstupu a minulých hodnot výstupu

- Konkrétní příklad:
	- ![y[n] = 3x[n] + x[n-1] -5x[n-2] -y[n -1] + y[n -2], y[-1] = 2, y[-2] = 4](https://latex.codecogs.com/svg.latex?y%5Bn%5D%20%3D%203x%5Bn%5D%20&plus;%20x%5Bn-1%5D%20-5x%5Bn-2%5D%20-y%5Bn%20-1%5D%20&plus;%20y%5Bn%20-2%5D%2C%20y%5B-1%5D%20%3D%202%2C%20y%5B-2%5D%20%3D%204)
- Rekurzivní / nerekurzivní DR
- Rekurzivní DR vyžadují počáteční podmínky

## Systémy s lineární fází

- Fázová charakteristika udává změnu fáze harmonické funkce o dané frekvenci při průchodu systémem
	- Nejsou-li všechny harmonické složky signálu zpožděné stejně,
dochází k fázovému zkreslení
- Systémy/ﬁltry, které nedeformují fázové spektrum signálu se označují jako ﬁltry se (zobecněnou) lineární fází

## Systémy s minimální fází

- Systém ![H_{min}(z)](https://latex.codecogs.com/svg.latex?H_%7Bmin%7D%28z%29) má minimální fázi, pokud má realizovatelný inverzní systém (nuly uvnitř jednotkové kružnice)
- Každý realizovatelný systém je možné převést na systém s minimální fází
- Převod ![H(z)](https://latex.codecogs.com/svg.latex?H%28z%29) na systém s minimální fází se provádí pokud:
	- Je třeba zajistit existenci inverzního systému
	- Je třeba, aby systém ![H(z)](https://latex.codecogs.com/svg.latex?H%28z%29) měl při dané magnitudové charakteristice, minimální skupinové zpoždění ![\tau g](https://latex.codecogs.com/svg.latex?%5Ctau%20g)

**Mechanismus převodu ![H(z)](https://latex.codecogs.com/svg.latex?H%28z%29) na systém s minimální fází:**

- Frekvenční charakteristiku každého realizovatelného systému je možné zapsat jako součin systému s minimální fází a realizovatelného allpass ﬁltru
	- ![H(z) = H_{min} (z) \cdot H_{ap} (z)](https://latex.codecogs.com/svg.latex?H%28z%29%20%3D%20H_%7Bmin%7D%20%28z%29%20%5Ccdot%20H_%7Bap%7D%20%28z%29)

