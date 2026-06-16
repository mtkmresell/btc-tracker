# ₿ BTC Tracker

Soukromá webová aplikace pro evidenci nákupů bitcoinu.

## Funkce

- 📒 Zápis nákupů: datum, množství BTC, zaplacená částka v CZK, místo nákupu (burza/směnárna), poznámka
- 💰 Přehledové karty: celkem BTC, investováno, aktuální hodnota (živý kurz z CoinGecko), zisk/ztráta, průměrný nákupní kurz
- ⏳ **Časový test 3 roky** – u každého nákupu odpočet dní do osvobození od daně z příjmu (§ 4 odst. 1 písm. x ZDP) a součet BTC, které už lze prodat s 0% daní
- 📈 Grafy: naakumulované BTC v čase, investováno vs. hodnota dnes
- ⬇ Export do CSV (podklad pro finanční úřad) a zálohování/obnova v JSON

- ☁️ **Synchronizace přes Firebase** – vlastní projekt `domacnost-finance` (pro osobní domácí/finanční aplikace), data dostupná na všech zařízeních (doma, práce, mobil); offline fallback na localStorage
- ⬆ **Import historie z Excelu** (.xlsx/.csv) s mapováním sloupců – aplikace sloupce sama rozpozná a chybějící údaje (cena/množství) doplní z historického kurzu BTC k datu nákupu (CoinGecko); doplněné hodnoty jsou označené jako ~odhad

## Použití

Žádná instalace ani build – jediný `index.html`, hostovatelný na GitHub Pages.
Data se ukládají do Firestore pod `users/{uid}/btc/data` (Firebase projekt
`domacnost-finance`) a zrcadlí se do localStorage. Pravidelně si dělej zálohu
přes „Záloha JSON".

### Import z Excelu

1. Klikni na „⬆ Import z Excelu" a vyber soubor.
2. Zkontroluj automatické přiřazení sloupců (datum je povinné + aspoň množství BTC nebo částka).
3. Co v Excelu nevedeš, nech „— nemám —" – kurz a chybějící hodnota se dopočítá z historického kurzu.
4. Duplicitní řádky se při opakovaném importu přeskočí.

Free API CoinGecko má limit ~10 dotazů/min, u většího importu doplnění chvíli trvá
(mezi dotazy se čeká); co se nestihne, doplní tlačítko „🪄 Doplnit chybějící údaje".

> ⚠️ Aplikace není daňové poradenství. Časový test se počítá jako 3 roky od data nákupu.
