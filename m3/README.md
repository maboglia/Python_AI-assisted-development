# Modulo 3 – Database e persistenza dei dati

16 ore

Teoria + laboratorio

Python Backend

## 1. Obiettivi formativi

Il modulo introduce la gestione della persistenza dei dati nelle applicazioni backend Python, partendo dai fondamenti del modello relazionale e del linguaggio SQL, fino all'integrazione di un database PostgreSQL attraverso l'ORM SQLAlchemy.

Gli studenti impareranno a progettare e interrogare un database relazionale, a rappresentare le entità applicative mediante classi Python e a gestire le operazioni di inserimento, lettura, modifica e cancellazione dei dati attraverso un livello di persistenza integrato nell'applicazione.

Particolare attenzione sarà dedicata alla gestione delle relazioni tra entità, alle transazioni, alla gestione degli errori e all'evoluzione dello schema del database mediante Alembic, evitando interventi manuali e ricreazioni del database durante lo sviluppo.

Al termine del modulo gli studenti saranno in grado di collegare un'API REST realizzata con FastAPI a un database PostgreSQL, organizzando correttamente il livello di accesso ai dati.

## 2. Prerequisiti

- Conoscenza della sintassi Python e della programmazione a oggetti.
- Conoscenza delle funzioni, delle classi e dei moduli Python.
- Conoscenza di base dell'architettura client-server e delle API REST.
- Familiarità con JSON e con i modelli Pydantic introdotti nel modulo precedente.
- Conoscenze di base di SQL (costituiscono un vantaggio, ma non sono indispensabili).

## 3. Micro-progettazione didattica

### Unità 3.1 – Fondamenti di database relazionali (2 ore)

Contenuti

- Introduzione ai database relazionali e al modello relazionale.
- Tabelle, righe, colonne e domini dei dati.
- Tipi di dato e rappresentazione delle informazioni.
- Chiavi primarie (PRIMARY KEY) e chiavi esterne (FOREIGN KEY).
- Vincoli di integrità: NOT NULL, UNIQUE, CHECK e DEFAULT.
- Relazioni tra tabelle: uno-a-uno, uno-a-molti e molti-a-molti.
- Concetto di normalizzazione: prima, seconda e terza forma normale.
- Progettazione concettuale e logica di un database.

Testo guida per la lezione

Un database relazionale permette di organizzare le informazioni attraverso tabelle collegate tra loro. Ogni tabella rappresenta un'entità del dominio applicativo, mentre le righe rappresentano le singole istanze di quell'entità.

In un'applicazione backend, ad esempio un sistema di gestione dei corsi, possiamo individuare alcune entità fondamentali:

- Studente
- Corso
- Docente
- Iscrizione

Le informazioni non devono essere duplicate inutilmente. La relazione tra le tabelle consente di mantenere la coerenza dei dati e di rappresentare correttamente i legami tra le entità.

La chiave primaria identifica univocamente ogni record, mentre la chiave esterna permette di collegare una tabella a un'altra.

La normalizzazione consente di ridurre le ridondanze e prevenire anomalie nelle operazioni di inserimento, modifica e cancellazione.

Esempio pratico

Progettazione di un database per la gestione degli studenti e dei corsi:

```
CREATE TABLE studenti (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL
);

CREATE TABLE corsi (
    id SERIAL PRIMARY KEY,
    titolo VARCHAR(150) NOT NULL,
    durata_ore INTEGER CHECK (durata_ore > 0)
);

CREATE TABLE iscrizioni (
    id SERIAL PRIMARY KEY,
    studente_id INTEGER REFERENCES studenti(id),
    corso_id INTEGER REFERENCES corsi(id),
    data_iscrizione DATE DEFAULT CURRENT_DATE
);
```

Attività laboratoriale

- Individuazione delle entità di un dominio applicativo.
- Definizione degli attributi e delle chiavi.
- Disegno di uno schema relazionale.
- Identificazione delle relazioni e dei vincoli di integrità.

### Unità 3.2 – SQL e PostgreSQL (3 ore)

Contenuti

