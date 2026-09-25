[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace

$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle

- **Kategorizovat a porovnat** architektury řídicích systémů (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé) podle výkonu, paměti, determinismu a spolehlivosti.
- **Analyzovat provozní prostředí a vnější vlivy** (krytí IP, teplotní rozsah, EMC rušení, vibrace) a stanovit požadavky na mechanickou a elektrickou odolnost hardware.
- **Sestavit I/O bilanci** a navrhnout optimální řídicí jednotku z reálných katalogů výrobců pro konkrétní průmyslovou či IoT aplikaci včetně projektové rezervy.
- **Vypracovat vícekriteriální rozhodovací matici** a obhájit zvolenou platformu z technického a ekonomického hlediska (pořizovací cena, náročnost vývoje, údržba a spolehlivost).
- **Provést kritický technický audit (troubleshooting)** nevhodného návrhu řízení, identifikovat bezpečnostní a provozní rizika a navrhnout certifikované řešení v souladu s průmyslovými standardy.

## Ověření cílů

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)

<!--
1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů. 
2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód. 
3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC). 
4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek. 
5. Kritická technická oponentura (audit) nevhodně navrženého řešení. 
-->


---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní orientační úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem          | Co zkratka znamená (česky / anglicky) | Základní charakteristika (architektura, kde běží program)                                            | Typický zástupce (konkrétní rodina / model) | Příklad reálného nasazení                |
| :----------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------------- | :------------------------------------------ | :--------------------------------------- |
| **MCU**                  | Mikrokontrolér / Microcontroller Unit                                      | Integrovaný čip (CPU + RAM + Flash na jednom substrátu), deterministický běh bez OS nebo RTOS        | např. ESP32, PIC16LF1xxx, RP2040            | Chytrá domácnost (čidla, termostaty), nositelná elektronika, elektronické hračky                                         |
| **MPU**                  | Mikroprocesorová jednotka / Microprocessor Unit                                      | Samostatný procesor vyžadující externí RAM a úložiště, zpravidla běží plnohodnotný OS (Linux)        |                                             |Raspberry Pi (Broadcom BCM2711), NXP i.MX, STM32MP1|
| **Embedded**             |Vestavěný (vnořený) systém / Embedded System|Účelově zaměřený počítačový systém (MCU/MPU/x86) vestavěný do většího zařízení, který řídí jeho specifické funkce.| Embedded PLC, Embedded PC                   | Bílá technika, bankomaty, regulace kotlů |
| **PLC**                  |Programovatelný logický automat / Programmable Logic Controller| Průmyslový automat pro cyklické deterministické řízení procesů, vysoká odolnost, modulární/kompaktní |Siemens LOGO! / S7-1200, Beckhoff, Schneider Modicon, Allen-Bradley|Řízení výrobních linek, robotických pracovišť, čističek odpadních vod, automatizace budov.|
| **iPC**                  |Průmyslový počítač / Industrial PC|Odolné PC (architektura x86/ARM) pro náročné průmyslové prostředí, běží na něm plnohodnotný OS (Windows, Linux), delší bootování.|Beckhoff C60xx, Advantech UNO, Siemens Simatic IPC|Vizualizace procesů (SCADA), počítačové vidění pro kontrolu kvality, řízení celých továren.|
| **Programovatelné relé** |Programovatelné relé / Smart Relay / Micro PLC| Zjednodušené kompaktní PLC pro méně náročné úlohy, nahrazuje časovací relé a stykačové kombinace|Siemens LOGO!, Eaton EasyE4, Schneider Zelio Logic|Řízení osvětlení, zavlažování, řízení posuvných bran, jednoduchá čerpadla.|

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Integrovaný obvod sdružující všechny klíčové elektronické obvody a komponenty celého počítače či elektronického systému na jediném křemíkovém čipu. 
> 	 Systém na čipu. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-06-07 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu
> - **DSP (Digital Signal Processor):** Specializovaný mikroprocesor architektury Harvard optimalizovaný pro matematické výpočty v reálném čase (rychlá Fourierova transformace FFT, filtrace šumu, digitální vektorové řízení střídavých motorů). 
> 	Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [Digitální signálový procesor – Wikipedie](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)
> - **FPGA (Field-Programmable Gate Array):** Programovatelné logické hradlové pole, jehož vnitřní struktura logických bloků a propojení je konfigurovatelná až u zákazníka. Umožňuje masivní paralelní zpracování s hardwarovou latencí v řádu nanosekund. 
> 	Programovatelné hradlové pole. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-01-10 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole


<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Zaměřte se na čas náběhu a architekturu: U MCU je kód ve vnitřní paměti Flash procesoru a vykonává se okamžitě po přivedení napájení (řádově milisekundy). U systémů s MPU a iPC musí BIOS/bootloader nejprve zavést jádro operačního systému (OS Linux, Windows) z disku/eMMC/SD karty do operační paměti RAM, což trvá desítky sekund.</p>
</details>

:star2: **Bonusová otázka k úloze 1:**
Proč se u kritických aplikací v letectví (např. systém řízení letu Fly-by-Wire) nebo v jaderné energetice stále upřednostňují jednoduché deterministické mikrořadiče s několika desítkami kilobajtů paměti nebo obvody FPGA před moderními vícejádrovými gigahertzovými procesory s gigabajty RAM?

*Vaše odpověď:*
`V kritických aplikacích se tyto obvody používají proto, že jsou 100% předvídatelné, matematicky plně otestovatelné a po výpadku se restartují během několika milisekund, zatímco u složitých GHz procesorů s operačním systémem nelze zaručit absolutní bezchybnost ani okamžitý náběh.`

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)

*Časová dotace: max. 15 minut | Mírně náročnější úloha propojující parametry a praxi*

