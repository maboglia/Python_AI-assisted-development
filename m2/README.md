# Modulo 2 – Architettura backend e API REST

18 ore

Teoria + laboratorio

FastAPI · Pydantic · REST · OpenAPI

## 1. Obiettivi formativi

Il modulo introduce gli studenti allo sviluppo di servizi backend attraverso la progettazione e realizzazione di API REST con Python e FastAPI.

L'obiettivo è comprendere il funzionamento dell'architettura client-server, il ruolo del protocollo HTTP e le convenzioni che regolano la progettazione delle API. Gli studenti impareranno a esporre funzionalità applicative attraverso endpoint REST, gestire richieste e risposte in formato JSON, validare i dati in ingresso e documentare automaticamente i servizi realizzati.

Al termine del modulo gli studenti saranno in grado di:

- Comprendere il funzionamento della comunicazione tra client e server.
- Interpretare richieste HTTP e costruire risposte coerenti.
- Progettare API REST secondo convenzioni consolidate.
- Realizzare endpoint con FastAPI.
- Gestire parametri, payload JSON e modelli di risposta.
- Validare e serializzare dati utilizzando Pydantic.
- Gestire errori applicativi e codici di stato HTTP.
- Utilizzare Swagger UI e OpenAPI per documentare e testare le API.
- Realizzare un servizio backend con operazioni CRUD.

# 2. Micro-progettazione didattica

La distribuzione proposta prevede 6 unità didattiche da 3 ore ciascuna.

## Distribuzione delle 18 ore

01

Architettura client-server e protocollo HTTP

Richieste, risposte, metodi, header e status code.

3 h

02

JSON e progettazione REST

Risorse, URI, convenzioni e operazioni CRUD.

3 h

03

Introduzione a FastAPI

Installazione, applicazione, routing ed endpoint.

3 h

04

Parametri, request body e response model

Path, query string, payload e modelli Pydantic.

3 h

05

Validazione, errori e documentazione

Pydantic, gestione eccezioni, OpenAPI e Swagger UI.

3 h

06

Laboratorio: sviluppo API REST CRUD

Realizzazione, test e verifica di una API completa.

3 h

# 3. Sviluppo dettagliato delle lezioni

## Lezione 1 – Architettura client-server e protocollo HTTP

3 ore

### Contenuti teorici

1\. Architettura client-server

- Introduzione al modello client-server.
- Ruolo del frontend e del backend.
- Comunicazione tra applicazioni distribuite.
- Separazione delle responsabilità.
- Il backend come fornitore di servizi e dati.
- Introduzione al concetto di API (Application Programming Interface).

2\. Il protocollo HTTP

- Caratteristiche del protocollo HTTP.
- Comunicazione request-response.
- Struttura di una richiesta HTTP:
  - Metodo.
  - URL.
  - Header.
  - Body.
- Struttura di una risposta HTTP:
  - Status code.
  - Header.
  - Body.
- Introduzione a HTTPS e al ruolo di TLS.

3\. Metodi HTTP

| Metodo | Funzione          | Utilizzo                |
| ------ | ----------------- | ----------------------- |
| GET    | Lettura           | Recuperare risorse      |
| POST   | Creazione         | Inserire nuove risorse  |
| PUT    | Sostituzione      | Aggiornare una risorsa  |
| PATCH  | Modifica parziale | Aggiornare alcuni campi |
| DELETE | Eliminazione      | Rimuovere una risorsa   |

4\. Status code

- 1xx: informazioni.
- 2xx: operazioni completate correttamente.
- 3xx: reindirizzamenti.
- 4xx: errori nella richiesta del client.
- 5xx: errori del server.

Status code principali:

- 200 OK.
- 201 Created.
- 204 No Content.
- 400 Bad Request.
- 401 Unauthorized.
- 403 Forbidden.
- 404 Not Found.
- 422 Unprocessable Content (utilizzato da FastAPI per errori di validazione).
- 500 Internal Server Error.

5\. Header HTTP

- Content-Type.
- Accept.
- Authorization.
- User-Agent.
- Content-Length.
- Differenza tra header della richiesta e della risposta.

### Esempi pratici

Analisi di una richiesta HTTP:

```
GET /api/products/10 HTTP/1.1
Host: localhost:8000
Accept: application/json
```

