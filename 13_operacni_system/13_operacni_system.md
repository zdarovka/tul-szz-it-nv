# 13. - Operační systém
> Operační systém a jeho základní úlohy – správa paměti, správa procesů, životní cyklus procesu, přidělování procesoru, správa periferií, problém uváznutí a metody jeho předcházení.

## Operační systém
Operační systém je základní programové vybavení počítače, které je zavedeno do paměti počítače při jeho startu a zůstává v činnosti až do jeho vypnutí. Skládá se z jádra (kernel) a pomocných systémových nástrojů. Hlavním úkolem operačního systému je zajistit uživateli možnost ovládat počítač, vytvořit pro procesy stabilní aplikační rozhraní (API) a přidělovat jim systémové zdroje.

![Operační systém](13_os.png)

**Požadavky na OS:**

- Rychlost
- Nenáročnost na zdroje
- Bezchybnost
- Přenositelnost
- Pořizovací a provozní náklady
- Snadnost vývoje aplikací

**Jdou bohužel proti sobě!**

### Funkce operačního systému

- **Správa programů (procesů)**
  - Zavedení do paměti, přidělení paměti, spuštění
  - Přidělování zdrojů a procesového času
  - Ukončení a uvolnění zdrojů
  - Dobré rozhraní pro programátora
  - Správa paměti
  - Přidělování operační paměti
  - Práce s úložišti
- **I/O operace**
  - Jednotný přístup k souborům a zařízením
  - Ochrana před kolizí a nekonzistencí dat
- **Manipulace se soubory**
  - Prostřednictvím souborového systému přístup k souborům v úložištích
  - Ochrana před kolizí a nekonzistencí
  - Bezpečnost přístupu
- **Komunikační služby**
  - Zajištění komunikace mezi spuštěnými programy
  - Např.: sdílení paměti nebo zasílání zpráv
- **Detekce chyb a obnova**
  - Odchycení HW chyb (nedostatek papíru v tiskárně) i SW chyb (dělení nulou)
  - Správná odpověď na každý typ chyby, programy jen předávají chybové hlášení

### Základní části operačního systému

- **Kernel (jádro)**
   - přiděluje paměť i procesorový čas
   - řídí optimální spolupráci mezi procesy
   - zodpovídá za abstrakci HW (poskytuje API - abstraktní vrstva pro lepší programování)
   - přiděluje HW aplikacím
- **Systémové nástroje**
   - Správa zařízení (formát disku, kopírování, ...)
   - Správa uživatelů
   - Pomocné nástroje - skripty, utility (pomocné programy)
- **Rozhraní**
   - API - programátorské rozhraní (standartní knihovny, přístup k hw)
   - ABI - binární rozhraní (pravidla definující spolupráci na úrovni strojového kódu mezi procesy a jádrem operačního systému, procesy a jimi používanými knihovnami nebo mezi součástmi aplikací)
   - UI - uživatelské rozhraní (nemusí být součástí, do jádra se řadí kvůli zvýšení výkonu)

### Režimy procesoru
Typicky má procesor dva režimy provozu:

- **Nechráněný – bez omezení**
   - Dostupná celá instrukční sada
   - Lze adresovat celou operační paměť
   - Lze měnit všechny registry procesoru
   - Kernel mode, unprotected mode, ...
- **Chráněný – s omezením**
   - Pokus vykonat některé instrukce končí chybou
   - Část paměti je skrytá, nelze ji adresovat
   - Pokus o změnu některých registrů končí chybou
   - User mode, protected mode, ...

**Režim je vlastnost procesoru, OS ji jen využívá. Některé procesory implementují hned několik režimů, takzvaných protection rings (nepoužívá se kvůli přenositelnosti). Přecházení mezi režimy je náročná operace, ale chrání OS před napadením nebo neúmyslným poškozením.**

### Kernel

- Pracuje v nechráněném režimu.
- Přiděluje a spravuje paměť.
- Přiděluje procesorový čas – řídí procesy.
- Ovládá HW zařízení, přiděluje HW aplikacím.
- Odpovídá za abstrakci HW.

**Typy jader**

- **„Maximální jádro“ - monolytické**
   - Všechny systémové funkce jsou zahrnuty v jádře OS.
   - Rychlé a efektivní.
   - Náročné na pamět.
   - Náchylné k chybám.
   - UNIX