1. **Typy pamětí v řídicích jednotkách:**
   - Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     - **RAM:** 
	     - Je volatilní (energeticky závislá)? `Ano`
	     - Rychlost zápisu: `Extrémně vysoká (v řádu nanosekund)` 
	     - K čemu se využívá v PLC/MCU: `Ukládání mezipaměti, pracovních proměnných, zásobník (stack) a běh programu za chodu.`
     - **Flash (ROM):** 
	     - Je volatilní? `Ne`
	     - K čemu se využívá v PLC/MCU: `Ukládání samotného řídicího programu (firmware), konstanta a konfiguračních dat, které musí zůstat zachovány i po vypnutí napájení.`
     - **EEPROM / NVRAM:** 
	     - Je volatilní? ` Ne`
	     - K čemu se využívá v PLC/MCU: `Ukládání provozních parametrů, kalibračních dat, čítačů a nastavení, které se mění za provozu a nesmí se při výpadku napájení ztratit.`
   - *Otázka z praxe:* Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
     - Odpověď: `Do remanentní paměti (NVRAM / EEPROM nebo do RAM zálohované superkondenzátorem / baterií).`

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**
   - Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?
     - Odpověď: `Protože PLC/RTOS garantuje Hard Real-Time (striktní determinismus) – reakce proběhne vždy do 5 ms. Standardní Linux je systém Soft Real-Time bez garantované doby odezvy; plánovač úloh (scheduler) může reakci zpozdit kvůli jinému procesu na pozadí, což by u lisu mohlo způsobit havárii či zranění.`

3. **Odolnost vůči vlivům prostředí a dešifrování kódu IP:**
   - Dešifrujte kód **IP68**:
     - První číslice (6): `Úplná prachotěsnost (ochrana před nebezpečným dotykem pomůckou a před vniknutím prachu)`
     - Druhá číslice (8): `Trvalé ponoření do vody pod tlakem (za podmínek specifikovaných výrobcem)`
   - Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?
     - Označte správnou volbu: `[ ] IP20` | `[ ] IP44` | `[X] IP65` | `[ ] IP00`
     - Zdůvodnění: `První číslice 6 zajišťuje úplnou prachotěsnost proti polétavému prachu a druhá číslice 5 chrání před tryskající vodou z jakéhokoli úhlu při přímém dešti.`

4. **Konstrukční rozdíly kancelářského PC vs. průmyslového iPC:**
   - Vyberte a doplňte hlavní odlišnosti:
     - *Chlazení:* 
	     - Kancelářské PC: `Aktivní (ventilátory, které nasávají prach)` 
	     - vs. iPC: `Pasivní (bezventilátorové / fanless, chlazení masivním hliníkovým tělem/žebrováním).`
     - *Napájecí napětí a filtrace:* 
	     - Kancelářské PC: `Standardní AC 230 V (běžný zdroj, nízká odolnost vůči výpadkům a přepětí)` 
	     - vs. iPC: `Průmyslové DC 24 V (široký rozsah napájení, galvazniká izolace, integrovaná přepěťová filtrace)`
     - *Odolnost proti otřesům a vibracím:* `Vysoká (použití celokovového šasi, SSD/eMMC namísto mechanických HDD a konektorů se šroubovacími pojistkami)`
     - *Způsob montáže:* 
	     - Kancelářské PC: na stůl/pod stůl 
	     - vs. iPC: `Na DIN lištu (TS35) nebo do 19" rozvaděče (rack) / VESA držák.`

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Determinismus (Real-Time):** Vlastnost systému, která zaručuje, že odezva na vstupní událost proběhne vždy v přesně definovaném a předvídatelném čase (deadline). V *Hard Real-Time* systémech znamená nedodržení časového limitu fatální havárii celého procesu. 
> 	Operační systém reálného času. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-05-12 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Opera%C4%8Dn%C3%AD_syst%C3%A9m_re%C3%A1ln%C3%A9ho_%C4%8Dasu
> - **Krytí IP (Ingress Protection):** Mezinárodní standard dle normy **ČSN EN 60529** určující stupeň ochrany krytem před vniknutím pevných cizích těles včetně prachu (1. číslice 0–6) a vniknutím vody (2. číslice 0–9K).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 60529 (33 0330) Stupně ochrany krytem (krytí - IP kód)*. Praha: Český normalizační institut, 1993. Třídící znak 330330.
> - **Remanentní paměť (Retain):** Paměťový prostor v PLC, jehož obsah zůstává zachován i po přerušení napájecího napětí (využívá zálohovací baterii, superkondenzátor nebo zápis do FRAM/MRAM/EEPROM).

<details>
<summary> :bulb: Tip k otázce determinismu: </summary>
<p>Běžný Linux je <b>preemptivní víceúlohový systém</b>, který se snaží spravedlivě rozdělit čas procesoru mezi stovky procesů. Může se stát, že kvůli obsluze disku, správě paměti nebo síťovému provozu se proces řízení pozdrží na desítky milisekund. PLC naproti tomu vykonává cyklus v pevném taktu bez zpoždění vyvolaného aplikacemi na pozadí.</p>
</details>

:star2: **Bonusová otázka k úloze 2:**
Co označuje doplňkové písmeno **K** v kódu krytí **IP69K** a v jakém průmyslovém odvětví je toto krytí bezpodmínečně vyžadováno?

*Vaše odpověď:*
`Písmeno K označuje ochranu proti vysokotlakému a vysokoteplotnímu ostřiku vodou (čištění tlakovou vodou / wapkou, např. 100 bar při 80 °C). Bezpodmínečně se vyžaduje v potravinářském průmyslu, farmaceutickém průmyslu a u zemědělské/stavební techniky z důvodu přísných hygienických nároků a pravidelného dezinfekčního mytí.`

---

### 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC) 

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v pozici nezávislého konzultanta automatizace. Tři různí zákazníci požadují navrhnout optimální kategorii řízení.

#### Příklad aplikace (vzorové řešení):
- **Vzorová aplikace 0 – Automatická vjezdová závora na parkoviště:** Jednoduchý jednoúčelový systém s indukční detekční smyčkou vozidla, bezpečnostní optozávorou, koncovými spínači polohy ramene, motorem závory (vpřed/vzad) a výstražným semaforem (červená/zelená). Požadavek na jednoduchou správu správcem objektu a spolehlivý chod v rozváděči u vjezdu.

