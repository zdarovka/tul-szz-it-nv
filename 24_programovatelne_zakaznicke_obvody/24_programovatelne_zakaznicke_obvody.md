# 24. - Programovatelné zákaznické obvody
> Rozdělení a architektury programovatelných zákaznických obvodů, jazyky pro popis technických prostředků, charakteristické rysy jazyka VHDL.

## Rozdělení a architektury programovatelných zakázkových obvodů
**ASIC** (Application Specific Integrated Circuit), nazývaný i zákaznický integrovaný obvod, je integrovaný obvod navržený a vyráběný pro určitou specifickou aplikaci. Dělíme je takto:

- **Zakázkové** (Custom) - podle uživatele se navrhují všechny masky technologického procesu
- **Polozakázkové** (Semi-custom) - podle uživatele se navrhují pouze propojovací masky
- **Programovatelné** (Programmable) - uživatel sám programuje funkci (např. přerušováním propojek)

**FPLD** (Field Programmable Logic Device) - **Programovatelné** zakázkové IO dělíme na :

- **PLD** (Programmable Logic Device)
 - *SPLD* (Simple PLD) - pevně daná struktura typu: vstup - pole AND- pole OR- výstup
 - *CPLD* (Complex PLD) - složitější architektury vycházející z SPLD (vrstevnaté, s centrální propojovací maticí).
- **FPGA** (Field Programmable Gate Array) - pravidelná struktura programovatelných log. bloků s vodorovnými či svislými propojovacími linkami a propojovacími maticemi

**Typy propojek:**

![Typy propojek](24_propojky.png)

**Nejvýznamnější výrobci FPLD:**

1. Xilinx (49 %)
2. Altera (40 %)

FPGA obvody představují přes 90 % trhu všech FPLD.

**Návrhové systémy:**

- ISE (Xilinx)
- Quartus (Altera)

## PLD
Programování na základě přepalování/porušování propojek.

![PLD](24_pld.png)

### SPLD

**PROM**

- programovatelné pole OR
- počet programovatelných bodů: N = m.(2^n) (n = počet vstupů; m = počet výstupů)
- EEPROM (Electrically Erasable PROM)
- použití jako paměť konstant

![PROM](24_prom.png)

**PAL**

- programovatelné pole AND
- počet programovatelných bodů: N = 2m.k.n
- omezený počet součinových termů k
- na výstupu mohou obsahovat klopné obvody

![PAL](24_pal.png)

**GAL**

- vychází z obvodů PAL
- na výstupu makrobuňka OLMC (Output Logic Macro Cell)
 - každý I/O lze konfigurovat jako vstup, výstup nebo třístavový výstup
 - některé z konfigurovatelných parametrů pouze globální

![GAL](24_gal.png)

**PLA**

- programovatelné pole AND i OR
- počet programovatelných bodů: N = m.k + 2k.n
- odstraňuje omezení v počtu součinových termů

![PLA](24_pla.png)

### CPLD

- složitostí mezi PLD a FPGA
- obsahují centrální propojovací matici
 - **MAPL** (Multiple Array Programmable Logic)
 - **MACH** (Macro Array CMOS High-density)
 - **PEEL** (Programmable Electrically Erasable Logic)

![CPLD](24_cpld.png)

## FPGA
Programovatelná hradlová pole (FPGA, Field Programmable Gate Array) jsou speciální číslicové integrované obvody obsahující různě složité programovatelné bloky propojené konfigurovatelnou maticí spojů.

![FPGA](24_fpga.png)

### Části obvodů FPGA
- **logické prvky (LE – logic element, LC – logic cell)**
- **programovatelné propojky (matice)**
- **I/O prvky s registry**
- globální distribuce a řízení hodinových signálů,
- JTAG rozhraní pro naprogramování a testování,
- paměti SRAM (embedded RAM)
- DSP bloky
- procesorová jádra
- PLL (fázové závěsy)
- ochrana proti kopírování
- interní oscilátor

**Look Up Table (LUT)** - blok pro implementaci kombinační logiky