- Introduzione a PostgreSQL e al modello client-server del database.
- Creazione e gestione di database e tabelle.
- Tipi di dato principali di PostgreSQL.
- Inserimento dei dati: INSERT.
- Consultazione dei dati: SELECT.
- Filtri e ordinamento: WHERE, ORDER BY, LIMIT.
- Operatori logici e operatori di confronto.
- JOIN: INNER JOIN, LEFT JOIN.
- Funzioni di aggregazione: COUNT, SUM, AVG, MIN, MAX.
- Raggruppamento dei dati: GROUP BY e HAVING.
- Modifica e cancellazione: UPDATE e DELETE.
- Subquery e query annidate.
- Introduzione alle transazioni SQL.

Testo guida per la lezione

Prima di utilizzare un ORM, è importante comprendere come il database viene interrogato direttamente attraverso SQL.

PostgreSQL è un database relazionale open source particolarmente adatto allo sviluppo di applicazioni backend professionali. Supporta funzionalità avanzate, vincoli di integrità, transazioni e un sistema di gestione dei dati robusto.

Le operazioni SQL possono essere suddivise in quattro categorie principali:

- DDL: definizione della struttura del database.
- DML: inserimento e modifica dei dati.
- DQL: interrogazione dei dati.
- DCL: gestione dei permessi e degli accessi.

L'attenzione sarà concentrata soprattutto sulle operazioni di interrogazione e manipolazione dei dati.

Esempi pratici

Consultazione degli studenti:

```
SELECT *
FROM studenti
ORDER BY nome;
```

Ricerca delle iscrizioni con JOIN:

```
SELECT
    s.nome,
    c.titolo,
    i.data_iscrizione
FROM iscrizioni i
JOIN studenti s
    ON i.studente_id = s.id
JOIN corsi c
    ON i.corso_id = c.id;
```

Conteggio degli iscritti per corso:

```
SELECT
    c.titolo,
    COUNT(i.id) AS numero_iscritti
FROM corsi c
LEFT JOIN iscrizioni i
    ON c.id = i.corso_id
GROUP BY c.id, c.titolo
ORDER BY numero_iscritti DESC;
```

Modifica di un record:

```
UPDATE studenti
SET email = 'mario.rossi@example.com'
WHERE id = 1;
```

Attività laboratoriale

Realizzazione di uno schema PostgreSQL per la gestione dei corsi, popolamento delle tabelle con dati di esempio e sviluppo di query per ottenere informazioni aggregate e relazioni tra entità.

### Unità 3.3 – ORM SQLAlchemy: mapping e persistenza (4 ore)

Contenuti

- Introduzione agli ORM (Object Relational Mapping).
- Vantaggi e limiti dell'approccio ORM.
- Installazione e configurazione di SQLAlchemy.
- Differenza tra SQLAlchemy Core e SQLAlchemy ORM.
- Definizione della connessione al database.
- Creazione della classe Base e dei modelli.
- Mapping tra classi Python e tabelle relazionali.
- Colonne, tipi di dato e vincoli.
- Generazione delle tabelle.
- Engine, Connection e Session.
- Operazioni CRUD attraverso l'ORM.
- Query e recupero dei risultati.
- Gestione del ciclo di vita della sessione.

Testo guida per la lezione

Nello sviluppo di applicazioni backend, il database rappresenta il livello responsabile della conservazione permanente delle informazioni.

L'applicazione Python utilizza oggetti, classi e attributi, mentre il database utilizza tabelle, righe e colonne.

Un ORM permette di mettere in relazione questi due modelli, consentendo di rappresentare le tabelle attraverso classi Python e i record attraverso istanze di tali classi.

SQLAlchemy è uno degli ORM più utilizzati nell'ecosistema Python. Permette di lavorare con diversi database relazionali e offre un sistema di mapping flessibile e potente.

Un concetto fondamentale è la Session, che gestisce il dialogo tra gli oggetti Python e il database. Attraverso la sessione è possibile aggiungere nuovi oggetti, recuperarli, modificarli e cancellarli.

Installazione

```
pip install sqlalchemy psycopg2-binary
```

Esempio pratico: configurazione

```
from sqlalchemy import create_enginefrom sqlalchemy.orm import DeclarativeBaseDATABASE_URL = (    "postgresql+psycopg2://"    "postgres:password@localhost:5432/formazione")engine = create_engine(DATABASE_URL)class Base(DeclarativeBase):    pass
```

Definizione del modello

