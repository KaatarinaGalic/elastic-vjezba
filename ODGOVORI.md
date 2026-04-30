# 1 Zadatak - statusi klastera:
### Green
Svi shardovi su aktivni i svi podaci su dostupni, klaster radi savrseno.
### Yellow
Primarni shardovi rade ali replike nisu dostupne.. Podaci su dostupni ali nema potpune sgurnosti.
### Red
Red upućuje da postoji problem nesto nedostaje.Neki shardovi nisu dostupni i dio podataka takodjer nije dostupan.

# Zadatak 2 – Mapping

## 5. Zasto je naslov tipa text
Polje naslov je definirano kao text zato što želimo omoguciti full-text pretragu. To znaci da Elasticsearch razbija naslov na manje dijelove (tokene) i omogućuje pretragu po pojedinim riječima, a ne samo po cijelom tekstu. Na taj način korisnik može pronaći knjigu i ako upiše samo dio naslova.

## 6. Zasto postoji dodatno polje naslov.keyword
Polje naslov.keyword postoji kako bi se omogućilo točno podudaranje, sortiranje i agregacije. Za razliku od text tipa, ovo polje se ne analizira i čuva originalnu vrijednost naslova. To je korisno kada želimo npr. sortirati knjige po nazivu ili grupirati rezultate.

## 7. Zasto su autor i zanr tipa keyword
Polja autor i zanr su tipa keyword jer se koriste za tocno podudaranje i filtriranje podataka. Kod ovih polja nije potrebno razbijanje na tokene jer ne tražimo dijelove teksta, nego točne vrijednosti (kao odredjeni autor ili žanr). Takodjer ovakav tip je učinkovitiji za agregacije.

## 8. Zašto se opis ne bi trebao spremati kao keyword
Polje opis predstavlja duži tekst i zato treba biti tipa text. Na taj način Elasticsearch može analizirati sadržaj i omogućiti pretragu po riječima i pojmovima unutar opisa. Kada bi opis bio keyword, tretirao bi se kao jedna cjelina i pretraga po pojedinim riječima ne bi bila moguća, što bi značajno smanjilo funkcionalnost pretrage.

# 3.Zadatak
### 11. u ODGOVORI.md objasniti zašto pretraga 'cuprija' pronalazi dokument 'Na Drini ćuprija'
Pretraga pojma cuprija pronalazi dokument "Na Drini ćuprija" jer analyzer koristi filter asciifolding.
Taj filter uklanja dijakritičke znakove, pa se riječ "ćuprija" indeksira i kao "cuprija" što omogućava uspješnu pretragu bez kvačica.

### 12. pogledati polje _score u rezultatu i objasniti što označava i zašto se razlikuje među dokumentima
Polje _score predstavlja relevantnost dokumenta u odnosu na upit.
Veći _score znači da dokument bolje odgovara pretraživanom pojmu.
Razlike u _score vrijednostima mogu biti zbog ucestalosti pojma u tekstu,duzine teksta ili pozicije riječi u dokumentu.


