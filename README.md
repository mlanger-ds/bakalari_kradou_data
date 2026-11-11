# Firma Bakaláři krade škole data - backdoor ve webové apilkaci #
Webová aplikace na IIS serveru (lokálně provozovaném) se pravidelně (téměř) každou noc připojuje na stats.bakalari.cz.  
Odtud získá seznam příkazů, které provede - získá data z databáze a odešle je firmě Bakaláři na stats.bakalari.cz (nejsou to webové stránky, proto po kliknutí prohlížeč nic nezobrazí)

Je to cca stovka příkazů, které získávají informace např. o uživatelích, učitelích, absencích, bankovních výpisech, přijímačkách, konfiguraci bakalářů, ... O aktuálním využívání firmou Bakaláři svědčí mj. to, že jedny ze získávaných dat jsou "Kdo využívá flexi rozvrh" - tj. nejde o starou zapomenutou funkčnost.

[Seznam popisů příkazů](https://github.com/mlanger-ds/bakalari_kradou_data/blob/main/prijate_prikazy_popisy.txt) a kompletní výpis [prijate_prikazy.json](https://github.com/mlanger-ds/bakalari_kradou_data/blob/main/prijate_prikazy.json) vč. SQL příkazů.  
Příkazy zarovnané SQL pro lepší čtení [queries_sql_indented.json](https://github.com/mlanger-ds/bakalari_kradou_data/blob/main/queries_sql_indented.json)  
Ukázka odesílaných dat (mnou anonymizovaná, údaje nahrazeny XXXX - skutečně odesílaná data jsou pouze pseudonymizovaná, obsahují unikátní identifikátory osob a neagregovaná) [send_first_3_anon.json](https://github.com/mlanger-ds/bakalari_kradou_data/blob/main/send_first_3_anon.json)

Proč tvrdím "krade" - protože bez vědomí zákazníka získává jeho data, jeho vlastnictví prostřednictvím zadních vrátek (backdoor) v software.

Existence takových zadních vrátek, (umožňují přijímat nejen SQL příkazy SELECT ale i UPDATE, INSERT, DELETE tj. i měnit a mazat data - aktuálně ověřuji v testovacím prostředí zda to opravdu jde) je velmi vážná bezpečnostní zranitelnost.

### Jak tomu zabránit? ###
Jednoduše - na webovém IIS serveru do souboru `C:\Windows\System32\drivers\etc\hosts` doplnit řádek (jsou nutná administrátorská práva)
`127.0.0.1   stats.bakalari.cz`

Na to jaká a kam přenáší webová aplikace bakaláři jsem se zeptal 17. 1. 2026, tiket #417458 - dosud bez odpovědi.