```
from sqlalchemy import Stringfrom sqlalchemy.orm import Mapped, mapped_columnclass Studente(Base):    __tablename__ = "studenti"    id: Mapped[int] = mapped_column(        primary_key=True    )    nome: Mapped[str] = mapped_column(        String(100)    )    email: Mapped[str] = mapped_column(        String(150),        unique=True    )
```

Creazione delle tabelle

```
Base.metadata.create_all(engine)
```

Operazioni CRUD

```
from sqlalchemy.orm import Sessionwith Session(engine) as session:    studente = Studente(        nome="Mario Rossi",        email="mario@example.com"    )    session.add(studente)    session.commit()
```

Recupero dei dati:

```
from sqlalchemy import selectwith Session(engine) as session:    stmt = select(Studente)    studenti = session.scalars(stmt).all()    for studente in studenti:        print(studente.nome)
```

Modifica e cancellazione:

```
with Session(engine) as session:    studente = session.get(Studente, 1)    if studente:        studente.nome = "Mario Bianchi"        session.commit()
```

Attività laboratoriale

- Installazione e configurazione di SQLAlchemy.
- Creazione dei primi modelli Python.
- Collegamento a PostgreSQL.
- Esecuzione delle operazioni CRUD.
- Verifica della corrispondenza tra oggetti Python e record del database.

### Unità 3.4 – Relazioni tra modelli e gestione delle transazioni (3 ore)

Contenuti

- Relazioni tra entità nel modello ORM.
- Relazione uno-a-molti (One-to-Many).
- Relazione molti-a-uno (Many-to-One).
- Relazione molti-a-molti (Many-to-Many).
- Utilizzo di ForeignKey e relationship().
- Back_populates e navigazione delle relazioni.
- Caricamento dei dati correlati.
- Strategie di caricamento: lazy loading e eager loading.
- Concetto di transazione.
- Commit e rollback.
- Gestione delle eccezioni.
- Integrità referenziale e gestione degli errori.

Testo guida per la lezione

Le applicazioni reali non gestiscono entità isolate, ma informazioni collegate tra loro.

In un sistema di formazione, uno studente può iscriversi a più corsi e ciascun corso può avere più studenti. Si tratta quindi di una relazione molti-a-molti.

SQLAlchemy permette di rappresentare queste relazioni direttamente attraverso le classi Python, utilizzando ForeignKey e relationship().

Un altro aspetto fondamentale riguarda la gestione delle transazioni.

Quando un'applicazione esegue più operazioni sul database, è importante garantire che queste vengano completate correttamente. Se una delle operazioni fallisce, il sistema deve poter annullare le modifiche non ancora confermate.

Il metodo commit() conferma le modifiche, mentre rollback() annulla le modifiche pendenti.

Esempio pratico: relazione uno-a-molti

Un corso può avere più iscrizioni:

```
from sqlalchemy import ForeignKeyfrom sqlalchemy.orm import relationship, Mapped, mapped_columnclass Corso(Base):    __tablename__ = "corsi"    id: Mapped[int] = mapped_column(        primary_key=True    )    titolo: Mapped[str]    iscrizioni: Mapped[list["Iscrizione"]] = relationship(        back_populates="corso"    )class Iscrizione(Base):    __tablename__ = "iscrizioni"    id: Mapped[int] = mapped_column(        primary_key=True    )    corso_id: Mapped[int] = mapped_column(        ForeignKey("corsi.id")    )    corso: Mapped["Corso"] = relationship(        back_populates="iscrizioni"    )
```

Esempio pratico: gestione delle transazioni

```
from sqlalchemy.exc import SQLAlchemyErrortry:    with Session(engine) as session:        nuovo_corso = Corso(            titolo="Python Backend"        )        session.add(nuovo_corso)        session.commit()except SQLAlchemyError as e:    print("Errore nella persistenza:", e)
```

È possibile utilizzare esplicitamente rollback() quando si gestisce manualmente una sessione e si desidera recuperare da un errore.

Attività laboratoriale

- Creazione delle relazioni tra Studente, Corso e Iscrizione.
- Inserimento di oggetti collegati.
- Recupero delle informazioni attraverso le relazioni.
- Simulazione di errori di integrità referenziale.
- Gestione di commit e rollback.

### Unità 3.5 – Migrazioni del database con Alembic (2 ore)