#### Popis zadaných aplikací pro studenty:
1. **Aplikace A – Chytrý pokojový termostat (IoT):** Bateriově napájený přístroj měřící teplotu a vlhkost v místnosti, zobrazující údaje na e-ink displeji a odesílající data přes protokol ZigBee/Wi-Fi do domácí brány. Plánovaná sériová výroba: 10 000 kusů ročně.
2. **Aplikace B – Automatická balicí linka:** Průmyslová linka ve výrobní hale. Obsahuje 28 optických snímačů, 14 pneumatických válců, 3 dopravníkové pásy s asynchronními motory a bezpečnostní světelnou závoru. Vyžaduje se nepřetržitý provoz 24/7 a snadná údržba podnikovým elektrikářem.
3. **Aplikace C – Kontrolní stanice optické jakosti svarů:** Pracoviště se 2 vysokorychlostními průmyslovými GigE kamerami snímajícími svary na karoserii automobilu. Snímky v rozlišení 4K jsou analyzovány neuronovou sítí v reálném čase, vady jsou označeny a ukládány do podnikové relační databáze (SQL / MES).

#### Váš úkol:
Vyplňte rozhodovací matici. Jako vzor poslouží vyplněný sloupec pro **Vzorovou aplikaci 0**. Přiřaďte každé aplikaci nejvhodnější platformu (**MCU / Embedded SoC**, **Kompaktní/modulární PLC**, **Průmyslové PC – iPC**) a doplňte multikriteriální posouzení:

