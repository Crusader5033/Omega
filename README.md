# Projekt Omega: Správa vojáka z povolání AČR

Tato okenní aplikace v C# slouží k správě vojáků z povolání v rámci vojenských služeb. Umožňuje zobrazovat, přidávat, mazat a upravovat informace o vojácích, jejich službách, zkouškách, specializacích a útvarech. Stejně tak zpracovává přihlášení uživatelů a registraci uživatelů pro používání aplikace. Další funkcí je  možnost spravovat uživatel a procházet záznamy přihlášení a registrace.

### Předpoklady pro Spuštění
Operační systém Windows 10 a novější. Nezbytné je mít nainstalovaný .NET Framework a správně nakonfigurovanou MSSQL databázi(to platí pro pokročilé uživatele viz. konfigurace pro pokročilé uživatele).

## Konfigurace

Pro běžného uživatele doporučujeme neupravovat ani se nijak jinak věnovat konfiguraci. S případnými dotazy ohledně konfigurace se obraťte na Vašeho správce IT. V případě že jste pokročilí uživatel vše naleznete v konfiguraci pro pokročilé 

## Spouštění Aplikace

Pro spuštění aplikace stačí spustit spustitelný soubor (exe) Omega.exe ve Omega\bin\Debug, aplikace se spustí sama

## Vytváření, Čtení, Aktualizace a Mazání (CRUD) Operace

Pro většinu entit (voják, specializace, zkouška, útvar, role, služba) jsou implementovány funkce pro CRUD operace, umožňující manipulaci s daty v databázi.

## HOW TO

### Přihlášení
Po spuštění.Budete vyzváni k zadání uživatelského jména a hesla. Pokud máte oboje, vyplňte pole a stisknete tlačítko pro přihlášení.

### Registrace
Pokud nemáte uživatelské jméno a heslo, zaregistrujte se. V oknu přihlášení stiskněte tlačítko pro registraci. Otevře se nové okno, vyplňte všechna pole a stiskněte tlačítko pro registraci.Pokud je vše správně dostanete potvrzení a můžete okno pro registraci zavřít a přihlásit se.

### Čtení
Zobrazení dat o vojácích, specializacích, zkouškách, útvarech, rolích a službách se provádí v okně výpis. Stačí stisknout tlačítko výpis a následně si vybrat jakou tabulku chcete zobrazit

### Vytvoření
Přidání nových záznamů do databáze je možné pomocí příslušných formulářů v okně pro přidání.Stiskněte tlačítko vložit. Vyberte pomocí záložek na vrchní straně jaký záznam chcete přidat.

### Mazání
Smazání záznamů lze provést pomocí okna pro smazání, kde je nutné vybrat, který záznam se má odstranit.Stiskněte tlačítko smazat.Pomocí záložek procházejte záznamy v různých tabulkách. Pro vybrání konkrétního záznamu pro smazání stiskněte první políčko(sloupec před id). Následně stiskněte na odpovídající tlačítko.

### Aktualizace
Upravování dat v databázi probíhá v okně úprava.Stiskněte tlačítko upravit.Pomocí záložek procházejte záznamy v různých tabulkách.Pro vybrání konkrétního záznamu pro úpravu stiskněte první políčko(sloupec před id).Vyplňte údaj který chcete změnit a stiskněte tlačítko pro úpravu. Není nutné vyplňovat všechny údaje.

### Export
Export dat z tabulek. Vyberte si v hlavním okně export buď v CSV či XML. Objeví se nové okno, vyberte tabulku ze které chcete exportovat data a stiskněte příslušné tlačítko. Vyberte cestu pro váš export a potvrďte.


### Přístup k AdminMenu
Odhlašte se pomocí Odhlásit tlačítka případně při dalším spuštění. Jako uživatelské jméno zadejte: admin ,heslo také: admin. Otevře se nové okno pro práci s uživateli a procházení záznamů přihlášení a registrace.