- **„Minimální jádro“ - mikrojádro** (hlavně realtime OS)
   - Zajišťuje pouze abstrakci HW, správu procesů a komunikaci.
   - Zbylé funkce jsou realizovány jako procesy.
   - Pomalé, kvůli častému přepínaní režimu.
   - Malé a odolné vůči chybám.
   - Speciální větve UNIX kernelu
- **„Hybridní jádro“ - modulární**
   - Jádro „malé“ jako u mikrokernelu.
   - Služby OS jsou oddělené od jádra, ale také v prostoru jádra.
   - Teoreticky spojuje výhody obour.
   - Windows, XNU (Apple)
 
 ![Typy jader](13_jadro.png)

### Přerušení
Událost, která nastává nahodile a asynchronně vzhledem k procesorovému času, probíhajícímu výpočtu a hodinovému taktu. Při vzniku události je přerušen stávající výpočet, vyřešena událost a následně je výpočet obnoven.

Během přerušení dochází ke změně **kontextu**. Kontext je vše, co potřebujeme k obnovení výpočtu (hodnota instruction pointeru, obsah registrů, návratová adresa, ...).

**Změna IP (instruction pointeru):**

- **Skok (nedochází ke změně kontextu)**
  - podmíněný
  - nepodmíněný
- **Přerušení (dochází k zálohování kontextu)**

**Zdroje přerušení:**

- **Vnější (hardwarové)**
  - *Řadič přerušení*, obvod budí procesor a stanovuje důležitost přerušení.
  - *Maskovatelné přerušení* lze za chodu systému zakázat a ignorovat.
  - *Nemaskovatelné přerušení* nastává vždy a ignorovat jej nelze (například reset).
  - Vnější přerušení (též hardwarové přerušení) je označováno podle toho, že přichází ze vstupně-výstupních zařízení (tj. z pohledu procesoru přicházejí z vnějšku). Vstupně-výstupní zařízení tak má možnost si asynchronně vyžádat pozornost procesoru a zajistit tak svoji obsluhu ve chvíli, kdy to právě potřebuje bez ohledu na právě zpracovávanou úlohu.
  - Vnější přerušení jsou do procesoru doručována prostřednictvím řadiče přerušení, což je specializovaný obvod, který umožňuje stanovit prioritu jednotlivým přerušením, rozdělovat je mezi různé procesory a další související akce.
- **Vnitřní (procesorové)**
  - Obsloužení chyb výpočtu
  - Dáno procesorem: u „intelů“ např. dělení nulou, problémy s pamětí, chyba koprocesoru
  - Vnitřní přerušení vyvolává sám procesor, který tak signalizuje problémy při zpracování strojových instrukcí a umožňuje operačnímu systému na tyto události nejvhodnějším způsobem zareagovat. Jedná se například o pokus dělení nulou, porušení ochrany paměti, nepřítomnost matematického koprocesoru, výpadek stránky a podobně.
- **Softwarové**
  - Vyvoláno programově instrukcí pro přerušení (Intel: INT n)
  - Probíhá synchronně s taktem procesoru
  - Slouží zejména k volání služeb OS = systémová volání a přechod mezi chráněným a nechráněným režimem
  - Ve srovnání s podprogramy má pevnou adresu pro obslužnou rutinu
  - Softwarové přerušení je speciální strojová instrukce (obvykle je jich v procesoru k dispozici několik, procesory Intel mapují všechna přerušení na softwarová přerušení). Tento typ přerušení je na rozdíl od druhých dvou typů synchronní, je tedy vyvoláno zcela záměrně umístěním příslušné strojové instrukce přímo do prováděného programu. Jedná se o podobný způsob, jako vyvolání klasickému podprogramu (podprogramem je zde ISR uvnitř operačního systému), avšak procesor se může zachovat jinak. Instrukce softwarového přerušení se proto využívá pro vyvolání služeb operačního systému z běžícího procesu (tzv. systémové volání). Uživatelská úloha tak sice nemůže skočit do prostoru jádra operačního systému, ale může k tomu využít softwarové přerušení (kterých je omezené množství a vstupní body lze snadno kontrolovat). Při využití privilegovaného režimu může softwarové přerušení aktivovat privilegovaný stav.
**Obsluha přerušeni**

1. Uložení aktuálního kontextu.
2. Volitelně zákaz ostatních přerušení.
3. Do IP se načítá začátek obslužné rutiny, aktualizují se registry řídící chod výpočtu.
4. Provede se obslužná rutina.
5. Volitelně povolení ostatních přerušení.
6. Obnoví se původní výpočet s pomocí uloženého kontextu.