Contenuti

- Introduzione al problema dell'evoluzione dello schema.
- Differenza tra creazione iniziale e migrazione del database.
- Introduzione ad Alembic.
- Installazione e configurazione.
- Integrazione con SQLAlchemy.
- Configurazione di alembic.ini e env.py.
- Generazione automatica delle migration.
- Revisione delle migration generate.
- Applicazione delle migration al database.
- Comandi upgrade e downgrade.
- Versionamento dello schema del database.
- Gestione delle modifiche ai modelli.

Testo guida per la lezione

Durante lo sviluppo di un'applicazione, il modello dei dati evolve continuamente.

Inizialmente una tabella potrebbe contenere soltanto nome ed email di uno studente. Successivamente potrebbe essere necessario aggiungere data di nascita, telefono o altri attributi.

Modificare manualmente la struttura del database non è una soluzione adeguata in un progetto professionale, soprattutto quando l'applicazione è già utilizzata o distribuita in ambienti diversi.

Alembic permette di gestire l'evoluzione dello schema attraverso migration versionate.

Ogni migration descrive una modifica alla struttura del database e può essere applicata o, in molti casi, annullata.

Il vantaggio è che lo schema del database diventa parte integrante del progetto software e può essere aggiornato in modo controllato e ripetibile.

Installazione

```
pip install alembic
```

Inizializzazione:

```
alembic init migrations
```

Generazione automatica di una migration:

```
alembic revision --autogenerate -m "creazione tabelle"
```

Applicazione delle modifiche:

```
alembic upgrade head
```

Visualizzazione della revisione corrente:

```
alembic current
```

Visualizzazione della cronologia:

```
alembic history
```

Annullamento dell'ultima migration:

```
alembic downgrade -1
```

Attività laboratoriale

- Inizializzazione di Alembic nel progetto.
- Collegamento dei metadati SQLAlchemy.
- Generazione della prima migration.
- Applicazione della migration su PostgreSQL.
- Modifica di un modello e generazione di una seconda migration.
- Verifica dell'aggiornamento dello schema.

Particolare attenzione sarà dedicata alla revisione manuale delle migration generate automaticamente: l'autogenerate non sostituisce il controllo dello sviluppatore.

### Unità 3.6 – Laboratorio integrato: persistenza nell'API FastAPI (2 ore)

Contenuti

- Integrazione tra FastAPI, SQLAlchemy e PostgreSQL.
- Organizzazione del livello di persistenza.
- Configurazione centralizzata della connessione.
- Gestione delle sessioni attraverso Dependency Injection.
- Separazione tra modelli ORM e schemi Pydantic.
- Implementazione delle operazioni CRUD attraverso endpoint REST.
- Gestione degli errori applicativi e di persistenza.
- Verifica del funzionamento tramite Swagger UI.

Testo guida per la lezione

Nelle applicazioni backend professionali il database non viene normalmente interrogato direttamente all'interno di ogni endpoint.

È preferibile separare le responsabilità, organizzando il progetto in moduli dedicati alla configurazione, ai modelli ORM e alla gestione delle operazioni di persistenza.

FastAPI mette a disposizione un sistema di Dependency Injection che consente di fornire agli endpoint le risorse necessarie, tra cui una sessione SQLAlchemy.

Un aspetto importante è distinguere i modelli ORM dagli schemi Pydantic: i primi descrivono la struttura persistente dei dati, mentre i secondi definiscono il formato delle informazioni ricevute e restituite attraverso le API.

Esempio di organizzazione del progetto

```
backend/
│
├── main.py
│
├── database/
│   ├── connection.py
│   └── models.py
│
├── schemas/
│   └── studente.py
│
├── routers/
│   └── studenti.py
│
└── migrations/
    └── versions/
```

Esempio: gestione della sessione

```
from sqlalchemy.orm import Sessionfrom database.connection import SessionLocaldef get_db():    db = SessionLocal()    try:        yield db    finally:        db.close()
```

Esempio: endpoint di inserimento

```
from fastapi import APIRouter, Dependsfrom sqlalchemy.orm import Sessionfrom database.models import Studentefrom schemas.studente import StudenteCreatefrom database.connection import get_dbrouter = APIRouter()@router.post("/studenti")def crea_studente(    dati: StudenteCreate,    db: Session = Depends(get_db)):    studente = Studente(        nome=dati.nome,        email=dati.email    )    db.add(studente)    db.commit()    db.refresh(studente)    return studente
```