## Konfigurace pro pokročilé 
Vše pro konfiguraci naleznete zde případně se obraťte na pdf přiložené k aplikaci.Toto je doporučeno pro správce IT případně uživatele kteří mají zkušenost s MSSQL a vědí co dělají.
###  Nastavení DB
Nejdříve je potřeba vytvořit DB do které se bude aplikace připojovat, zde je diagram:
![DiagramSQL](https://github.com/Crusader5033/Omega/assets/113086006/f38c3b94-3149-4c5e-8e91-95b486be3c12)
Ujistěte se že username u uživatele by měl být unique.
### Struktura `app.config`
Nyní je potřeba upravit konfigutační soubor.
Konfigurační soubor app.config obsahuje informace potřebné pro připojení k MSSQL databázi. Struktura souboru je následující:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<appSettings>
		<add key="DataSource" value="193.85.203.188"/>
		<add key="Database" value="prochazka6"/>
		<add key="Name" value="prochazka6"/>
		<add key="Password" value="dominik2005"/>
	</appSettings>
</configuration>
```
### Nastavení Připojení do Databáze
Výše uvedené hodnoty (`DataSource`, `Database`, `Name`, `Password`) je třeba přizpůsobit aktuálním připojovacím údajům pro MSSQL server.



# Dokumentace pro vývojáře

## Struktura databáze
 

![DiagramSQL](https://github.com/Crusader5033/Omega/assets/113086006/81a95218-f230-483a-87a3-1f92c678e06b)


### Tabulky

- `Vojaci`: Obsahuje informace o vojácích.
- `Specializace`: Obsahuje informace o vojenských specializacích.
- `Zkousky`: Obsahuje informace o zkouškách, kterým vojáci podstupují.
- `Utvary`: Obsahuje informace o vojenských útvarech.
- `Role`: Obsahuje informace o vojenských rolích.
- `Sluzby`: Obsahuje informace o vojenských službách vojáků.
- `Users`: Obsahuje informace o uživatelích.
- `Logs`: Obsahuje informace o záznamech o přihlášení a registraci.
  
###  Pohledy
- `Vojaci_S_Specializacemi`: Pohled spojující informace o vojácích a jejich specializacích.
- `Vojaci_S_Sluzbami`: Pohled spojující informace o vojácích a jejich službách.
### Transakce
- Při přidání vojáka lze najednou přidat vojáka a automaticky mu přiřadiť zkoušku na KZP(Kurz základní přípravy).
## Modelování Databáze

### Singleton pro Připojení
Pro zajištění efektivního připojení k databázi se využívá singleton třída `DatabaseSingleton`.

### Třídy Controller a Model
Pro každou tabulku existuje Controller a Model třída , uživatel pracuje oknem které následně pracuje s Controllerem a následně Model s DB. Například `RoleController` a `Role` pro tabulku `Role` ,.

## Struktura Aplikace
![Výstřižek](https://github.com/Crusader5033/Alfa3/assets/113086006/e798132d-2ade-463d-b80c-1ea692e762f4)

### Okna
Aplikace obsahuje několik oken:
- **Hlavní Okno**: Zobrazuje nabídku oken pro práci s DB.
- **Přidání **: Slouží k přidání nových záznamů do databáze.
- **Smazání **: Slouží ke smazání záznamů z databáze.
- **Výpis **: Obsahuje funkce na výpis záznamů v databázi.
- **Úprava **: Obsahuje funkce na úpravu záznamů v databázi.
- **Přihlášení **: Okno pro přihlášení do aplikace a vstupu do registrace.
- **Registrace **: Okno pro vytvoření uživatele.
- **AdminMenu **: Hlavné okno pro práci a prohlížení uživatelů a záznamů.
- **Uživatelé **: Obsahuje funkce pro správu,úpravu a export uživatelů.
- **Záznamy **: Obsahuje funkce pro prohlížení a export záznamů.
- **ExportCSV **: Okno pro export tabulek do formátu CSV.
- **ExportxML **: Okno pro export tabulek do formátu XML.

## Funkce Oken
Každé okno má specifické funkce pro zobrazení, přidání, úpravu a mazání dat. Okna jsou navržena tak, aby bylo snadné pracovat s jednotlivými entitami.

### Knihovna třetí strany Krypton
V projektu byla využita knihovna třetí strany Krypton pro GUI, hlavně tlačítek a textBoxů v okně pro přihášení ,registraci a hlavním okně.
[odkaz na knihovnu](https://github.com/ComponentFactory/Krypton)
