# 14. - Databázové systémy

> Databázové systémy – relační a objektový model dat, NoSQL databáze (typy škálování, teorém CAP).

## Databázové systémy
**databáze** = organizovaná kolekce dat

**DBS** (databázový systém) = **SŘBD** (systém řízení báze dat) + **DB** (databáze; data)

**SŘBD typicky obsahuje:**
- parser - převod dotazovacího jazyka (např. SQL) do strojové podoby
- optimalizátor - optimalizace výrazu z pohledu výkonu
- operator evaluator (vyhodnocovatel výrazů)
- plan executor (vykonavatel plánů) - plán je strojová podoba příkazu, která je vyhodnocená, optimalizovaná a připravená k provedení
- lock manager - správa zámků
- transaction manager - správa transakcí

### Základní modely DBS
- Navigační databáze - hiearchický model, síťový model a grafový model
- Relační model
- Objektový model
- Dokumentový model

## Relační model dat - RMD
Založen na pevném matematickém aparátu relačních množin a predikátové logice. Databázová relace se od matematické poněkud liší. Má zavedený pomocný aparát nazvaný schéma relace. Schéma relace říká, jaký je název relace, kolik má sloupců a jaké jsou jejich názvy a domény (doména je množina přípustných hodnot pro daný sloupec). V databázích je schématem relace definice struktury tabulky. Ovšem relací nemusí být pouze tabulka, nýbrž jakákoliv struktura dělená do řádků a sloupců. Relací je například i výsledek jakéhokoliv dotazu, a podle toho s ním je možno i dále pracovat.

Relační databázový model sdružuje data do tzv. relací (tabulek), které obsahují n-tice (řádky). Tabulky (relace) tvoří základ relační databáze. Tabulka je struktura záznamů s pevně stanovenými položkami (sloupci - atributy). Každý sloupec má definován jednoznačný název, typ a rozsah, neboli doménu. Záznam se stává n-ticí (řádkem) tabulky. Pokud jsou v různých tabulkách sloupce stejného typu, pak tyto sloupce mohou vytvářet vazby mezi jednotlivými tabulkami. Tabulky se poté naplňují vlastním obsahem - konkrétními daty.

Relační model klade velký důraz na zachování integrity dat. Zavádí pojmy referenční integrita, cizí klíč, primární klíč, normální tvar apod.

Relační model dat je nezávislý na fyzickém uložení dat (Na konkrétní implementaci relační databáze).

### Základní pojmy
- **relace** - pojmenovaná tabulka s řádky a sloupci - množina n-tic (výsledek dotazu, tabulka, aj.)
- **entita** - definovaná množina dat (např. tabulka)
- **atribut** - An; pojmenovaný sloupec
- **doména atributu** - Dn; množina přípustných hodnot pro atribut
- **schema relace** - je R(An:Dn); říká nám to, jaký je název relace, kolik má sloupců a jaké jsou jejich názvy a domény = definice databázové tabulky
- **atribut relace** - je dvojice An:Dn
- **n-tice** - jsou prvky relace (řádky)
- **řád relace** - počet atributů relace
- **relační schema** - je dvojice (R,I), kde R je schema relace a I je množina integritních omezení

### Vlastnosti relace
- sloupce mohou být v libovolném pořadí,
- řádky mohou být v libovolném pořadí,
- sloupce musí být homogenní = ve sloupci musí být údaje stejného typu,
- každému sloupci musí být přiřazeno jednoznačné jméno (tzv. atribut),
- v relační tabulce nesmí být dva zcela stejné řádky

### Integrita databáze a integritní omezení
Integrita databáze znamená, že databáze vyhovuje zadaným pravidlům – integritním omezením. Tato integritní omezení jsou součástí definice databáze, a za jejich splnění zodpovídá SŘBD.

Entitní integrita
- **primární klíč** - množina atributů jednoznačně určující n-tici relace,
- **kandidáti primárního klíče** - obdoba primárního klíče, avšak kandidátů může být více,
- **klíčový atribut** - atribut, který je součástí některého klíče,
- **neklíčový atribut** - atribut, který není součástí žádného klíče,

Referenční integrita
- popisuje vztahy mezi daty ve dvou relacích,
- **cizí klíč** - atribut, kterého se týká referenční integrita (foreign key).
- **kardinalita** - vlastnost binárních vztahů která určuje kolik instancí entit vstupuje do vztahu (např. 1:1, 1:N, M:N),
- **parcialita** - vyjadřuje, zda je účast ve vztahu povinná nebo volitelná,

### Relační algebra
Pomocí základních operací (relační algebry) uskutečnit veškeré operace s daty. Aplikuje se na relace a výsledkem je opět relace.