Esempio di risposta:

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "id": 10,
    "name": "Notebook",
    "price": 799.90
}
```

### Laboratorio

- Utilizzo del browser per analizzare le richieste HTTP.
- Introduzione agli strumenti Developer Tools.
- Utilizzo di Postman oppure Thunder Client per inviare richieste HTTP.
- Analisi di richieste GET e POST.
- Interpretazione degli status code restituiti dal server.

### Risultato atteso

Lo studente comprende come avviene la comunicazione tra client e backend e sa interpretare una richiesta e una risposta HTTP.

## Lezione 2 – JSON e progettazione delle API REST

3 ore

### Contenuti teorici

1\. Il formato JSON

- Introduzione a JavaScript Object Notation.
- Struttura di un documento JSON.
- Oggetti e array.
- Tipi di dato supportati:
  - Stringhe.
  - Numeri.
  - Boolean.
  - Null.
  - Oggetti.
  - Array.
- Differenza tra JSON e dizionari Python.
- Serializzazione e deserializzazione.
- Utilizzo del modulo `json` di Python.

2\. Introduzione alle API REST

- Significato di REST (Representational State Transfer).
- Principi architetturali fondamentali.
- Client-server.
- Stateless.
- Risorse e rappresentazioni.
- Identificazione delle risorse attraverso URI.
- Utilizzo dei metodi HTTP.
- Separazione tra risorsa e operazione.

3\. Progettazione delle risorse

Esempio: gestione di un catalogo prodotti.

| Endpoint       | Metodo | Operazione             |
| -------------- | ------ | ---------------------- |
| `/products`    | GET    | Elenco prodotti        |
| `/products/10` | GET    | Dettaglio prodotto     |
| `/products`    | POST   | Creazione prodotto     |
| `/products/10` | PUT    | Aggiornamento completo |
| `/products/10` | PATCH  | Aggiornamento parziale |
| `/products/10` | DELETE | Eliminazione           |

4\. Convenzioni REST

- Utilizzo di nomi al plurale per le risorse.
- Identificativi nelle URI.
- Utilizzo appropriato dei metodi HTTP.
- Coerenza nella struttura delle risposte.
- Differenza tra operazioni safe e idempotenti.
- Statelessness e gestione dello stato applicativo.
- Evitare endpoint basati su nomi di funzioni o azioni.

### Esempi pratici

Struttura JSON di un prodotto:

```
{
    "id": 1,
    "name": "Monitor",
    "price": 249.90,
    "available": true,
    "categories": [
        "hardware",
        "periferiche"
    ]
}
```

Conversione JSON/Python:

```
import jsonproduct = {    "id": 1,    "name": "Monitor",    "price": 249.90}# Serializzazionejson_data = json.dumps(product, indent=4)print(json_data)# Deserializzazionedata = json.loads(json_data)print(data["name"])
```

### Laboratorio

Progettazione su carta di una API REST per la gestione di una rubrica contatti.

Gli studenti dovranno individuare:

- Le risorse principali.
- Gli identificativi.
- Gli endpoint.
- I metodi HTTP.
- Le strutture JSON di richiesta e risposta.

### Risultato atteso

Lo studente sa progettare una semplice API REST, identificando risorse, URI, metodi HTTP e strutture JSON.

## Lezione 3 – Introduzione a FastAPI e organizzazione degli endpoint

3 ore

### Contenuti teorici

1\. Introduzione a FastAPI

- Cos'è FastAPI.
- Caratteristiche principali.
- Differenze generali rispetto a Flask e Django.
- FastAPI e il framework Starlette.
- Integrazione con Pydantic.
- Programmazione asincrona e supporto ad `async`/`await`.
- Casi d'uso nello sviluppo di backend e servizi AI.

2\. Configurazione dell'ambiente

- Creazione di un ambiente virtuale Python.
- Installazione delle dipendenze.
- Utilizzo di pip.
- Avvio del server di sviluppo Uvicorn.
- Struttura iniziale del progetto.

Installazione:

```
python -m venv .venv

source .venv/bin/activate