| Kritérium hodnocení                                                                                   | **Vzorová aplikace 0 (Vjezdová závora - VZOR)**                                                                                                                                                                           | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :---------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------ | :------------------------ | :----------------------------------- |
| **Doporučená platforma** *(MCU / PLC / iPC)*                                                          | **Programovatelné relé / kompaktní PLC** *(např. Siemens LOGO!, Eaton easyE4)*                                                                                                                                            | `MCU / Embedded Soc`                           | `Kompaktní/modulární PLC`                     | `Průmyslové PC - iPC`                                |
| **Pořizovací cena HW na 1 kus** *(nízká < 500 Kč / střední 5–30 tis. Kč / vysoká > 50 tis. Kč)*       | **Střední** *(cca 3 500 – 6 000 Kč)*                                                                                                                                                                                      | `Nízká (cca 100–300 Kč za komponenty a čip)`                           | `Střední (cca 15 000 – 40 000 Kč dle I/O modulů)`                     | `Vysoká (> 50 000 Kč, často 70 000 – 150 000+ Kč včetně akcelerační karty)`                                |
| **Primární programovací jazyk** *(C/C++/MicroPython vs. IEC 61131-3 ST/LAD vs. Python/C#/C++ pod OS)* | **FBD / LAD** *(grafické funkční bloky nebo liniové schéma dle IEC 61131-3)*                                                                                                                                              | `C/C++/MicroPython`                           | `IEC 61131-3 ST/LAD`                     | `Python/C#/C++ pod OS`                                |
| **Klíčový technický argument pro volbu** *(např. spotřeba, determinismus, grafický výkon)*            | Montáž přímo na DIN lištu v rozváděči, integrovaný displej pro nastavení časovačů přímo na místě, robustní reléové výstupy pro motor a semafor, napájení 24 V DC / 230 V AC bez nutnosti vývoje vlastního plošného spoje. | `Nízká spotřeba energie pro provoz z baterie, nízké jednotkové náklady při sérii 10 000 ks/rok, integrované bezdrátové rozhraní (ZigBee/Wi-Fi)`                           | `Vysoký determinismus reálného času, průmyslová odolnost (EMC, vibrace), snadná diagnostika a údržba podnikovým elektrikářem`                     | `Obrovský výpočetní a grafický výkon pro běh neuronové sítě v reálném čase nad 4K obrazem, přímé ukládání do SQL/MES databází`                                |
| **Hlavní riziko při volbě špatné platformy** *(proč by neuspěly ostatní dvě varianty)*                | **MCU:** Nutnost vývoje vlastní desky, nízká odolnost vůči venkovnímu rušení a obtížný servis údržbou.<br>**iPC:** Zbytečně extrémní cena (> 30 tis. Kč), dlouhý start po výpadku napájení a vysoká spotřeba.             | `Kompaktní/modulární PLC / Průmyslové PC – iPC: Nerealizovatelné pro bateriové napájení (vysoká spotřeba), neekonomické kvůli vysoké pořizovací ceně při masové sérii 10 000 ks/rok.`                           | `MCU / Embedded SoC: Vysoké riziko rušení, drahý vývoj vlastního HW, náročný servis bez znalosti C++/Pythonu`                     | `MCU / Embedded SoC / Kompaktní/modulární PLC: Absolutně nedostatečný výpočetní výkon a RAM pro maticové operace neuronových sítí a zpracování 4K videa v reálném čase.`                                |

**Multikriteriální posouzení**:
 
 **Ekonomika sériovosti a pořizovací náklady (HW & Vývoj)**

Aplikace A (Termostat – 10 000 ks/rok): Při sériové výrobě 10 000 kusů ročně je klíčové minimalizovat jednotkovou cenu hardwaru. Použití MCU / Embedded SoC sice vyžaduje vysoké jednorázové náklady na vývoj tištěného spoje (PCB) a certifikaci, ale tyto náklady se rozpočítají do velké série. Jednotkový HW stojí pouze stovky Kč. Nasazení PLC nebo iPC by znamenalo neakceptovatelné náklady v řádu tisíců až desítek tisíc Kč na jeden kus.   

Aplikace B (Balicí linka – Jednotková/kusová výroba): Výroba jedné nebo několika málo linek neospravedlňuje vývoj vlastního elektronického obvodu (MCU). Vyplatí se koupit hotové Kompaktní/modulární PLC za střední cenu (desítky tisíc Kč), které má již hotové certifikace, průmyslové krytí a konektory.   

Aplikace C (Kontrola svarů – Jednotková/kusová výroba): Vysoká pořizovací cena iPC (přes 50 000 Kč) je plně akceptovatelná, protože jde o specializované pracoviště s vysokou přidanou hodnotou. Náklady na iPC tvoří jen malou část celkové ceny kamerového systému a výrobní linky.   

 **Energetická náročnost a napájení**
  
   Aplikace A: Vyžaduje bateriové napájení. MCU / Embedded SoC je jediná možnost, protože nabízí extrémně nízkou spotřebu v režimu spánku (v řádu $\mu\text{A}$). PLC i iPC mají příkon v řádu wattů až stovek wattů a z baterie by fungovaly pouze několik hodin.

   Aplikace B a C: Obě zařízení jsou trvale napájena z průmyslové sítě (24 V DC / 230 V AC v rozváděči), takže spotřeba energie není omezujícím kritériem.   

 **Výpočetní výkon, typ dat a konektivita**
   
   Aplikace A: Zpracovává pouze jednoduchá skalární data (teplota, vlhkost) a odesílá malé datové pakety přes ZigBee/Wi-Fi. Výkon MCU je pro tento účel plně dostačující.

   Aplikace B: Vyžaduje rychlé zpracování logických signálů z 28 optických snímačů a spínání 14 pneumatických válců a 3 motorů. Řídicí logika je diskrétní (I/O signály). PLC poskytuje potřebný reakční čas v řádu milisekund.

   Aplikace C: Vyžaduje masivní paralelizaci výpočtů pro zpracování obrazového toku v rozlišení 4K ze 2 GigE kamer a běh neuronové sítě v reálném čase. iPC disponuje potřebným výpočetním výkonem CPU/GPU, operační pamětí RAM a přímou konektivitou pro ukládání dat do podnikové databáze (SQL/MES). MCU ani PLC nemají pro maticové operace AI a zpracování 4K videa dostatečnou paměť ani výpočetní kapacitu.   

 **Provozní spolehlivost, provoz 24/7 a servisní náročnost**

   Aplikace A: Zařízení je určeno pro běžného spotřebitele/domácnost.

   Aplikace B: Vyžaduje nepřetržitý provoz 24/7 a snadnou údržbu podnikovým elektrikářem. Kompaktní/modulární PLC nabízí vysokou průmyslovou odolnost (EMC rušení, vibrace, teploty). V případě poruchy může elektrikář modul snadno vyměnit a diagnostikovat chybu v normovaném jazyce IEC 61131-3 (LAD/FBD), aniž by musel znát programovací jazyky C++ nebo Python.

   Aplikace C: Odolnost iPC je zajištěna průmyslovým provedením (bezvětrákové chlazení, SSD disky, odolnost vůči vibracím). Servis a úpravy algoritmu AI však vyžadují specializovaného IT/software inženýra.

**Vysvětlivky**: 

**EMC** = elektromagnetická kompatibilita (Jedná se o schopnost elektrického nebo elektronického zařízení fungovat správně v prostředí, kde působí elektromagnetické rušení, aniž by současně sama způsobil nepřípustné rušení jiných zařízení v okolí.) 

**SQL** = označuje relační databázi, která ukládá data do strukturovaných tabulek s jasně definovanou relací (vztahy) mezi nimi. K čemu slouží v průmyslu: Ukládají se do ní strukturovaná historická data, záznamy o vadách, metriky kvality, časová razítka nebo parametry výroby. Typické příklady: Microsoft SQL Server, PostgreSQL, MySQL, Oracle.
Přímé ukládání znamená: Systém nepotřebuje žádný další mezičlánek ani ruční export – naměřená nebo vyhodnocená data ze 4K obrazu zapsat přímo pomocí dotazů SQL do centrální databáze.

**MES** = je zkratka pro Manufacturing Execution System (výrobní informační systém). K čemu slouží v průmyslu: MES propojuje řízení výroby na dílně (PLC, kamery, senzory) s nadřazenými podnikovými systémy (ERP, např. SAP). Sleduje celý výrobní proces od surovin až po hotový výrobek v reálném čase. Co MES spravuje: Sledovatelnost (Traceability): Přesný záznam, který kus byl vyroben kdy, z jakých dílů a s jakým výsledkem kontroly.
Řízení jakosti: Automatické zastavení linky při detekci sériové vady. OEE (Celková efektivita zařízení): Sledování dostupnosti, výkonu a kvality linky.
Přímé ukládání znamená: Výsledky z neuronové sítě se okamžitě propisují k danému výrobnímu příkazu nebo kódovému štítku (SN/DataMatrix) konkrétního výrobku v MES systému.

> **Kritéria hodnocení úlohy 3 (bodování a známka):**
> - :star: **Správnost technického přiřazení platforem (30 %):** Stoprocentně logické a obhajitelné přiřazení všech 3 technologií.
> - :star: **Inženýrská a ekonomická argumentace (40 %):** Zohlednění ekonomiky sériovosti (kusová vs. masová výroba), spotřeby energie, náročnosti vývoje a schopností servisního personálu.
> - :star: **Analýza rizik nevhodné platformy (30 %):** Věcné zdůvodnění, proč je v daném případě jiná platforma neefektivní, příliš drahá nebo neschopná úlohu odbavit.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Norma ČSN EN 61131-3:** Mezinárodní standard pro programovací jazyky PLC automatů. Definuje dva textové jazyky (ST – strukturovaný text, IL – seznam instrukcí) a tři grafické jazyky (LD – příčkový diagram / kontaktní schéma, FBD – funkční blokové schéma, SFC – sekvenční funkční schéma).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 61131-3 ed. 3 (18 0080) Programovatelné řídicí jednotky - Část 3: Programovací jazyky*. Praha: Úřad pro technickou normalizaci, metrologii a státní zkušebnictví, 2014. Třídící znak 180080.
> - **GigE Vision:** Komunikační standard rozhraní pro průmyslové kamery využívající gigabitový Ethernet, umožňující přenos nekomprimovaného videa vysokou rychlostí na velké vzdálenosti.

<details>
<summary> :bulb: Tip pro Aplikaci A vs. B vs. C: </summary>
<p>U aplikace A rozhoduje kusová cena a odběr proudu z baterie (PLC ani iPC z baterie nerozběhnete). U aplikace B potřebujete vyměnitelný modul na DIN lištu s diagnostickými LED, který přeprogramuje běžný údržbář v jazyce LAD. U aplikace C potřebujete obrovský výpočetní výkon pro AI a ovladače pro průmyslové kamery, což MCU ani běžné PLC nezvládne.</p>
</details>

:star2: **Bonusová otázka k úloze 3:**
Co je to tzv. **SoftPLC** a jak umožňuje průmyslovému PC (iPC) kombinovat výhody operačního systému Windows/Linux a deterministického řízení reálného času v jediném fyzickém počítači?

*Vaše odpověď:*
`SoftPLC je software (např. TwinCAT nebo CODESYS), který z obyčejného průmyslového PC (iPC) udělá plnohodnotné PLC.` 

`Jak to funguje v jednom iPC:Rozdělení procesoru: Tzv. Real-Time Hypervizor si vyhradí část jader procesoru a paměti RAM výhradně pro řízení stroje (SoftPLC). Zbytek jader nechá pro běžný operační systém (Windows/Linux).`   

`Deterministické řízení: SoftPLC část běží se 100% předností. Zaručuje okamžitou reakci v milisekundách na vstupy a výstupy, i kdyby byl operační systém pod kapotou zrovna maximálně vytížený.`   

`Nezávislost při pádu: Pokud Windows/Linux zamrzne nebo spadne, SoftPLC část na vyhrazeném jádře běží dál a stroj bezpečně řídí nebo odstaví.`

`Hlavní výhoda: Získáte rychlost a spolehlivost klasického PLC i výkon PC pro AI, kamery a databáze v jediné krabici.`

---

### 4. Návrh a konfigurace řídicí jednotky pro čerpací stanici

*Časová dotace: 25–30 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v roli projektanta automatizace. Zákazník poptává zhotovení řízení pro obecní přečerpávací stanici odpadních vod.

#### Zadání technologického procesu a periferií:
- **Snímače a vstupy:**
  - 3× plovákový hladinový spínač (havarijní spodní hladina proti chodu nasucho, zapínací hladina, havarijní přepad) – bezpotenciálový kontakt spínající 24 V DC.
  - 1× hydrostatická ponorná sonda výšky hladiny v jímce – výstupní signál 4–20 mA.
  - 1× termistorové ochranné relé přehřátí motoru čerpadla – poruchový kontakt 24 V DC.
- **Akční členy a výstupy:**
  - 2× stykač pro spouštění motorů hlavního a záložního čerpadla – spínání cívky stykače 230 V AC / 0,5 A.
  - 1× opticko-akustický výstražný maják – napájení 24 V DC / 0,3 A.
  - 1× řízení otáček frekvenčního měniče hlavního čerpadla – analogový signál 0–10 V.
- **Komunikace a přenos dat:**
  - Odesílání údajů o hladině a poruchách na dispečink vodáren (Ethernet / Modbus TCP nebo GSM/LTE modul).
- **Provozní podmínky:**
  - Venkovní nekrytý terén, rozváděč vystavený dešti, prachu a teplotám v rozmezí **-20 °C až +45 °C**.

#### Váš úkol:

1. **Sestavte tabulku I/O bilance** a spočtěte celkový počet signálů. Připočtěte rezervu min. 20 % pro budoucí rozšíření:

| Typ signálu | Požadavek aplikace (kusy) | Popis signálů v aplikaci | Počet po započtení rezervy (+20 %) |
| :--- | :--- | :--- | :--- |
| **Digitální vstup (DI)** | `4` | `3× plovákový spínač (chod nasucho, zapínání, přepad), 1× termistorové relé čerpadla` | `5 (4 × 1,2 = 4,8 zaokrouhleno nahoru)` |
| **Digitální výstup (DO) – reléový** | `2` | `2× cívka stykače motorů hlavního a záložního čerpadla (230 V AC / 0,5 A) (Doporučeno spínat přes pomocná mezilehlá relé)` | `3 (2 × 1,2 = 2,4 zaokrouhleno nahoru)` |
| **Digitální výstup (DO) – tranzistorový** | `1` | `1× opticko-akustický maják (24 V DC / 0,3 A)` | `2 (1 × 1,2 = 1,2 zaokrouhleno nahoru)` |
| **Analogový vstup (AI)** | `1` | `1× hydrostatická sonda výšky hladiny (4–20 mA)` | `2 (1 × 1,2 = 1,2$ zaokrouhleno nahoru)` |
| **Analogový výstup (AO)** | `1` | `1× řízení otáček frekvenčního měniče hlavního čerpadla (0–10 V)` | `2 (1 × 1,2 = 1,2 zaokrouhleno nahoru` |

2. **Výběr konkrétního hardwaru z katalogu výrobce:**
   - Navrhněte konkrétní přístroj z praxe (např. *Siemens LOGO! 24RCE + rozšiřující moduly*, *Siemens S7-1200 CPU 1212C/1214C DC/DC/RLY*, *Schneider Modicon M221*, *Eaton easyE4-UC-12RC1*, *WAGO 750*, případně průmyslový IoT kontrolér typu *UniPi Neuron*).
   - Uveďte:
     - Výrobce a přesný model CPU: `Siemens SIMATIC S7-1200 CPU 1214C DC/DC/DC`
     - Objednací kód (Part Number / Order Code): `6ES7214-1AG40-0XB0`
     - Rozšiřující moduly (pokud jsou nutné pro AI 4–20 mA nebo AO 0–10 V): `AI modul: SM 1231 AI 4 × 13 bit (objednací kód: 6ES7231-4HD32-0XB0) – umožňuje přímé zapojení proudové smyčky 4–20 mA pro hydrostatickou sondu.   AO modul: SB 1232 AO 1 × 12 bit (objednací kód: 6ES7232-4HA30-0XB0) – Signálová deska (Signal Board) vložená přímo do těla CPU pro napěťový výstup 0–10 V pro frekvenční měnič.`
     - Napájecí napětí zvolené jednotky: `24 V DC`
     - Jak je vyřešeno odesílání dat na dispečink: `CPU obsahuje integrovaný Ethernet (PROFINET) port a podporuje protokol Modbus TCP nativně v základní výbavě. Pro zálohu/bezdrátový přenos přes GSM/LTE lze doplnit komunikační modul CP 1243-1 LTE (6GK7243-1DX30-0XE0).`
     - Odkaz na technický list (datasheet): `(https://www.google.com/search?q=https%3A%2F%2Fmall.industry.siemens.com%2Fmall%2Fcz%2Fcz%2FCatalog%2FProduct%2F6ES7214-1AG40-0XB0)`
     - Odkazy na další použité zdroje: `(https://www.google.com/search?q=https%3A%2F%2Fsupport.industry.siemens.com%2Fcs%2Fww%2Fen%2Fps%2F13683%2Fman)`

3. **Technické ověření z datasheetu:**
   - Zvládá zvolená jednotka garantovaný provoz při -20 °C? Doložte údaj z datasheetu: `Standardní jednotky S7-1200 mají provozní teplotu 20°C až 60°C (při vodorovné instalaci). V datasheetu Siemens uvádí: "Free fall / Ambient temperature during operation: 20°C to 60°C. Jednotka tak vyhovuje zadanému rozsahu bez nutnosti speciální řady SIPLUS.`
   - Jakým způsobem spínáte cívku stykače 230 V AC (reléový výstup jednotky přímo, nebo přes pomocné mezilehlé relé)? Zdůvodněte: `Řešení a zdůvodnění: Cívku spínáme přes pomocné mezilehlé relé (např. Finder / Weidmüller s paticí na DIN lištu).`

`Důvod: Galvanické oddělení řídicí elektroniky PLC od silového napětí 230 V AC. Při případném zkratu nebo indukčním rázu při vypnutí cívky stykače dojde k poškození vyměnitelného pomocného relé za pár korun, nikoli k proražení výstupního tranzistoru nebo spálení kontaktu na základní desce PLC.`

4. **Krytí rozváděče:**
   - Jaké minimální krytí **IP skříně** zvolíte? Jak v rozváděči zajistíte provoz v mrazech -20 °C a v letních vedrech?
     - Zvolené krytí rozváděče: `IP65 (nebo IP66) – prachotěsná skříň odolná proti tryskající vodě, vhodná pro venkovní nekrytý terén vystavený dešti.`
     - Teplotní management skříně: `Provoz v mrazech (-20 °C): Instalace odporového topného tělesa s termostatem (např. STEGO 50–100 W) do spodní části rozváděče pro udržení vnitřní teploty nad bodem mrazu a prevenci kondenzace vlhkosti.`
     
`Provoz v letních vedrech (+45 °C): Instalace ventilační jednotky s prachovým filtrem a termostatem (případně se solárním krytem / dvojitou střechou proti přímému slunečnímu záření), přičemž krytí ventilačních mřížek musí zachovávat krytí min. IP54/IP55 s použitím krycích stříšek.`

> **Kritéria hodnocení úlohy 4 (bodování a známka):**
> - :star: **Správnost I/O bilance a dimenzování (30 %):** Správný součet všech signálů, korektní rozlišení reléových vs. tranzistorových výstupů a správné započtení rezervy min. 20 %.
> - :star: **Reálnost výběru a kompatibilita HW (40 %):** Zvolený přístroj skutečně existuje na trhu, konfigurace plně pokrývá všechny vstupy/výstupy (včetně analogů 4–20 mA a 0–10 V) a komunikaci.
> - :star: **Posouzení provozních podmínek a instalace (30 %):** Správná volba krytí rozváděče (min. IP65), vyřešení vytápění/ventilace pro mráz a spolehlivé galvanické oddělení výkonových akčních členů.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Proudová smyčka 4–20 mA:** Průmyslový standard pro přenos analogových signálů ze senzorů. Výhodou oproti napěťovému signálu 0–10 V je vysoká odolnost proti elektromagnetickému rušení, nezávislost na odporu dlouhého vedení a detekce přetržení vodiče (pokud je proud roven 0 mA, jde o poruchu vedení – tzv. živá nula / live zero).
> 	Proudová smyčka. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-04-18 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Proudov%C3%A1_smy%C4%8Dka
> - **Galvanické oddělení:** Elektrické oddělení dvou elektrických obvodů (např. pomocí optočlenů nebo relé), které zabraňuje přenosu rušení, rozdílům zemních potenciálů a chrání citlivé vstupy řídicí jednotky před zničením přepětím.
> - **Bezpotenciálový kontakt** (označovaný také jako **dry contact**) je elektrický kontakt, který sám o sobě nemá žádné vlastní napětí ani neposkytuje žádný proud. Funguje čistě jako mechanický nebo elektronický spínač (jako klasický vypínač na zdi), který pouze spojí nebo rozpojí dva vodiče v externím obvodu.

<details>
<summary> :bulb: Tip pro výběr modulů: </summary>
<p>Pozor na analogové vstupy: Základní kompaktní jednotky (např. LOGO! nebo S7-1200) mívají integrované analogové vstupy pouze pro napětí 0–10 V. Vstupní signál 4–20 mA ze sondy vyžaduje buď speciální rozšiřující modul pro proudové signály, nebo zařazení přesného paralelního odporu 500 Ω (převod 4–20 mA na 2–10 V).</p>
</details>

:star2: **Bonusová otázka k úloze 4:**
Proč se u čerpadel v čistírnách odpadních vod a jímkách striktně upřednostňuje měření hladiny pomocí proudového signálu 4–20 mA před napěťovým signálem 0–10 V a proč se do jímky nepoužívá ultrazvukový senzor, pokud v ní vzniká hustá pěna?

*Vaše odpověď:*
Otázku jsem si rozdělil na dvě odpovědí:

`1. Nereaguje na rušení ani délku drátů: Velká čerpadla v jímkách vytváří elektřinu, která napěťový signál (0–10 V) snadno zkreslí. Proudový signál (4–20 mA) tímto rušením netrpí a funguje přesně i na dlouhé vzdálenosti.`

`Pozná přetržený kabel: Nejnižší možná hodnota pro měření je 4 mA. Pokud do řídicí jednotky teče 0 mA, systém hned ví, že se přetrhl drát nebo vypadla sonda, a nahlásí poruchu. U napětí (0 V) systém nepozná, jestli je jímka prázdná, nebo je utržený kabel.`

`2. Pěna tlumí zvuk: Ultrazvuk měří tak, že pošle zvukový signál a čeká, až se odrazí od vody zpět. Hustá pěna funguje jako akustická izolace – zvuk pohltí a senzor nic nenaměří.`

`Měří špatnou výšku: Pokud se zvuk od pěny přece jen odrazí, senzor změří výšku pěny, ne reálnou hladinu vody. Čerpadlo by si pak myslelo, že je v jímce voda, i když tam je jen pěna. Proto se raději používá ponorná sonda až na dně, která měří tlak vody pod pěnou.`

---

### 5. Technický audit a oponentura nevhodného návrhu

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jako vedoucí inženýr jste převzal projekt po nezkušeném brigádníkovi, který navrhl řízení automatizovaného tvářecího a lisovacího stroje v prašné kovářské dílně následovně:
- **Řídicí deska:** Běžná vývojová deska **Arduino Uno (Rev3)** s mikrokontrolérem ATmega328P.
- **Pouzdro a umístění:** Plastová krabička vytištěná na 3D tiskárně z materiálu **PLA**, přišroubovaná přímo na těleso vibrujícího hydraulického lisu.
- **Napájení:** 5V USB nabíječka na mobilní telefon zapojená do prodlužovacího kabelu 230 V.
- **Spínání zátěže:** 4kanálový hobby reléový modul z čínského e-shopu propojený s Arduinem tenkými nepájenými vodiči (DuPont propojky). Modul přímo spíná 400V ventily hydrauliky.
- **Bezpečnost (Safety):** Nouzové stop tlačítko (E-Stop) je zapojeno přímo do digitálního pinu D2 Arduina jako softwarové přerušení (interrupt), které v kódu nastaví výstupy na `LOW`.

#### Váš úkol:

1. **Zpracujte písemný audit rizik (minimálně 4 fatální technická selhání):**
   Vyplňte protokol o zjištěných vadách a popište konkrétní fyzikální mechanismus, jak daná chyba způsobí havárii stroje či ohrožení lidského života:

| Oblast auditu | Zjištěná vada v amatérském návrhu | Fyzikální mechanismus selhání (proč to selže) | Následek pro stroj nebo obsluhu |
| :--- | :--- | :--- | :--- |
| **Elektromagnetická kompatibilita (EMC)** | `Použití nepřímo stíněného vývojového modulu Arduino Uno a nechráněné USB nabíječky z 230V` | Napěťové špičky z indukční zátěže hydraulických ventilů způsobí restart MCU... | `Ztráta kontroly nad řízením lisu, nepředvídatelné chování (např. nekontrolovaný pohyb hydrauliky) nebo trvalé sepnutí výstupů` |
| **Mechanická a teplotní odolnost** | PLA plast a montáž na těleso lisu | `PLA má nízkou teplotní odolnost a nízkou houževnatost. Neustálé vibrace hydraulického lisu způsobí únavu materiálu, prasknutí krabičky a její odtržení. Teplo z lisu způsobí deformaci krytu` | `Mechanické zničení řídicí elektroniky, obnažení živých částí a ztráta ochrany krytím (IP)` |
| **Konektivita a propojení vodičů** | DuPont propojovací kabely bez aretace | `Nepájené, volně nasunuté krimpované konektory (DuPont) nemají žádnou mechanickou pojistku. Vlivem vibrací dochází k mikro-pohybům, přechodovému odporu, jiskření a nakonec k úplnému vypadnutí vodičů` | `Náhodné vypadávání signálů, výpadky řízení nebo nechtěné sepnutí/rospnutí hydraulických ventilů` |
| **Funkční bezpečnost (Safety)** | Nouzový stop řešený softwarově v čipu | `Pokud mikrokontrolér zatuhne (zasekne se čip vlivem EMC rušení, přeteče paměť nebo zamrzne kód), přerušení (interrupt) se vůbec nevyrazí a software nezreaguje` | `Při stisku tlačítka E-Stop stroj nepřestane pracovat, což vede k přímému ohrožení života a zdraví obsluhy (riziko přimáčknutí či amputace)` |

2. **Návrh profesionálního nápravného řešení:**
   - Navrhněte, jakými certifikovanými průmyslovými komponenty tento celek nahradíte při zachování minimálního rozpočtu:
     - *Náhrada řídicí jednotky:* `Průmyslové PLC nebo programovatelné relé s montáží na DIN lištu (např. Siemens LOGO!, Schneider Zelio Logic nebo Eaton EASY) s certifikovanou EMC odolností a krytím IP20/IP65 v rozvaděči` *(např. certifikované průmyslové programovatelné relé s montáží na DIN lištu a krytím)*
     - *Náhrada napájecího zdroje:* `Stabilizovaný průmyslový spínaný zdroj 24 V DC na DIN lištu (např. Mean Well řada HDR/NDR nebo Siemens SITOP) s ochranou proti přepětí, přetížení a zkratu` *(např. stabilizovaný průmyslový zdroj 24 V DC na DIN lištu s ochranou proti přepětí)*
     - *Způsob zapojení bezpečnostního okruhu (Safety):* Jak musí být podle norem zapojeno tlačítko Emergency Stop (E-Stop)? Smí být spoléháno pouze na software mikrokontroléru? Zdůvodněte: `Tlačítko Emergency Stop (červený hřib s žlutým podkladem) musí být zapojeno dvoukanálově do samostatného bezpečnostního relé (např. Pilz PNOZ, Schneider Preventa nebo Siemens SIRIUS). Bezpečnostní relé při stisku tlačítka přímo na hardwarové úrovni odpojí napájení silových stykačů hydraulických ventilů`

`NESMÍ. Dle normy EN ISO 13849-1 / IEC 62061 nesmí bezpečnostní funkce záviset na nedůvěryhodném softwaru nebo standardním MCU bez bezpečnostní certifikace. Software může zamrznout, zacyklit se nebo selhat v důsledku EMC rušení. Bezpečnostní odpojení musí fungovat vždy nezávisle na řídicím procesoru.`

> **Kritéria hodnocení úlohy 5 (bodování a známka):**
> - :star: **Odborná úroveň identifikace závad (35 %):** Přesná technická terminologie (např. elektromagnetická indukce, absence odrušovacích varistorů, skelný přechod PLA plastu při 60 °C, studené spoje a vyklepání konektorů vibracemi).
> - :star: **Pochopení norem funkční bezpečnosti Safety (35 %):** Znalost základního principu bezpečnosti strojních zařízení – nouzové zastavení musí být řešeno hardwarově přes certifikované bezpečnostní relé s nuceně vedenými kontakty, nikoliv pouhým softwarovým vstupem MCU.
> - :star: **Kvalita a realizovatelnost nápravného řešení (30 %):** Návrh odpovídá robustní průmyslové praxi s montáží do oceloplechového rozváděče na DIN lištu.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Funkční bezpečnost (Safety) vs. Kybernetická bezpečnost (Security):** *Safety* (dle ČSN EN ISO 13849-1) zajišťuje, že strojní zařízení nezpůsobí úraz člověku ani při vnitřní poruše řídicího systému (využívá redundantní obvody, bezpečnostní relé, optické závory, kategorii spolehlivosti PL a až PL e / SIL 3). *Security* řeší ochranu dat a systému před úmyslným napadením zvenčí (hackeři, malware).
> - **EMC (Elektromagnetická kompatibilita):** Schopnost zařízení spolehlivě pracovat v prostředí s elektromagnetickým rušením (odolnost / imunita) a současně nezpůsobovat nepřípustné rušení jiným zařízením (emise).
> 	Elektromagnetická kompatibilita. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-11-20 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Elektromagnetick%C3%A1_kompatibilita

<details>
<summary> :bulb: Tip k bezpečnostnímu okruhu (Safety): </summary>
<p>Základní pravidlo bezpečnosti: <strong>Software může selhat, zacyklit se nebo zamrznout.</strong> Bezpečnostní okruh nouzového zastavení (červený hřib) musí být vždy dvoukanálový, zapojený do hardwarového bezpečnostního relé (např. Pilz, Schneider Preventa, Siemens SIRIUS), které odpojí silové napájení stykačů ventilů přímo na hardwarové úrovni nezávisle na procesoru!</p>
</details>

:star2: **Bonusová otázka k úloze 5:**
Proč hobby reléové moduly s optočleny určené pro Arduino v průmyslovém rozváděči často shoří nebo způsobí trvalé sepnutí zátěže (tzv. přivaření kontaktů), i když jmenovitý proud relé je 10 A a cívka stykače odebírá jen 0,5 A?

*Vaše odpověď:*
`Hlavním důvodem přivaření kontaktů je indukční charakter zátěže cívky stykače. Udávaný proud 10 A u hobby relé platí výhradně pro čistě odporovou zátěž (AC-1); při spínání a vypínání indukční cívky však vzniká vysoká proudová špička a silné přepěťové napětí, které způsobuje elektrický oblouk. Tento oblouk roztaví nekvalitní slitinu kontaktů hobby relé a dojde k jejich trvalému přivaření k sobě. Levné plošné spoje navíc nemají dostatečné izolační vzdálenosti pro průmyslové napěťové špičky, což leads k proražení optočlenů nebo shoření desky.`

---

### 6. Rozšiřující inženýrská výzva: TCO a životní cyklus v automatizaci

*Časová dotace: 15–20 minut | :star2: Bonusová výzva pro pokročilé studenty*

V průmyslové automatizaci nákupní cena řídicí jednotky (CAPEX) často tvoří méně než 15 % celkových nákladů na životní cyklus zařízení (OPEX / TCO).

Představte si, že management firmy rozhoduje mezi dvěma variantami řízení pro sérii 50 kusů výrobních linek s plánovanou životností 15 let:
- **Varianta 1 (Nízkonákladová na pořízení):** Využití levných embedded mikrokontrolérových desek s vlastním zákaznickým návrhem plošného spoje (cena HW: 2 500 Kč / kus, vývoj firmwaru v C/C++ od externího programátora bez dokumentace).
- **Varianta 2 (Průmyslový standard):** Využití modulárního PLC renomovaného výrobce (Siemens / Rockwell / Schneider) s cenou 22 000 Kč / kus, programováno v normovaném jazyce LAD/ST dle IEC 61131-3.

#### Váš úkol:
1. Srovnejte obě varianty v níže uvedené tabulce a uveďte předpokládaná skrytá rizika a náklady v horizontu 10–15 let:

| Aspekt životního cyklu | Varianta 1 (Custom Embedded MCU) | Varianta 2 (Průmyslové PLC) |
| :--- | :--- | :--- |
| **Dostupnost náhradních dílů za 10 let** | `...` | `...` |
| **Servisovatelnost podnikovým elektrikářem** | `...` | `...` |
| **Doba odstávky linky při poruše CPU** | `...` | `...` |
| **Cena vývojových nástrojů a licencí IDE** | `...` | `...` |
| **Závěrečné doporučení (kterou variantu vybrat a proč)** | `...` | `...` |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **CAPEX (Capital Expenditure)**: Zjednodušeně jde o jednorázové kapitálové výdaje na pořízení samotného zařízení (hardware, licence).
> - **OPEX (Operating Expense)**: Zjednodušeně jde o průběžné provozní náklady nutné k udržení zařízení v chodu (energie, servis, podpora).
> - **TCO (Total Cost of Ownership):** Finanční odhad celkových přímých i nepřímých nákladů spojených s pořízením, provozem, servisem, údržbou a likvidací produktu po celou dobu jeho životnosti. Zjednodušeně je to součet CAPEX + OPEX za celou dobu životnosti zařízení. 
> 	Total cost of ownership. *Wikipedia: The Free Encyclopedia* [online]. St. Petersburg (Florida): Wikimedia Foundation, 2024, 2024-08-14 [cit. 2026-09-17]. Dostupné z: https://en.wikipedia.org/wiki/Total_cost_of_ownership
> - **Vendor Lock-in:** Stav závislosti zákazníka na konkrétním dodavateli produktů nebo služeb, kdy je přechod k jiné platformě spojen s neúměrně vysokými finančními i časovými náklady.

<details>
<summary> :bulb: Tip k úvaze o TCO: </summary>
<p>Když za 7 let odejde custom deska z Varianty 1 a původní vývojář již ve firmě nepracuje a čip se nevyrábí, musí firma vyvinout celou řídicí elektroniku znovu od nuly. Hodina odstávky automobilové linky přitom stojí desítky až stovky tisíc korun.</p>
</details>

:star2: **Bonusová otázka k úloze 6:**
Co znamená pojem **MTBF (Mean Time Between Failures)** v datasheetech průmyslových řídicích jednotek a jaký vliv má okolní teplota v rozváděči na tuto hodnotu (tzv. Arrheniovo pravidlo)?

*Vaše odpověď:*
`...`
