# Informačný systém pre nemocnicu

Tento repozitár obsahuje jednoduchú ukážku zdravotníckeho informačného systému pozostávajúcu z:

- **backendu** vo Flasku (Python, REST API, práca s CSV súbormi / databázou),
- **frontendu** v JavaScripte/TypeScripte (webové UI),

---

## Štruktúra projektu

```text
README.md
backend/
  app.py
  requirements.txt
  files/
    __init__.py
    api.py
    auth.py
    models.py
    pds_api.py
    queries.py
    test_routes.py
    views.py
  templates/
data/
  M_DIAGNOZA.csv
  M_HOSPITALIZACIA.csv
  M_LIEK.csv
  M_MIESTNOST.csv
  M_OBJEDNAVKA.csv
  M_OSOBA.csv
  M_PACIENT.csv
  M_POUZIVATEL.csv
  M_RECEPT.csv
  M_SKLAD_LIEKOV.csv
  M_SPECIALIZACIA.csv
  M_ZAMESTNANEC.csv
  M_ZDRAVOTNY_ZAZNAM.csv
  M_ZMENA.csv
frontend/
  package.json
  README.md
  tsconfig.json
  public/
  src/
vystupy/
  vystupy.sql
```

### Backend (Flask)

Adresár [backend](backend) obsahuje serverovú časť aplikácie postavenú na microframeworku **Flask**:

- Hlavný spúšťací súbor: [`backend/app.py`](backend/app.py)  
- Závislosti Python backendu: [`backend/requirements.txt`](backend/requirements.txt)  
- Aplikačná logika a API:
  - [`backend/files/api.py`](backend/files/api.py) – implementácia REST endpointov
  - [`backend/files/auth.py`](backend/files/auth.py) – autentifikácia a autorizácia
  - [`backend/files/models.py`](backend/files/models.py) – dátové modely / doménové entity
  - [`backend/files/queries.py`](backend/files/queries.py) – prístup k dátam, dotazy nad DB
  - [`backend/files/pds_api.py`](backend/files/pds_api.py) – integrácia s externým PDS rozhraním (ak je dostupné)
  - [`backend/files/views.py`](backend/files/views.py) – view funkcie / routy
- Šablóny HTML (ak sa používajú): [backend/templates](backend/templates)  
- Jednotkové / integračné testy backendu: [`backend/files/test_routes.py`](backend/files/test_routes.py)

Backend pracuje s dátami z priečinka [data](data) a podľa potreby ich načítava, filtruje a vystavuje cez API.

### Frontend

Adresár [frontend](frontend) obsahuje klientsku (webovú) časť aplikácie:

- Konfigurácia a závislosti: [`frontend/package.json`](frontend/package.json)
- TypeScript konfigurácia: [`frontend/tsconfig.json`](frontend/tsconfig.json)
- Verejné statické súbory: [`frontend/public`](frontend/public)
- Zdrojový kód frontendu: [`frontend/src`](frontend/src)

Frontend typicky komunikuje s backendom cez HTTP/JSON API a vizualizuje zdravotnícke dáta (pacienti, diagnózy, hospitalizácie, lieky atď.).

### Dátové súbory

Adresár [data](data) obsahuje CSV súbory reprezentujúce jednotlivé entity zdravotníckeho systému, napr.:

- `M_PACIENT.csv` – informácie o pacientoch
- `M_DIAGNOZA.csv` – diagnózy
- `M_HOSPITALIZACIA.csv` – záznamy o hospitalizáciách
- `M_LIEK.csv`, `M_SKLAD_LIEKOV.csv` – lieky a sklad
- `M_ZDRAVOTNY_ZAZNAM.csv` – zdravotná dokumentácia
- `M_ZAMESTNANEC.csv`, `M_SPECIALIZACIA.csv` – zdravotnícky personál

Tieto súbory môžu slúžiť ako zdroj dát pre backend, alebo ako vstup pri napĺňaní databázy.

### SQL výstupy

Adresár [vystupy](vystupy) obsahuje SQL skript:

- [`vystupy/vystupy.sql`](vystupy/vystupy.sql) – príklady dotazov alebo návrh databázy nad rovnakým dátovým modelom.

---

## Lokálne spustenie

### 1. Príprava backendu

1. Prejdite do priečinka backend:

   ```bash
   cd backend
   ```

2. Vytvorte a aktivujte virtuálne prostredie (odporúčané):

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Linux/macOS
   # alebo
   .venv\Scripts\activate     # Windows
   ```

3. Nainštalujte závislosti:

   ```bash
   pip install -r requirements.txt
   ```

4. Spustite backend (konkrétny príkaz môže byť v `app.py`):

   ```bash
   python app.py
   ```

Backend by mal bežať napr. na `http://localhost:5000` (alebo inom porte definovanom v kóde).

### 2. Príprava frontendu

1. V novom termináli prejdite do priečinka frontend:

   ```bash
   cd frontend
   ```

2. Nainštalujte závislosti:

   ```bash
   npm install
   # alebo
   yarn install
   ```

3. Spustite vývojový server:

   ```bash
   npm start
   # alebo
   yarn start
   ```

Frontend bude bežať typicky na `http://localhost:3000` a bude pristupovať k backend API.

---


## Konfigurácia a prispôsobenie

- Konfiguráciu databázy, ciest k CSV súborom a prístupových údajov je možné upraviť v súboroch v priečinku [`backend/files`](backend/files) (najmä [`models.py`](backend/files/models.py), [`queries.py`](backend/files/queries.py), [`auth.py`](backend/files/auth.py)).
- Frontend je možné prispôsobiť v priečinku [`frontend/src`](frontend/src) (komponenty, služby, volania API).
