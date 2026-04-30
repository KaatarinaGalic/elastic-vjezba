# Elasticsearch vježba

## Opis projekta
Ovaj projekt prikazuje rad s Elasticsearchom i Kibanom kroz praktične zadatke.
Cilj je bio kreirati indeks, ubaciti podatke, izvršavati različite vrste upita
(match, term, range, bool) te raditi agregacije i analizu teksta.

## Pokretanje projekta
Pokrenuti Elasticsearch i Kibanu:

docker compose up -d

## Provjera da sustav radi:
curl http://localhost:9200
curl http://localhost:9200/_cat/health?v

## Provjera pokrenutih kontejnera:
docker compose ps
Oba servisa (elasticsearch i kibana) moraju imati status "running".

## Servisi
- Elasticsearch: http://localhost:9200
- Kibana: http://localhost:5601

## Sadržaj repozitorija
- docker-compose.yml → konfiguracija okruženja
- queries.http → svi Elasticsearch upiti
- screenshots/ → dokazi izvršavanja zadataka
- ODGOVORI.md → teorijski odgovori
- README.md → opis projekta

## Funkcionalnosti
- kreiranje indeksa s mappingom i analyzerom
- unos podataka pomoću Bulk API-ja
- full-text pretraga (match query)
- filtriranje (term, range, bool query)
- analiza teksta (_analyze)
- agregacije (group by, avg, max)

## Napomena
Projekt je rađen postepeno kroz više commitova.