## Správa paměti
Soubor metod, které využívá OS při přidělování operační paměti jednotlivým procesům, které jsou v počítači spuštěny. Proces při vzniku musí mít přidělenou část paměti, a jinde pracovat nesmí. Jádro řídí přidělování paměti procesům, udržuje stav o volné/využité paměti, ochraňuje paměť
proti přepsání.

Správu paměti aplikuje operační systém ve vnitřní paměti (RAM).

### Metody správy paměti

1. **Přidělování bez dělení do bloků** - typicky pro starší systém, kde běží jen jedna úloha (bez multitaskingu), ve víceúlohových systémech se vše ukládá a vrací do OP z disku
   - Výhody: jednodušší jádro - nemusí obsahovat rutinu pro přidělení paměti
   - Ochrana paměti: nutná jen kontrola přístupu do oblasti jádra
2. **Přidělování pevných bloků pamětí (segmentace)** - po startu systému se paměť rozdělí do bloků 16kB, 32kB, ... Tyto bloky mají konstatntní velikost po celou dobu běhu systému. Procesy na základě požadavku na paměť dostanou patřičně velký blok.
   - Výhody: rychlejší přepínání kontextu - více procesů v paměti, jednoduchá správa paměti - pouze tabulka s využitím bloků
   - Nevýhoda: nelze spouštět procesy, které mají nárok větší než je největší blok, neefektivní využití paměti
3. **Dynamické přidělování paměti** - po startu systému je paměť nerozdělená, procesy po spuštění berou paměť, kolik potřebují. Při ukončení ji uvolní. Náročné na implementaci

**Memory Management Unit (MMU)** - speciální jednotka procesoru, která řeší:
  - Řízení přístupu k operační paměti
  - Řízení cache
  - Překlad logické adresy na fyzickou a zpět

**Stránkování**

- Paměť je rozdělena na stránky
- Stránka má pevnou velikost a proces může mít přidělen více stránek
- Logická adresa se pak přeloží na fyzickou adresu pomocí *tabulky stránek*
- Řeší fragmentaci
- Umožňuje lepší optimalizaci (odkládání na disk)
- Používán v moderích OS
- Aby nebylo nutné pro převod logických adres na fyzické udržovat velké množství informací, je adresní prostor rozdělen na stránky stejné velikosti (typicky 4 KiB, ale i 8 KiB nebo větší) a udržují se jen data mapování pro ně. Virtuální adresní prostor je tedy složen ze stránek, které odpovídají stejně velkým oblastem ve fyzické paměti RAM. Zatímco logické stránky vytvářejí souvislý lineární adresní prostor, umístění fyzických stránek je díky převodu zcela nahodilé. Pro běžící proces se tak vytváří iluze, že jeho adresní prostor v operační paměti je souvislý, zatímco ve skutečnosti jsou fyzické stránky fragmentovány. Fragmentace je však procesu (resp. jeho strojovým instrukcím) skryta a není ji nutné nijak řešit (na rozdíl od segmentace paměti , kde je nutné fragmentaci odstraňovat přesunem segmentů).

**Odkládání na disk** - pokud je v systému povoleno, umožňuje zapsat část paměti na disk a uvolnit tím místo v RAM. Typicky se odloží procesy, které již dlouho neběžely.

**Memory Allocator** - správa paměti, většinou v kernelu, přiděluje volné bloky dle algoritmu, optimalizace na rychlost - paměť je “levnější”.

**Fragmentace** - Důsledek dynamického přidělení paměti, po určitém čase v dynamickém přidělování se objevují náhodně volné bloky.

### Strategie přidělování

1. **Best FIT** - přidělení nejmenšího možného bloku - snaha šetřit paměť
   - Nevýhody: proces vrací malé množství pamětí. Nutné projít všechny volné bloky paměti
2. **Worst FIT** - použije se nějvětší blok, co proces nevyužije, to vrátí. Dobrá strategie, protože se vrací velké bloky dat které jsou dále použitelné, ale dlouhodobě nevýhodné, neboť velké bloky brzy dojdou Vhodné kombinovat s jinými strategiemi.
3. **First FIT** - použije se první blok (bloky jsou seřazeny), co vyhovuje, co proces nevyužije, to vrátí. Dost používaná, dobré výsledky.
   - Nevýhody: velké bloky na začátku paměti jsou rozporcovány na menší