Attività laboratoriale

Realizzazione di un primo livello di persistenza per l'API sviluppata nel modulo precedente:

- Configurazione della connessione PostgreSQL.
- Creazione dei modelli ORM.
- Definizione degli schemi Pydantic.
- Implementazione degli endpoint CRUD.
- Gestione delle sessioni.
- Verifica delle operazioni tramite Swagger UI.
- Aggiornamento dello schema con Alembic.

## 4. Distribuzione delle ore

# 16 ore

Ripartizione delle attività didattiche

3.1 – Fondamenti di database relazionali

2 h

3.2 – SQL e PostgreSQL

3 h

3.3 – ORM SQLAlchemy

4 h

3.4 – Relazioni e transazioni

3 h

3.5 – Migrazioni con Alembic

2 h

3.6 – Laboratorio integrato FastAPI

2 h

Totale\
16 ore

| Tipologia                       | Ore |
| ------------------------------- | --- |
| Lezione guidata e dimostrazioni | 5   |
| Esercitazioni SQL e ORM         | 5   |
| Laboratorio integrato           | 6   |
| Totale                          | 16  |

## 5. Metodologia didattica

Il modulo sarà sviluppato attraverso un approccio progressivo, alternando spiegazioni teoriche, dimostrazioni operative ed esercitazioni pratiche.

La metodologia prevede:

- Lezione partecipata con esempi riferiti a casi applicativi reali.
- Dimostrazioni di progettazione e interrogazione di database PostgreSQL.
- Esercitazioni individuali e di gruppo con SQLAlchemy.
- Sviluppo incrementale di un livello di persistenza integrato con FastAPI.
- Analisi e risoluzione di errori relativi alla gestione dei dati.
- Utilizzo di strumenti di AI-assisted development per supportare la comprensione delle query SQL, la generazione di modelli ORM e l'analisi delle migration, verificando sempre la correttezza del codice prodotto.

## 6. Project work del modulo

Sistema di gestione corsi e iscrizioni