- unární
  - selekce (výsledkem je podmnožina n-tic z relace, které splňují danou podmínku)
  - projekce (výběr sloupců)
- binární
  - sjednocení (výsledkem je relace, kde k n-ticím z R jsou přidány n-tice z S  - relace musí mít kompatibilní schéma)
  - kartézský součin (kombinace každé n-tice z R s každou n-ticí z S, podmnožinou této operace je spojené vnější/vnitřní)
  - rozdíl (výsledkem je relace, která obsahuje jenom ty n-tice z R, které nejsou v S - relace musí mít kompatibilní schéma)

## Objektový model dat - OMD
Objektová databáze je systém správy databází, ve kterém je informace reprezentována formou objektů. To by mělo přirozeněji a věrněji popisovat
skutečný svět a entity modelované v databázi. Lze je rozdělit na **objektově orientované** a **objektově relační**. Objektově orientované jsou si podobné s objekty v objektově orientovaných programovacích jazycích. Pro obě skupiny neexistuje žádný standard. V praktickém využití jej nalezneme minimálně oproti relačnímu modelu.

### Objektově orientovaný datový model
OOSŘBD využívají datového modelu, který má objektově orientované aspekty jako třídy s atributy a metodami a integritními omezeními; poskytují objektové identifikátory (OID) pro každou trvalou instanci třídy; podporují zapouzdření (encapsulation); násobnou dědičnost (multiple inheritance) a podporují abstraktní datové typy.

Kombinují prvky objektově orientovaného programování s databázovými schopnostmi. Rozšiřují funkčnost objektových programovacích jazyků (C++, Java) a poskytují plnou schopnost programování databáze. Datový model aplikace a datový model databáze se ve výsledku hodně shodují a výsledný kód se dá mnohem efektivněji udržovat. Objektově orientovaný jazyk (C++, Java) je jazykem jak pro aplikaci, tak i pro databázi. Poskytuje těsný vztah mezi objektem aplikace a uloženým objektem.

An object database stores complex data and relationships between data directly, without mapping to relational rows and columns, and this makes them suitable for applications dealing with very complex data. Objects have a many to many relationship and are accessed by the use of pointers. Pointers are linked to objects to establish relationships. Another benefit of an OODBMS is that it can be programmed with small procedural differences without affecting the entire system.
In contrast to relational database management systems (RDBMSs), where data is stored in tables with rows and columns, an object-oriented database stores complex data and relationships between data directly, without mapping to relational rows and columns.
One benefit of object-oriented databases is that, when it’s integrated with an object-oriented programming language, there is a much greater consistency between the database and the programming language. Both use the same model of representation for the data.

## Srovnání RMD a OMD
Relační model je jednoduchý a elegantní, ale je naprosto rozdílný od objektového modelu. Relační databáze nejsou navrhovány pro ukládání objektů a naprogramování rozhraní pro ukládání objektů v databázi je velmi složité. Relační databázové systémy jsou dobré pro řízení velkého množství dat, vyhledávání dat, ale poskytují nízkou podporu pro manipulaci s nimi. Jsou založeny na dvourozměrných tabulkách a vztahy mezi daty jsou vyjadřovány porovnáváním hodnot v nich uložených. Jazyky jako SQL umožňují tabulky propojit za běhu, aby vyjádřily vztah mezi daty.

Naproti tomu objektové modely jsou založeny na objektech, což jsou struktury, které kombinují daný kód a data. Objektové databázové systémy umožňují využití hostitelského objektového jazyka jako je třeba C++, Java přímo na objekty "v databázi"; tj. místo věčného přeskakování mezi jazykem aplikace (např. C) a dotazovacím jazykem (např. SQL) může programátor jednoduše používat objektový jazyk k vytváření a přístupu k metodám. Krátce řečeno, OMD jsou výborné pro manipulaci s daty. Pokud navíc opomeneme programátorskou stránku, dá se říct, že některé typy dotazů jsou efektivnější než v RMD díky dědičnosti a referencím. 

## NoSQL databáze
**NoSQL** = Not only SQL database

NoSQL je nerelační systém řízení báze dat navržený pro distribuovaná datová uložiště, nevyžadující pevné schéma databáze, nepoužívající JOIN operace a horizontálně škálující.

![](noSQL.PNG)

### Distribuovaná databáze 
Systém, který je složen z několika počítačů a softwarových komponent, které spolu komunikují pomocí počítačové sítě.