4. **Next FIT** - přidělí se první blok, který se po posledním použitým blokem, optimalizace FirstFitu - snaha o rychlejší hledání.
   - Nevýhody - sklony k fragmentaci (měřením se ukazuje, že výrazněji, než předchozí metody)
   - Next fit is a modified version of ‘first fit’. It begins as first fit to find a free partition but when called next time it starts searching from where it left off, not from the beginning. This policy makes use of a roving pointer. The pointer roves along the memory chain to search for a next fit. This helps in, to avoid the usage of memory always from the head (beginning) of the free block chain.

## Správa procesů

### Zdroje vlastněné procesem

- **Obraz kódu programu** - kopie originálního programu načtená do paměti
- **Paměť** (typicky oblast ve virtuální paměti), která obsahuje:
  - Kód
  - Statická data
  - Halda (dynamická data)
  - Zásobník (pro volání procedur, skoky a další události)
- **Práva** - informace o vlastníkovi procesu a o oprávněních procesu
- **Kontext** - registry procesoru, fyzické paměťové adresy
  - Je-li proces vykonáván, uloženo typicky jako registry v procesoru, jinak v paměti
- **Informace o zdrojích** uložena v datových strukturách nazývaných PCB – process control blocks (přesná podoba dána OS)
- **Virtuální paměť** - „iluze“ souvislého paměťového prostoru pro procesy (ve skutečnosti různě fragmentováno a fyzicky různě implementováno)

### Process Control Block (PCB)

- Datová struktura obsahující informace o procesu
- Uložena v chráněné oblasti paměti
- Obsahuje informace jako:
  - Číslo procesu
  - Priorita
  - Vlastník
  - Oprávnění
  - Otevřené soubory
  - Spotřebovaný čas procesoru
  - Používané zdroje
  - Proměnné prostředí
  - Popis adresního prostoru procesu

### Přidělování procesoru
Aby systém fungoval jak má, je nutné, aby současně zpracovával více procesů, musí tedy docházet ke střídání činnosti, kterou realizuje procesor.

- **Nepreemtivní (kooperativní) multiprocesing** - Využívali jej starší OS, proces se musí procesorového času vzdát sám, což není optimální. Pokud by byl program naprogramován chybně, proces se nevzdá procesorového času a celý systém může zamrznou vlivem jednoho špatného vlákna.
- **Preemptivní multiprocesing** - Plánovací modul OS určije, komu přidělí procesorový čas a jaký proces pozastaví. Je to výhodnější, programátor nemusí řešit jak se budou vlákna střídat. Je ale stále nutné řešit synchronizaci prostředků, které vlákna mohou vyžívat

### Strategie rozhodování o spuštění procesů 

- **Dlouhodobá** - při pokusu o spuštění programu se posuzuje, zda bude vůbec vytvořen proces; určuje počet současně běžících procesů
- **Střednědobá** - ve všech systémech s virtuální pamětí; odklad procesů do záložní paměti; odstraňovány jsou dlouhodobě nespuštěné nebo s nízkou prioritou
- **Krátkodobá** - s časovým rámcem se vyhodnocuje, jaký proces bude běžící; řídí se i přepínání procesů při přerušení
  - **FIFO, FCFS** - first come first server; procesy se řadí ve frontě; přidělování procesoru vždy na zásobník - dlouhé odezvy; bez priorit, jednoduché
  - **SJF, SRT** - nejkratší očekávaný úsek; přednost mají kratší ůlohy nebo ty, které nevyužijí celé časové kvantum; odhad dle minulé činnosti; dobrá průchodnost nečeká se na ukončení dlouhých úloh
  - **Preemptivní plánování s prioritou** - řazení do fronty dle důležitosti; proces s nízkou důležitostí může být přerušen procesem s vyšší důležitostí; mohou i čekat pokud je více procesů s vyšší prioritou
  - **Round Robin** - cyklická obsluha; úlohy jsou cyklicky střídány; rychlá odezva; doba závisí pouze na počtu spuštěných procesů; rychlé procesy jsou dokončeny dříve než FCFS, delší dříve než SJF

### Stavy procesu

- **Běžící proces** (running) je vykonáván (má přidělen procesor).
- **Čekající proces** (waiting) čeká na přidělení procesorového času.
- **Vytvořený proces** (created) po vzniku má kopírovány do paměti zdroje ze záložních médií; následně je správcem procesů označen jako čekající.
- **Ukončený proces** (terminated) zůstává v paměti, dokud není vymazán, ale už nedostane přidělen procesor; není-li vymazán, stává se z procesu zombie.
- **Blokovaný proces** (blocked) čeká na nějaký další zdroj (vstup uživatele, čtení ze souboru). Až se dočká, převede jej správce procesů do stavu čekajícího procesu.
- Procesy, které nebyly dlouho aktivní, jsou odsunuty do záložní paměti:
  - **Odložený a čekající** (swapped and waiting)
  - **Odložený a blokovaný** (swapped and blocked)