- na principu SRAM
- na principu multiplexorů

![LUT](24_lut.png)

### Logická buňka
Příklad logické buňky, skládá se z konfigurovatelného LUTu a klopného obvodu.
Mnohafunkční LUT může pracovat jako:

- 16-bitový posuvný registr
- 16-bitová paměť RAM
- 4vstupový LUT

![Logická buňka](24_clb_slice_lc.png)

*Zleva: Logická buňka (LC) < Řez (Slice) < Konfigurovatelný logický blok (CLB)*

### Programovatelné propojky
PSM (Programmable Switch Matrix), propojuje vertikální a horizontální linie vodičů.

![PSM](24_psm.png)

V FPGA se nejčastěji používají programovatelné přepínače na principu:

- **SRAM** (nejčastěji z 5-6 tranzistorů);
- **antipojistky** (anti-fuses) - amorfní křemík v místě křížení dvou vodičů – nevodivá dieletrická vrstva se zvýšeným napětím prorazí (odpor 100MΩ/50Ω); PLICE (Actel), ViaLink (QuickLogic);
- **EEPROM/flash** – u FPGA v omezené míře.

### Vstupně výstupní buňky
- Zajišťují tok dat mezi vnitřní logikou a I/O piny:
  - přizpůsobují logické úrovně vně a uvnitř čipu,
  - zesilují výstupní signály,
  - podporují řadu vstupně-výstupních napěťových standardů.
