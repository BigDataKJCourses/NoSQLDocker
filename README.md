# NoSQLDocker - Workshop Environment

To repozytorium zawiera gotowe konfiguracje środowisk kontenerowych przeznaczone do pracy z popularnymi systemami baz danych NoSQL oraz środowiskiem programistycznym Node.js. 

Projekt jest idealny do celów warsztatowych, testowych oraz lokalnego developmentu.

## 📂 Struktura Projektu

Struktura opiera się na plikach `compose.yml` podzielonych na moduły tematyczne w katalogu `Docker/config/`.

### 1. Bazy Danych i Analityka
* **Elasticsearch & Kibana**: Stos w wersji 9.2.0 skonfigurowany jako pojedynczy węzeł (single-node).
* **Redis Stack**: Wersja 7.4.0-v7 z aktywnym interfejsem graficznym na porcie 8001.
* **Cassandra**: Baza kolumnowa w wersji 5.0.5.
* **Neo4j**: Grafowa baza danych (v5.26.14) z predefiniowanym hasłem `grap#_d4t4`.
* **MongoDB**:
    * **Simple**: Klasyczna instancja z kontem admin/admin.
    * **Complex (Sharding)**: Zaawansowana architektura zawierająca 3 serwery konfiguracji, 2 shardy (repliki) oraz router `mongos`.

### 2. Środowisko Programistyczne
* **Node.js (node-dev)**: Kontener oparty na obrazie `node:25`.
* **Mapowanie Wolumenów**: Projekty są montowane z lokalnej ścieżki `${HOME}/Docker/Node/projects` do katalogu `/projects` wewnątrz kontenera.
* **Uprawnienia**: Środowisko korzysta ze zmiennych `${UID}` i `${GID}` dla zapewnienia zgodności uprawnień plików między hostem a kontenerem.

### 3. Narzędzia i VS Code
* **SQLTools**: Predefiniowane połączenie dla bazy Cassandra w pliku ustawień `.vscode/settings.json` (host: localhost, port: 9042).

---

## 🚀 Szybki Start

1. **Konfiguracja zmiennych**:
   Upewnij się, że pliki `.env` w folderach projektów (np. `Docker/config/redis/`) zawierają Twój identyfikator użytkownika:
```env
UID=1000
GID=1000
```

2. **Uruchomienie usługi**:
   Wejdź do katalogu z wybraną konfiguracją i uruchom:

```bash
docker-compose up -d
```

3. **Porty Usług**:

- Elasticsearch: 9200 
- Kibana: 5601 
- Redis Stack: 6379 (Baza) / 8001 (Panel WWW) 
- MongoDB: 27017 
- Neo4j: 7474 (HTTP) / 7687 (Bolt) 
- Cassandra: 9042