[Create a database diagram | drawDB Docs](https://images.openai.com/static-rsc-4/u_Cgrnil2gxDu-qjCb2ckswgqElE10J2yzFWlRUTI34dOepsHhudfHM9YqIIvz1IvjKGkrHD1_VUvNW1-H-mSxgVC7YopTC5I9tiAmg6gXsBkmB_pgkYpYl6rCEPZKzrHziWir_aQax-AMS8uAeTMfXiUs0nppRlpCbK_PvR2co?purpose=inline)

[drawdb-io.github.io](https://drawdb-io.github.io/docs/create-diagram?utm_source=chatgpt.com)

Gli studenti realizzeranno il livello di persistenza di un'applicazione backend per la gestione di corsi di formazione e iscrizioni.

Entità principali

- Studente
- Corso
- Iscrizione

Funzionalità richieste

1. Progettazione dello schema relazionale.
2. Creazione delle tabelle PostgreSQL.
3. Definizione dei modelli ORM.
4. Gestione delle relazioni tra entità.
5. Implementazione delle operazioni CRUD.
6. Gestione delle transazioni e degli errori.
7. Evoluzione dello schema attraverso Alembic.
8. Collegamento del database agli endpoint FastAPI.

Risultato atteso

Un backend capace di conservare e gestire dati persistenti, con uno schema database versionato e integrato nell'applicazione REST.

## 7. Competenze e risultati di apprendimento

Al termine del modulo lo studente sarà in grado di:

- Comprendere e progettare un database relazionale.
- Definire tabelle, chiavi, vincoli e relazioni.
- Scrivere query SQL per interrogare e modificare i dati.
- Utilizzare PostgreSQL come sistema di gestione del database.
- Implementare il mapping tra oggetti Python e tabelle relazionali attraverso SQLAlchemy.
- Gestire operazioni CRUD e relazioni tra modelli.
- Gestire sessioni, transazioni ed errori di persistenza.
- Utilizzare Alembic per versionare ed evolvere lo schema del database.
- Integrare SQLAlchemy e PostgreSQL in un'applicazione FastAPI.

Verifica dell'apprendimento

La verifica sarà effettuata attraverso un'esercitazione pratica nella quale lo studente dovrà progettare un semplice modello relazionale, implementare i corrispondenti modelli SQLAlchemy, eseguire operazioni CRUD e realizzare almeno una migration con Alembic.

## 8. Stack tecnologico e strumenti

[PostgreSQL | AIQ Integrations](https://images.openai.com/static-rsc-4/EHiLhEq6sahKKDTIRbaG1I4NLRieLf8_FEyfGa8wAekLqHDDR7FULJX8VBkXH_YnAYmuOkyFPUi0TvCWw8wgjT4t5PhiNq_c_DVwhsPU4wNroAjNC6zpyieUkTmIgDPyTpWyHc6Un40cqeCpur1X1qqQGJTp6UNfFjMir-cWVNw?purpose=inline)

PostgreSQL

Database relazionale

[Pythonで始めるSQLAlchemy入門：ORMの基本から実践まで](https://images.openai.com/static-rsc-4/E_Wu8T4AYTDb9DA0dSKfIJKmP2aM3O33lqJize7a9ZqPzIcw-6dY_egTDurW6_Uz9HVTJH39Tr_YPJCkqJSg-85SpZZgpjTNTN0A3KMsJVn_ImdWmf2nGrvX05wb43Vh1EcerdCqbDFzTNFVG6z89suoTbiBKZc-iIl-HuAAmtQ?purpose=inline)

SQLAlchemy

ORM e persistenza

[ビットオン AIブログ トップ](https://images.openai.com/static-rsc-4/7PXHy90Id5YUUXprcWeZUF9_Wx6of70wO1aBM6hJhrb5Svk9xxQC9vACNtAnMjU2POKQtnyYWD3VWbvBu4QlLbF0BVejekqCeT7PI_mRlBczgHlKopi234rsVdpHV1iFfAZaNMyJlMJV_8baLnCZAqFiy_zqwusND4HgJ-9Zm3A?purpose=inline)

Alembic

Database migration

[File:Python logo 01.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/4WQnbUUJdvO4G_O54H-9RXYeiNC8ap-hadl7zQO_37z43QV44clQv_3mffdRKUsamUYFp5veqRIRVDSmAnDHlkj1JtcAh46t9rVGeEsTz7Kfg4qMWcGYIrrsCkO7nIRnHcOOcRu-Lm-tFOE47ydEtspq6XPPqxxyX0kFOlIlqkM?purpose=inline)

Python

Linguaggio backend

[FastAPI nedir? Geliştirme Ortamlarının Kurulumu ve İlk Örnekler. | by Kaan Mercan | Medium](https://images.openai.com/static-rsc-4/AbCmeZD4TfobGUoc3RCUW8KwLZrOtWGyAsAclWg19A3BD6a-VIjjQqzklxVO32-j_3xHx_YqdedoAGlxwyhbYUwvZe8H6z7alP7jsjh-o6Eknz9_Uu-Em_6krVZnpVPJduVXLeJ6cTUoswiWhYUflU3YTNwWqbydDn187DCtemY?purpose=inline)

FastAPI

Integrazione REST

[omv6:docker_in_omv \[omv-extras.org\]](https://images.openai.com/static-rsc-4/ZHUgVPL5puLp_1GSrZXNgRPXrJprRcfwUdPZLnn3YgdapXevIQoLhpVVRXdJlVFflc8gXKSMsHLdZzBWWeMS5spzZe3Yb0-CpLP779ryt44I7rJTuWvNVMYSUSASZxzq-uBODtzbFKQ0zncLYfGEEsXa8jG8bp_Y9uwQM-9_YGo?purpose=inline)

Docker

Ambiente database

Nota didattica: suggerisco di utilizzare SQLAlchemy 2.x con mapping dichiarativo tipizzato (`Mapped`, `mapped_column`) e Alembic. È importante insegnare agli studenti fin da subito il flusso corretto: modifica del modello → generazione migration → revisione → applicazione al database. In questo modo il database viene trattato come componente evolutiva del software e non come una struttura da ricreare manualmente.

Il modulo prepara direttamente al successivo sviluppo di applicazioni backend complete, nelle quali API REST, logica applicativa e persistenza lavorano insieme.
