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

# 5.Zadatak
### lista tokena za korak 
{
  "tokens": [
    {
      "token": "brzi",
      "start_offset": 0,
      "end_offset": 4,
      "type": "<ALPHANUM>",
      "position": 0
    },
    {
      "token": "smedi",
      "start_offset": 5,
      "end_offset": 10,
      "type": "<ALPHANUM>",
      "position": 1
    },
    {
      "token": "most",
      "start_offset": 11,
      "end_offset": 15,
      "type": "<ALPHANUM>",
      "position": 2
    },
    {
      "token": "preko",
      "start_offset": 16,
      "end_offset": 21,
      "type": "<ALPHANUM>",
      "position": 3
    },
    {
      "token": "rijeke",
      "start_offset": 22,
      "end_offset": 28,
      "type": "<ALPHANUM>",
      "position": 4
    }
  ]
}
### lista tokena za 5. zadatak "Na Drini ćuprija"
{
  "tokens": [
    {
      "token": "na",
      "start_offset": 0,
      "end_offset": 2,
      "type": "<ALPHANUM>",
      "position": 0
    },
    {
      "token": "drini",
      "start_offset": 3,
      "end_offset": 8,
      "type": "<ALPHANUM>",
      "position": 1
    },
    {
      "token": "cuprija",
      "start_offset": 9,
      "end_offset": 16,
      "type": "<ALPHANUM>",
      "position": 2
    }
  ]
}

### 19.objasniti što rade filtri lowercase i asciifolding i u čemu je razlika!
lowercase pretvara sva slova u mala npr riječ "Drini" u "drini", dok asciifolding uklanja dijakritike npr "ćuprija" u "cuprija".
Razlika je u tome što lowercase mijenja velika/mala slova, a asciifolding uklanja posebne znakove.

### 20.objasniti zašto je analyzer ključan za full-text search i što bi se dogodilo da ga ne koristimo!
Analyzer omogučuje da se tekst razbije na riječi i normalizira te pretraga može pronaći riječi i kada nisu identične. Na primjer upit "cuprija" pronalazi ćuprija jer analyzer uklanja dijakritike.Bez analyzera bi se tekst spremao kao cijelina i pretraga bi radila samo za potpuno iste izraze, što bi značajno smanjilo učinkovitost pretrage.

# Završni zadatak - filmovi
### 30. Elasticsearch vs SQL LIKE
Elasticsearch ima prednost nad SQL LIKE pretragom jer koristi invertirani indeks koji omogućuje vrlo brzu pretragu velikih količina teksta.
Za razliku od SQL LIKE '%tekst%' koji mora prolaziti kroz svaki zapis, Elasticsearch može odmah pronaći relevantne dokumente. Taakođer, Elasticsearch koristi analyzere koji omogućuju pretragu bez obzira na velika/mala slova i dijakritike. Podržava i rangiranje rezultata (_score), što znači da najrelevantniji rezultati dolaze prvi.
SQL LIKE vraća samo točne podudarnosti bez razumijevanja jezika.
Elasticsearch omogućuje napredne opcije kao što su fuzzy pretraga, sinonimi i kombinacija uvjeta.
Osim toga, Elasticsearch je distribuiran sustav i može se skalirati na više servera, dok SQL baze imaju ograničenja u skaliranju za ovakve tipove pretrage.