Výhody:
- spolehlivost - pokud některý uzel má výpadek, tak to neohrozí funkci celého systému,
- rozšiřitelnost - distribuovaný systém je možné snadno rozšířit přidáním nových serverů,
- sdílení zdrojů - je základní pro mnoho aplikací, data jsou sdílena v distribuovaném systému,
- flexibilita - je snadnější instalovat, implementovat a odladit nové služby,
- rychlost, výkon.

Nevýhody:
- závislost na počítačové síti,
- obecně složitější na správu,
- obecně méně bezpečné než autonomní systémy.

Typy:
- Document store (MongoDB, CouchDB)
  -  V podstate „klíč-hodnota“, ale hodnota je strukturovaná. (databáze vidí „dovnitř“, hodnota je pochopena, analyzována)
  -  Hodnota např. jako XML/JSON, nebo jako objekt. (možnost referencí na jiné záznamy, vnořování struktur, kolekce)
  -  Dotazy i složitejší, než přes klíce. (např. XPath nebo jako v objektových databázích)
- Key-value store (Redis, Aerospike)
  -  Jeden klíč, jedna hodnota, žádný duplikát. (klíč může být složený, např. z hlavní a upřesnující části, které lze použít jako ID ˇ
struktury a ID její položky)
  -  Přístup podle klíce přes hash tabulky (brutálně rychlé) ˇ
  -  Hodnota je BLOB, databáze se to ani nesnaží chápat. (zpracování obsahu „hodnoty“ je na aplikaci, databáze ji jen uchovává jako celek)
  -  Pokud nás zajímá jen část hodnoty, at’ pro dotazy, nebo pro zápis, tak je pomerně neefektivní. (lze řešit vyjmutí části pod záznam s vlastním „klíčem“, např. s upřesnující částí)
- Wide column stores (Cassandra by Facebook, Accumulo, BigTable by Google)
  -  Řádky jako v RDB, u řádku máme růuzné sloupce s hodnotami
  -  Struktura řádku není dána, každý může mát různé sloupce
- Graph store (AllegroGraph, ArangoDB)
  - Grafy = uzly, vlastnosti uzlů, hrany spojující uzly
  - Různé implementace úložište.
  - Použití pro reprezentaci sítí a jejich topologií. (např. sociální ci dopravní sítě, topologie počítačových sítí, . . . ) ˇ
  
#### Ukázka práce s MongoDB
![MongoDB](mongo.png)

### Škálování
Schopnost přidat vlastnosti, aby byly uspokojeny nové nároky uživatelů.

- **vertikální škálování** - přidání zdrojů do již existujícího systému, aby se zvýšila jeho kapacita, průchodnost atd. (např. přidat procesor, paměť, ...)
- **horizontální škálování** - přidání nových uzlů (např. nový počítač do již existující infrastruktury)

### CAP teorém
Při návrhu distribuované aplikace je nutné brát v potaz následující požadavky:
- **konzistence** (Consistency) - data musí zůstat konzistentní i po provedení operace,
- **dostupnost** (Availability) - systém musí být stále dostupný, tzn. že každý dotaz dostane odpověď, zda byl proveden úspěšně či selhal,
- **partition tolerance** - systém musí být schopen stále komunikovat, i když je komunikace mezi severy nespolehlivá.

Teoreticky není možné splnit všechny tři požadavky najednou. CAP říká, že základní požadavky na distribuované systémy musí splňovat dva ze tří požadavků. Různé NoSQL databáze tedy podporují různé kombinace C, A, P. 

- CA - data jsou konzistentní mezi všemi uzly, pokud jsou všechny uzly online. Můžeme číst/zapisovat z kteréhokoli uzlu a být si zároveň jisti, že data jsou stejná. 
- CP - data jsou konzistentní mezi všemi uzly a zachovávají partition tolerance (zamezují desychroznizaci) tím, že pokud je uzel offline data jsou nedostupná.
- AP - systém je dostupný díky replikaci, k synchronizaci dojde hned jak bude partition znovu dostupná. Nicméně není garantováno, že všechny uzly budou mít stejná data.

![CAP distribuovaná aplikace](CAP-Theorem-The-Parts.png)

![CAP distribuovaná aplikace](14_cap2.png)

## SŘBD vs. NoSQL
SŘBD
- strukturovaná a organizovaná data
- SQL, DML, DDL, ACID
- transakce, konzistence

NoSQL
- nemá deklarativní dotazovací jazyk
- nemá definované schéma
- ukládá dvojice klíč-hodnota; Uložení sloupců, dokumentů, grafů
- případná konzistence upřednostněna před ACID
- podpora nestrukturovaných a nepředvídatelných dat
- CAP teorém
- upřednostňují vysoký výkon, dostupnost a rozšiřitelnost