![Stavy procesu](13_stavy_procesu.png)

### Komunikace mezi procesy

- **Sdílení paměti** (memory sharing): společný přístup do určité oblasti paměti
- **Zasílání zpráv** (messaging): asynchronní předání dat mezi odesílatelem a příjemcem; data jsou většinou kopírována k příjemci
- **Volání vzdálené procedury** (remote procedure call): program spouští proceduru, která je uložena na jiném místě, například lze volat funkci přes síť
- **Synchronizace** (synchronization): procesy se musí sejít v určitém okamžiku – synchronizační primitiva

## Správa periferií
Operační systém poskytuje **abstrakci** přístupu k hardware, ke kterému přistupuje skrze **ovladače**. Je nutné určité dělení na podobná zařízení, aby byla abstrakce možná. Autor aplikace pak pracuje se „vstupy a výstupy“, aniž by musel znát jejich konkrétní podobu. Přímou komunikaci se zařízením vždy zajišťuje kernel!

### Typy zařízení

- **Znaková (character devices):**
  - K zařízení lze přistupovat jako ke proudu (stream) znaků.
  - Narozdíl od souboru je zařízení většinou tunel, do nějž a z nějž čerpáme data.
  - Ovladač většinou podporuje systémová volání open, close, read, write.
  - Příklad: terminály v Linuxu, klávesnice, myš, tiskárna.
- **Bloková (block devices):**
  - Zařízení se jeví jako souborový systém.
  - Podporovaná volání různá dle OS. (Např. Unix jen přesouvání bloků dat, Linux podobné operace jako znaková zařízení.)
  - Rozdíl oproti znakovým zařízením zejména v rozhraní mezi zařízením a jádrem (správa dat).
  - Příklad: Magnetické disky, CD a spol., flash…
- **Síťová (network interfaces, devices):**
  - Přijímají a vysílají datové pakety.
  - Umožňují výměnu dat s jinými systémy.
  - Lze realizovat s pomocí HW (karta) nebo SW (loopback).

### Požadované vlastnosti

- **Transparentní přístup:** zařízení se pro I/O jeví jako soubory; konkrétní typ zařízení se určuje až při běhu programu. (Příklad: Tisk na různých tiskárnách.)
- **Řízení přístupu:** sdílení mezi procesy, ochrana dat, ochrana proti kolizi apod.
- **Zabezpečení:** respektuje úrovně zabezpečení v systému – různí uživatelé mají dostupná různá zařízení.
- **Flexibilita:** zařízení lze připojovat a odpojovat s minimálním zásahem do systému. (Příklad: Plug-and-play)

### Ovladače zařízení
**Ovladač obsahuje:**

1. Funkce pro komunikaci s procesy (zajištění I/O front).
2. Rutina obsluhy přerušení při komunikaci se zařízením.
3. Rutina pro inicializace zařízení (pro PnP).

**Ovladače dělíme na:**

- **Producent**
  - Logická vrstva směrem k OS.
  - Přebírá data od procesů a řadí je do fronty.
  - Závislá jen na typu zařízení, ale ne na HW.
  - Může být obecná pro více zařízení („klávesnice“, „tiskárna“ apod.).
- **Konzument**
  - Fyzická vrstva směrem k zařízení (přímá komunikace se zařízením)
  - Odbavuje frontu směrem k zařízení.
  - Závislé na typu HW.

**Ovladač obstarává:**

- **Inicializace:**
  - Slouží k zavedení zařízení do OS.
  - Používá se při startu OS, při zapnutí zařízení nebo při aktualizaci jeho nastavení.
- **Připoj zařízení:**
  - Pro zařízení typu plug and play.
- **Ovládání zařízení:**
  - Zápis a čtení dat, jiné I/O operace, vlastní práce zařízení.
- **Start I/O:**
  - Slouží k zahájení (a ukončení) přenosu dat do a ze zařízení.
- **Obsluha přerušení:**
  - Používá se, pokud zařízení pracuje v přerušení.
- **Zrušení operace:**
  - Obnova při zrušení I/O operace z libovolného důvodu.
- **Rychlý průchod:**
  - Umožní realizovat I/O rychleji něž při komunikaci se zařízením - např. čtením souboru z cache namísto z disku.
