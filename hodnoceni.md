Mám výhradu k projektu. Podle zadání je referenčním kompilátorem MSVC. Kód je považován za správný, pokud jej lze zkompilovat pomocí MSVC a běží pod Windows. Tady nastává několik problémů.

1) MSVC není standard compliant, nesplňuje standardy specifikované ISO. Teď nemyslím nadstandardní rozšíření (např. gcc podporuje definice funkce ve funkci, což standard C nepodporuje), ale vyloženě nesplnění specifikace (jako příklad: v C existuje knihovna iso646.h, v C++ jsou makra definovaná knihovnou standardem definovaná jako keywords, MSVC tohleto nesplňuje)

2) MSVC je Microsoftí technologie

3) MSVC není open source

4) MSVC běží pouze pod Windows. Studenti jsou tedy nuceni minimálně jednou použít Windows (což by mělo být považováno za válečný zločin). Kromě toho ale není možné použít platform specific knihovny/funkce jako jsou např. BSD funkce arc4random() pro generování náhodného čísla, POSIXová knihovna ncurses využitelná k tvorbě grafického rozhraní, atp.

---

Existuje jedno daleko jednodušší řešení, příjemnější pro všechny. Projekty by mohly běžet v Dockeru. Studenti by se zdrojovým kódem odevzdali také Dockerfile, ve kterém by měli vyřešené ubuildění projektu. 

**Výhody:**

1) Student by si sám mohl vybrat, pro jaký systém chce vyvíjet, jaké knihovny a jaký kompilátor chce použít. Celé prostředí by nastavil v Dockerfile. Vytvořil by si image na základě OS vlastního výběru, nainstaloval by si kompilátor i knihovny podle vlastního výběru a projekt by ubuildil vlastním způsobem. Takto odevzdaný projekt by se následně dobře kontroloval cvičícím, ale také dobře prezentoval studentům. Projekt by šlo spustit na jakémkoliv počítači, na kterém je nainstalovaný Docker. Nebylo by třeba bojovat s různými verzemi Visual Studia a také by odpadla nutnost pro studenty i cvičící používat stejný operační systém. 

2) Studenti by se seznámili s Dockerem, stále častěji používanější technologií, která je v praxi velmi oblíbená. Např. u nás v práci všechny nové komponenty běží v Kubernetu a staré se do Kubernetu portují, pokud to ještě má smysl.

3) Studenti by si mohli vyzkoušet kompilaci z příkazové řádky a podobné věci. Studenti jsou zvyklí na to, že za ně všechno dělá IDE. IDE je skvělý nástroj, který usnadňuje člověku práci, člověk by ale měl vědět, co za něj to IDE vůbec dělá. 

**Nevýhody:**

Ne všichni studenti mají s Dockerem zkušenosti a ne všichni by byli vůbec schopni pochopit, co Docker je a k čemu to slouží. Studenti by mohli mít problém sestavit si vlastní Dockerfile.

**Řešení:**

Studenti vůbec nemusí vědět, co Docker dělá a jak funguje. Bylo by možné poskytnout základní Dockerfile, který by vytvořil image založený např. na Debianu, aktualizoval repozitáře, updatoval software, stáhl g++, přidal složku src/ do image, ubuildil projekt (g++ *.cpp -std=c++14 -Os -Wall -o projekt) a nakonec projekt spustil (ENTRYPOINT ["./projekt"]). Schopnější a zvědavější studenti by si mohli sami dočíst, co je Docker a jak funguje a napsat si vlastní Dockerfile. 

---

**Námitka:** 

Docker by mohl zvýšit komplexitu a studenti by mohli mít s projektem problém

**Odpověď:** 

Studenti mají s projektem problém i bez Dockeru a je jim to úplně jedno, stejně většinu věcí opisujou a kopírují, jak jim je řečeno. To, že by se v Dockerfile mohli setkat s manuálním spouštěním kompilátoru by jim mohlo spíš prospět.