- Buňky jsou rozděleny do bank, každou banku lze připojit na jiný napájecí zdroj.
- Většina buněk může být konfigurována jako vstupní, výstupní nebo obousměrné.
- Struktura buňky obsahuje většinou 3 základní signálové cesty:
  - vstupní cesta (data z pinu do vnitřní logiky),
  - výstupní cesta (přenos dat z vnitřní logiky na výstupní pin,
  - cesta ovládající třístavový výstup.
- Ve výstupní cestě je zařazen programovatelný výstupní driver:
  - umožňuje měnit rychlost přeběhu (2-3 stupně),
  - určuje výstupní proudové zatížení (2-25 mA),
  - umožňuje nastavení do stavu vysoké impedance.
- Součástí I/O buňky jsou:
  - pull-up a pull-down rezistory,
  - ochrany proti kladnému i zápornému přepětí,
  - obvody zajišťující impedanční přizpůsobení (OCT – On-Chip
  
## Jazyky pro popis technických prostředků

### Urovně abstrakce
- **Behaviouristická úroveň**
  - popis chování systému
  - volba algoritmů a architektury
  - volba mezi HW a SW realizací
- **Úroveň FB (RTL - Register Transfer Level)**
  - popis tokem dat (stavový diagram)
  - FB: logické operátory, paměti, multiplexery, čítače, …
  - nezávislá na technologickém procesu
- **Úroveň logického schématu**
  - popis spojovací tabulkou mezi logickými prvky
  - jednoznačný přechod na úroveň tranzistorů

### Formy popisu

![Formy popisu](24_popisy.png)

### Jazyky
**HDL jazyky:**

- **VHDL** (popsáno podrobněji níže)
- **Verilog HDL**
  - jednodušší a omezenější ve srovnání s VHDL
  - podobný jazyku C

*Nové jazyky vznikají zejména z důvodu dosažení větší abstrakce od hardwaru, kladou důraz na popis na úrovni algoritmů (nejsou koncipovány pro přímý popis HW - nejsou to HDL jazyky).*

**Non HDL jazyky:**

- **SystemVerilog** – standard IEEE Std 1800-2005 (vychází z Verilogu)
- **SystemC** – standard IEEE Std 1666-2005 (vychází z objektového jazyka C++)

## VHDL
**VHDL** (Very High Speed Integrated Circuits HDL) je programovací jazyk sloužící pro popis hardware. Používá se pro návrh a simulaci digitálních integrovaných obvodů, například programovatelných hradlových polí (CPLD, FPGA, …), nebo různých zákaznických obvodů (ASIC).

### Charakterizace

- všeobecně přístupný otevřený standard
- jazyk pro popis technických prostředků elektronických systémů
- vhodné pro návrh metodou shora-dolů (top-down)
- nezávislé na budoucí technologii realizace
- důraz na funkci obvodu (oproštění od detailů)
- umožňuje opakované používání modelů (knihovny)
- využití pro dokumentaci a modelování
- **paralelní jazyk** (ne sekvenční)
- libovolná část návrhu může být osamostatněna
- model VHDL může být simulován v různých systémech
- podpora testovatelnosti (Boundary Scan Architecture)
- „upovídaný“ jazyk (opakování bloků, deklarace)
- ne všechny konstrukce jazyka musí být syntetizovatelné (lze pouze simulovat)

### Styly popisu architektur

- **Behaviorální styl**
  - popis na vysoké úrovni abstrakce
  - neuvažujeme detaily (šířky sběrnic, hodinové signály)
    - použití hlavně pro simulaci
- **Styl popisující tok dat** – styl typu RTL (Register Transfer Level)
  - vhodné pro syntézu
  - návrhář si řídí architekturu svého návrhu
- **Styl strukturální**
  - vkládání komponent do netlistu (např. z knihoven)
  - omezení možností syntézy

### Základní konstrukce

**Entity a Architecture**
Základní konstrukce, které jsou povinné.

- *Entita* - „černá skříňka“ se vstupy a výstupy (obdoba grafického symbolu)
  - Entita nepopisuje chování modulů (nedefinuje funkci)
- *Architektura* - určuje chování entit
  - tělo architektury má dvě části: deklarační část (např. definice signálů), příkazová část (uzavřeno do begin - end )
  - architektura musí být spojena se specifikovanou entitou
  - rozdílné architektury definují rozdílné pohledy na entity

**Porty** (Brány)

Porty popisují vnější signály entity a jsou charakterizovány:

- jménem (libovolná skupina znaků začínající písmenem)
- datovým typem (lze spojovat porty stejného typu)
- módem (určuje směr toku dat) – 5 módů
  - *IN* – data lze z portu pouze číst
  - *OUT* – data vycházejí z portu (výstupní signál nemůže být použit jako vstup uvnitř entity)
  - *BUFFER* – výstup se zpětnou vazbou (může být buzen pouze z vnitřku entity - data mohou z entity pouze vystupovat, lze zpětně číst)
  - *INOUT* – obousměrný tok (obousměrné vstupy/výstupy)
  - *LINKAGE* – neznámý směr datového toku nebo obousměrný (návaznost na jiné než VHDL modely, např. Verilog)

**Datové objekty**

- *Constants* (konstanty) – mají neměnnou hodnotu
- *Variables* (proměnné) – používají se jako pomocné objekty (nepředstavují skutečné signály, nelze je použít jako porty, jsou lokální v procesech)
- *Signals* (signály) – většinou jsou fyzicky přítomné ve formě elektrických signálů

**Příkaz PROCESS**

- představuje nezávislý děj, který se provede při aktivaci
- užívá se zejména pro popis sekvenčních dějů
- příkazy uvnitř procesu se vykonávají sekvenčně
- více procesů v architektuře se vykonává paralelně.

```vhdl
[jméno] : PROCESS [(clock, reset)] -- seznam citlivých proměnných
-- deklarace procesu
BEGIN
-- příkazy procesu
END PROCESS [jméno] ;
```

Seznam citlivých proměnných je při syntéze ignorován, ale je významný pro správné provádění simulace

### Příklad
V následujícím příkladu je popsáno hradlo XOR v jazyce VHDL

```vhdl
-- Circuit : XOR Gate

--import std_logic from the IEEE library
library ieee;
use ieee.std_logic_1164.all;

--ENTITY DECLARATION: name, inputs, outputs
entity xorGate is	
   port( A, B : in std_logic;
            F : out std_logic);
end xorGate;

--FUNCTIONAL DESCRIPTION: how the XOR Gate works
architecture func of xorGate is 
begin
   F <= A xor B;
end func;
```
