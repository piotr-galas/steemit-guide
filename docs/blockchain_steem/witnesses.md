Sieć steem oparta jest na zdecentralizowanym blockchain-ie. Można wyobrazić to sobie, jako wielką zdecentralizowaną bazę danych.
Zdecentralizowaną, czyli nie ma jednego serwera na którym zainstalowana jest aplikacja [steemd](https://github.com/steemit/steem), a zamiast tego aplikacja [steemd](https://github.com/steemit/steem) zainstalowana jest na
wielu komputerach. Pojedynczy komputer wpięty w sieć nazywa się nodem.
W komentarzu do artykułu [Dla początkujących użytkowników Steem](https://steemit.com/polish/@alcik/dla-poczatkujacych-uzytkownikow-steem-troche-o-blockchainie-steem-wynagrodzeniu-kuratorskim-i-kategoriach#@piotr-galas/re-alcik-dla-poczatkujacych-uzytkownikow-steem-troche-o-blockchainie-steem-wynagrodzeniu-kuratorskim-i-kategoriach-20171218t213123167z)
użytkownik [@jamzed](https://steemit.com/@jamzed) napisał komentarze wyjaśniające role nodów. Oto treść jednego z nich


Każdy może uruchomić własny node Steem-a, z technicznego punktu widzenia jest to serwer na którym działa aplikacja [steemd](https://github.com/steemit/steem). steemd "rozumie" blockchain, jest w stanie z niego pobierać dane i zapisywać. Węzły można podzielić na 3 główne grupy:


* seed node
* exchange / api node
* witness node

**seed node**  
to rodzaj węzła którego głównym zadaniem jest przechowywanie aktualnej wersji blockchain-a i udostępnianie danych wszystkim zainteresowanym, w praktyce wygląda to tak, że jeśli uruchomisz steemd to aplikacja połączy się do seed node-ów i z nich pobierze aktualne dane niezbędne do działania. Listę takich node-ów możesz zobaczyć na https://github.com/steemit/steem/blob/master/doc/seednodes.txt.

**exchange / api node**  
to również ta sama aplikacja steemd ale uruchomiona z dodatkowymi pluginami, dzięki temu możemy pobierać konkretne dane o postach, użytkownikach, tagach, transakcjach, itd. Komunikacja klienta z takim węzłem odbywa się poprzez interfejs RPC (json), przykładowy request zwracający informację o koncie wygląda tak,

$ curl --data '{"jsonrpc": "2.0", "method": "get_accounts", "params": [["jamzed"]], "id": 1 }' https://gtg.steem.house:8090/rpc

Listę publicznie dostępnych API node-ów możesz sprawdzić na https://geo.steem.pl/ (mała autoreklama) ;-)

**witness node**   
to też steemd ale uruchomiony z pluginem witness, pozwalącym "produkować" bloki. Steem opiera się o protokół DPOS (Delegated Proof of Stake), więc do poprawnego działania całej sieci potrzebni są delegaci którzy są wybierani poprzez głosowanie. Każdy może być witnessem (opublikować publiczny klucz typu signing), ale żeby realnie produkować bloki trzeba jeszcze uzyskać odpowiednią liczbę głosów i nie chodzi tu o ich ilość, ale o moc (ilość posiadanych VESTS przez głosującego). Witnessi oprócz produkcji bloków ustalają również cenę STEEM, wysokość opłaty za utworzenie nowego konta, posiadają również kilka mechanizmów dzięki którym są w stanie "sterować" wartością SBD który zawsze powinien być w okolicy ~1 USD.