# Projekt Omega: Správa vojáka z povolání AČR

Tato okenní aplikace v C# slouží k správě vojáků z povolání v rámci vojenských služeb. Umožňuje zobrazovat, přidávat, mazat a upravovat informace o vojácích, jejich službách, zkouškách, specializacích a útvarech. Stejně tak zpracovává přihlášení uživatelů a registraci uživatelů pro používání aplikace. Další funkcí je  možnost spravovat uživatel a procházet záznamy přihlášení a registrace.

### Předpoklady pro Spuštění
Operační systém Windows 10 a novější. Nezbytné je mít nainstalovaný .NET Framework a správně nakonfigurovanou MSSQL databázi(to platí pro pokročilé uživatele viz. konfigurace pro pokročilé uživatele).

## Konfigurace

Pro běžného uživatele doporučujeme neupravovat ani se nijak jinak věnovat konfiguraci. S případnými dotazy ohledně konfigurace se obraťte na Vašeho správce IT. V případě že jste pokročilí uživatel naleznete konfiguraci  [konfiguraci pro pokročilé zde](#konfigurace)

## Switch to another file

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## Rename a file

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.

## Konfigurace pro pokročilé {#konfigurace}
Vše pro konfiguraci naleznete zde případně se obraťte na pdf přiložené k aplikaci.Toto je doporučeno pro správce IT případně uživatele kteří mají zkušenost s MSSQL a vědí co dělají.
###  Nastavení DB
Nejdříve je potřeba vytvořit DB do které se bude aplikace připojovat, zde je diagram:
![DiagramSQL](https://github.com/Crusader5033/Omega/assets/113086006/f38c3b94-3149-4c5e-8e91-95b486be3c12)
Ujistěte se že username u uživatele by měl být unique.
### 2.1 Struktura `app.config`
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