pip install "fastapi[standard]"
```

3\. Prima applicazione FastAPI

Creazione del file `main.py`.

```
from fastapi import FastAPIapp = FastAPI(    title="Product API",    description="Prima API REST con FastAPI",    version="1.0.0")@app.get("/")def home():    return {        "message": "Benvenuto nella Product API"    }@app.get("/products")def get_products():    return [        {"id": 1, "name": "Notebook"},        {"id": 2, "name": "Monitor"}    ]
```

Avvio:

```
fastapi dev main.py
```

4\. Organizzazione degli endpoint

- Decoratori FastAPI.
- Associazione tra URL e funzioni Python.
- Gestione delle richieste GET e POST.
- Funzioni sincrone e asincrone.
- Restituzione di dizionari, liste e oggetti Python.
- Risposte JSON automatiche.
- Introduzione all'organizzazione del codice in moduli.

### Laboratorio

Realizzazione della prima applicazione backend:

- Creazione progetto.
- Configurazione ambiente virtuale.
- Installazione FastAPI.
- Creazione degli endpoint `/` e `/products`.
- Avvio del server.
- Test delle richieste tramite browser e client HTTP.

### Risultato atteso

Lo studente sa configurare un progetto FastAPI e realizzare semplici endpoint HTTP che restituiscono dati in formato JSON.

## Lezione 4 – Parametri, request body e response model

3 ore

### Contenuti teorici

1\. Parametri di percorso (Path Parameters)

- Parametri dinamici nelle URI.
- Identificazione delle risorse.
- Conversione automatica dei tipi.

Esempio:

```
@app.get("/products/{product_id}")def get_product(product_id: int):    return {        "id": product_id,        "name": "Notebook"    }
```

2\. Parametri query string

- Differenza tra path e query parameters.
- Parametri obbligatori e opzionali.
- Valori predefiniti.
- Filtri e ordinamento.

Esempio:

```
@app.get("/products")def get_products(    category: str | None = None,    limit: int = 10):    return {        "category": category,        "limit": limit    }
```

Richiesta:

```
GET /products?category=hardware&limit=5
```

3\. Request Body

- Invio di dati dal client al server.
- Differenza tra parametri URL e body.
- Utilizzo del formato JSON.
- Ricezione di dati tramite modelli Python.
- Creazione di risorse attraverso POST.

4\. Response Model

- Definizione della struttura della risposta.
- Utilizzo di `response_model`.
- Controllo dei dati restituiti.
- Separazione tra dati interni e dati pubblici.
- Esclusione di attributi non destinati al client.

### Esempio pratico

```
from pydantic import BaseModelclass Product(BaseModel):    name: str    price: float    available: bool = True@app.post("/products", response_model=Product)def create_product(product: Product):    return product
```

Richiesta POST:

```
{
    "name": "Mouse",
    "price": 29.90,
    "available": true
}
```

### Laboratorio

Estensione della Product API:

- Endpoint GET con identificativo.
- Endpoint GET con filtri.
- Endpoint POST per inserire prodotti.
- Utilizzo di request body.
- Definizione di modelli di risposta.

### Risultato atteso

Lo studente sa ricevere e gestire parametri HTTP, acquisire dati JSON e definire strutture di risposta attraverso FastAPI.

## Lezione 5 – Validazione, gestione degli errori e documentazione

3 ore

### Contenuti teorici

1\. Pydantic e validazione dei dati

- Introduzione a Pydantic.
- Definizione di modelli attraverso `BaseModel`.
- Type hints e controllo dei tipi.
- Campi obbligatori e opzionali.
- Valori predefiniti.
- Vincoli sui dati.
- Validazione automatica dei request body.
- Serializzazione dei modelli.

Esempio:

```
from pydantic import BaseModel, Fieldclass Product(BaseModel):    name: str = Field(        min_length=2,        max_length=100    )    price: float = Field(        gt=0    )    quantity: int = Field(        ge=0    )
```

2\. Gestione degli errori

- Differenza tra errori HTTP e errori applicativi.
- Utilizzo di `HTTPException`.
- Status code appropriati.
- Messaggi di errore.
- Gestione delle risorse non trovate.
- Validazione degli input non corretti.
- Introduzione agli exception handler personalizzati.

Esempio:

```
from fastapi import HTTPException@app.get("/products/{product_id}")def get_product(product_id: int):    product = None    if product is None:        raise HTTPException(            status_code=404,            detail="Prodotto non trovato"        )    return product
```

3\. Documentazione OpenAPI

- Cos'è OpenAPI.
- Specifica delle API.
- Generazione automatica della documentazione.
- Descrizione di endpoint e parametri.
- Schemi di richiesta e risposta.
- Codici di risposta.
- Interazione con Swagger UI.

4\. Swagger UI

- Accesso alla documentazione interattiva.
- Visualizzazione degli endpoint.
- Esecuzione delle richieste.
- Inserimento dei parametri.
- Test dei request body.
- Analisi delle risposte.

FastAPI espone automaticamente:

- `/docs`: Swagger UI.
- `/redoc`: documentazione alternativa.
- `/openapi.json`: specifica OpenAPI.

5\. Convenzioni progettuali

- Coerenza degli endpoint.
- Gestione uniforme degli errori.
- Paginazione.
- Filtri.
- Ordinamento.
- Limiti sui risultati restituiti.

### Esempio pratico: paginazione

```
@app.get("/products")def get_products(    skip: int = 0,    limit: int = 10):    return {        "skip": skip,        "limit": limit,        "items": []    }
```

Richiesta:

```
GET /products?skip=10&limit=5
```

### Laboratorio

- Introduzione dei vincoli Pydantic.
- Test di richieste valide e non valide.
- Gestione di errori 404 e 422.
- Consultazione della documentazione Swagger.
- Test degli endpoint direttamente dal browser.

### Risultato atteso

Lo studente sa validare i dati in ingresso, gestire gli errori e utilizzare la documentazione automatica per testare e descrivere una API REST.

## Lezione 6 – Laboratorio: realizzazione di una API REST CRUD

3 ore

### Obiettivo

Realizzare una piccola applicazione backend con FastAPI, applicando le conoscenze acquisite nelle precedenti lezioni.

Progetto: Product Management API

L'applicazione dovrà consentire la gestione di un catalogo prodotti.

### Funzionalità richieste

| Metodo | Endpoint         | Funzionalità           |
| ------ | ---------------- | ---------------------- |
| GET    | `/products`      | Elenco prodotti        |
| GET    | `/products/{id}` | Dettaglio prodotto     |
| POST   | `/products`      | Inserimento prodotto   |
| PUT    | `/products/{id}` | Aggiornamento prodotto |
| DELETE | `/products/{id}` | Eliminazione prodotto  |

### Struttura del progetto

```
product_api/
│
├── main.py
│
├── models/
│   └── product.py
│
├── data/
│   └── products.py
│
└── requirements.txt
```

Per il laboratorio si utilizzerà inizialmente una collezione Python in memoria, senza introdurre ancora un database relazionale.

### Modello dati

```
from pydantic import BaseModel, Fieldclass Product(BaseModel):    id: int | None = None    name: str = Field(        min_length=2,        max_length=100    )    price: float = Field(        gt=0    )    quantity: int = Field(        ge=0    )
```

### Attività operative

1. Creazione e configurazione del progetto.
2. Definizione del modello Product con Pydantic.
3. Realizzazione dell'endpoint GET per l'elenco.
4. Realizzazione dell'endpoint GET per il dettaglio.
5. Realizzazione dell'endpoint POST per l'inserimento.
6. Realizzazione degli endpoint PUT e DELETE.
7. Gestione delle risorse non trovate.
8. Validazione dei dati in ingresso.
9. Verifica degli status code.
10. Test e documentazione attraverso Swagger UI.

### Estensioni facoltative

Per gli studenti che completano anticipatamente il progetto:

- Aggiunta di filtri per nome e prezzo.
- Implementazione della paginazione.
- Introduzione dell'ordinamento.
- Gestione di codici di risposta personalizzati.
- Separazione tra modello di creazione, aggiornamento e risposta.

### Risultato atteso

Ogni studente realizza una API REST funzionante, documentata e testabile, capace di gestire le operazioni CRUD e validare i dati ricevuti.

# 4. Materiali didattici e strumenti

## Tecnologie e strumenti

[Python logo Icons, Logos, Symbols – Free Download PNG, SVG](https://images.openai.com/static-rsc-4/DmsB8FS-GP7uphH6D36okAKArZlBuv18j7laB7MGQztxtnElBP3iuvRtFFsgJN3_CMjTR795lNP5nkz0C0O5HRM_6vUhOfMDScUzQErc9yfIrgdVyj38VLAdNtbsn3vWhJAUhRcvYx9LUssqXM5zJvcGr4rSiP0dNojMqKdTlnc?purpose=inline)

Python 3

Linguaggio di programmazione

[Fastapi Logo PNG Vector (SVG) Free Download](https://images.openai.com/static-rsc-4/3234HTtfzpYlSxRStZofhOPAbMcq24eqzXzCmLLM7WIVxLsZgXUEDAHX5FEZ6_pwX4f6_FFhefFmdZIf9HCiPALAISHFx3ad7X1_68DqY8SxTzcwx-svS4XGrPLCDSWT5g-kyGw2JwSjoIP_469N7hdrYI7MqKc-P4NvzXiUa8U?purpose=inline)

FastAPI

Framework per lo sviluppo di API REST

[Pydantic (@pydantic) on X](https://images.openai.com/static-rsc-4/xfsAV07-hZsEr3M35w_gkFQQ1MA1JdX8TRZMJaUUS-ZIx55JQUE6PKNOI6tR_ueM4WvoP62BssPJESTi4w5YP5uuQtSuuYyLjGfQhOnHlmtrm1MJACzE59vVHuSBoxYdOZ8SNWWci1mhslxjpoEnNGjY3GpbYU2agTQSFqNYrDE?purpose=inline)

Pydantic

Validazione e serializzazione dei dati

[Swagger Logo PNG Vector (SVG) Free Download](https://images.openai.com/static-rsc-4/DZMUKSvrP0DxUSnLmIuFJy_oanGakoT1xYpFcjU_0p0hhZvGKh6oQXi3K_gtjtDcLqmkv8Rz1kgpG-MCvVGXB4SyxYmt-ebmmKnjCK6iwmLkrtaEX8jfyhiI_cA9-w0YaQHvII5MM3ACSbn4H_0S7VUQFBH_Cyzgv4xpMCIM-js?purpose=inline)

OpenAPI / Swagger UI

Documentazione e test delle API

[Visionco | services](https://images.openai.com/static-rsc-4/bDTDp-kPgMFGVhrV9CFYRBVY_fSLVnXtPoOpKhXLI7R_6Dwzy0vZ9Fy3dm60OSheomIpV9xh6oPBr_3yHRbF-nji9QjXWEQTk6IwrM2RFuYXFIVNtmk21msDsgCUnZAnB1dL215LsGFTPjnE9Ru9RMPG12V05n6oicPO-am4NKI?purpose=inline)

Postman / Thunder Client

Test delle richieste HTTP

## Risorse di riferimento

- [FastAPI – Documentazione ufficiale](https://fastapi.tiangolo.com/?utm_source=chatgpt.com)
- [Pydantic – Documentazione ufficiale](https://docs.pydantic.dev/latest/?utm_source=chatgpt.com)
- [OpenAPI Specification](https://www.openapis.org/?utm_source=chatgpt.com)
- [MDN – HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP?utm_source=chatgpt.com)
- [Postman](https://www.postman.com/?utm_source=chatgpt.com)

# 5. Verifica degli apprendimenti

La valutazione può essere effettuata attraverso prove pratiche e verifiche durante il laboratorio.

| Area di competenza | Modalità di verifica                    |
| ------------------ | --------------------------------------- |
| Protocollo HTTP    | Interpretazione di richieste e risposte |
| Progettazione REST | Definizione di risorse ed endpoint      |
| FastAPI            | Realizzazione di endpoint               |
| Pydantic           | Definizione e validazione dei modelli   |
| Gestione errori    | Restituzione di status code appropriati |
| OpenAPI            | Consultazione e utilizzo di Swagger UI  |
| CRUD               | Realizzazione di una API funzionante    |

Prova pratica conclusiva: realizzazione di una API REST per la gestione di una risorsa a scelta (prodotti, contatti, libri o corsi), con almeno quattro operazioni CRUD, validazione degli input e documentazione automatica.

# 6. Collegamento con i moduli successivi

Il modulo costituisce il passaggio dalla programmazione Python alla realizzazione di applicazioni backend strutturate.

La progressione didattica del corso può essere organizzata così:

Modulo 1 · 16 h

Python e programmazione a oggetti

Sintassi, funzioni, classi, oggetti, moduli e organizzazione del codice.

Modulo 2 · 18 h

Architettura backend e API REST

HTTP, REST, FastAPI, Pydantic, CRUD e documentazione OpenAPI.

Modulo successivo

Persistenza dei dati e database

Integrazione delle API con database relazionali, ORM e gestione della persistenza.

Moduli successivi

Sicurezza, testing e AI integration

Autenticazione, autorizzazione, test automatici e integrazione di servizi AI.

## 7. Indicazioni metodologiche per il docente

Per rendere il percorso efficace in sole 18 ore, suggerisco di mantenere un unico progetto evolutivo: la Product API.

Ogni lezione aggiunge una funzionalità al progetto precedente:

- Lezione 1: comprendere il protocollo HTTP.
- Lezione 2: progettare le risorse REST.
- Lezione 3: creare il primo server FastAPI.
- Lezione 4: gestire input e output.
- Lezione 5: validare e documentare.
- Lezione 6: completare il CRUD.

Una scelta didattica importante: non introdurrei ancora SQLAlchemy, database, autenticazione JWT o Docker. Sono argomenti che meritano spazio nei moduli successivi. In questo modulo è fondamentale che gli studenti comprendano bene il ciclo request-response e la progettazione delle API.

Inoltre, manterrei il laboratorio su dati in memoria: permette di concentrarsi sull'architettura REST senza sovraccaricare gli studenti con la gestione della persistenza.

Il risultato finale sarà una prima API backend realmente funzionante, che potrà essere progressivamente evoluta nei moduli successivi.