- **Oznámení o vypnutí:**
  - Při oznámení vypnutí systému se může řadič korektně ukončit.
- **Záznam chyb:**
  - Zaznamenává chyby a může o nich informovat I/O subsystém.

![Ovladače zařízení](13_ovladace_zarizeni.png)

## Uváznutí
Procesy se vzájemně blokují: A má zamčen zdroj ZA, B má zamčen zdroj ZB. A nebude pokračovat, dokud nebude volné ZB, B nebude pokračovat, dokud nebude volné ZA. Systém se zastaví. Bez zásahu shora nelze řešit.

![Uváznutí](13_uvaznuti.png)

**K uváznutí může dojít v systému, kde jsou současně splněny tyto čtyři podmínky (Coffman, 1971):**

- je možný výlučný přístup k některým zdrojům
- prostředky jsou přidělovány postupně, proces může držet prostředky a čekat na další
- nelze násilím odebrat přidělený prostředek
- může vzniknout kruh procesů, které na sebe vzájemně čekají.

**Prevence** = při návrhu systému
- Systém navrhujeme tak, aby uváznutí nemohlo vzniknout.
- V principu se snažíme navrhnout takový systém, v němž neplatí alespoň jedna z výše citovaných podmínek.
 
**Předcházení** = za běhu
- Systém z principu uváznutí umožňuje.
- Za chodu vyhodnocujeme požadavky na zdroje a rozhodujeme, zda požadavku vyhovíme .
- „Hračky přiděluje rodič a přemýšlí při tom“.

### Předcházení souběhu
**Podmínka č. 1: Odstraníme výlučný přístup.**

- Virtualizace prostředků – procesy pracují s „náhražkou“ skutečného zdroje (soubor místo tiskárny).
- Spooling (simultaneous peripherial output online) – proces nepracuje přímo se zařízením, ale s předřazenou frontou (tiskárny, disky).

**Podmínka č. 2: Nedovolíme držet neomezeně zdroj.**

- Žádá se jen jednou: proces dostane buď vše, nebo nic (když nemůžu dát procesu autíčko a kočárek zároveň, nedám mu nic a nechám jej čekat).
- Nevýhoda: Nízká efektivita nakládání zdroji (procesy jsou raději hamouni, ať mají jistotu).
- Alternativa: prostředky jen tomu, kdo zrovna nemá nic (nikdo nemá právo požadovat další hračku, když už nějakou má).
- Nevýhoda: Hladovění - proces může dlouho čekat na všechny své zdroje.

**Podmínka č. 3: Povolíme zásah shora.**

- Odebírat by mělo jen jádro, ne procesy sobě navzájem; jinak může vést k chaosu.
- Nutná obnovitelnost, musí se obnovit původní stav zdroje – lze např. pro procesor nebo operační paměť.
- Systém v roli rodiče - rozhodne na základě znalosti souvislostí a s předcházením nejhorším situacím, že musí být vydáno autíčko či kočárek.

**Podmínka č. 4: Roztrhneme kruh čekání.**

- Všechny zdroje se číslují.
- Prostředky číslovány, proces např. nesmí žádat o prostředky s nižším číslem, než je jeho první přidělený prostředek.
- Zdroje jednoho typu musejí být požadovány najednou.
- Znovu je zde systém v roli rodiče: „Už sis vzal autíčko, dokud je nevrátíš, nemáš právo žádat o kočárek.“

### Další možnosti jak řešit uváznutí
**Ignorování („pštrosí algoritmus – hlava v písku“):**

- Systém uváznutí vůbec neřeší.
- Při uváznutí zásah vyšší moci: uživatel vypne procesy.

**Vyhýbání se konfliktu („bankéřův algoritmus“)**

- Systém zná nároky procesů; před přidělením kritického zdroje se zjišťuje, zda je možné pokračovat i v případě, že proces zdroj zabere – vyhodnocuje se možnost ukončení ostatních procesů.
- Bankéřův? Bankéř má vždy méně peněz, než kolik má sjednaných úvěrů, on prostě předpokládá, že klienti nebudou chtít všichni současně všechny peníze.

**Vyhodnocení bezpečného/nebezpečného stavu**

- Průběžně vyhodnocujeme, co je již alokováno a zda nehrozí cyklus.
- Nepovolíme požadavky, které by vedly k uváznutí.
- Nutná schopnost detekce uváznutí a vyhodnocení stavu systému.
- V případě uváznutí prostě procesy zabijeme všechny nebo jeden náhodný a otestujeme znovu.
