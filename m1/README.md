# Micro-progettazione didattica – Modulo 1

## Python e programmazione a oggetti

16 ore

Livello: Fondamenti / Intermedio

Teoria + laboratorio

## 1. Inquadramento del modulo

Il modulo introduce Python come linguaggio di programmazione per lo sviluppo di applicazioni backend, fornendo le competenze necessarie per affrontare successivamente la realizzazione di API REST e servizi web.

Il percorso parte dagli elementi fondamentali del linguaggio, affrontando sintassi, tipi di dato, operatori, strutture di controllo e collezioni. Si passa quindi alla programmazione strutturata e modulare attraverso funzioni, parametri, valori restituiti e organizzazione del codice.

Una parte centrale è dedicata alla programmazione orientata agli oggetti (OOP), con particolare attenzione alla progettazione di classi, alla creazione di istanze, all'incapsulamento, all'ereditarietà e al polimorfismo.

Gli studenti acquisiranno inoltre familiarità con la gestione delle eccezioni, l'utilizzo dei type hints, l'organizzazione dei package e la creazione di ambienti virtuali.

L'intero modulo avrà un'impostazione laboratoriale: gli argomenti saranno introdotti attraverso esempi progressivi e applicati a un caso concreto di progettazione software, relativo alla gestione di utenti, prodotti e ordini.

Risultato atteso: lo studente sarà in grado di sviluppare un piccolo programma Python organizzato in moduli e basato su un modello a oggetti, applicando i principali principi della programmazione orientata agli oggetti.

## 2. Articolazione delle 16 ore

Propongo 4 unità didattiche da 4 ore ciascuna. Questa suddivisione permette di alternare spiegazione, dimostrazione al computer, esercitazioni individuali e momenti di verifica.

| Unità  | Argomento                                        | Ore |
| ------ | ------------------------------------------------ | --- |
| 1      | Fondamenti del linguaggio Python                 | 4   |
| 2      | Funzioni, modularità e organizzazione del codice | 4   |
| 3      | Programmazione orientata agli oggetti            | 4   |
| 4      | OOP avanzata, eccezioni e laboratorio integrato  | 4   |
| Totale |                                                  | 16  |

# 3. Micro-progettazione dettagliata

## Unità didattica 1 – Fondamenti del linguaggio Python

4 ore

Lezione 1

### Obiettivi formativi

Al termine dell'unità lo studente sarà in grado di:

- Comprendere le caratteristiche principali di Python e il suo modello di esecuzione.
- Scrivere ed eseguire semplici programmi Python.
- Dichiarare variabili e utilizzare i principali tipi di dato.
- Applicare operatori aritmetici, logici e di confronto.
- Utilizzare condizioni, cicli e strutture dati fondamentali.

### 1.1 Introduzione a Python

Testo guida per la lezione

Python è un linguaggio di programmazione ad alto livello, interpretato e multiparadigma. È utilizzato in numerosi ambiti applicativi: sviluppo web, automazione, analisi dei dati, machine learning e intelligenza artificiale.

Le sue caratteristiche principali sono la sintassi leggibile, la gestione automatica della memoria, la disponibilità di numerose librerie e un ecosistema particolarmente adatto allo sviluppo rapido di applicazioni.

Verranno introdotti:

- Python e i suoi principali ambiti applicativi.
- Interprete Python e modalità di esecuzione.
- Differenza tra modalità interattiva e script.
- Utilizzo del terminale.
- Convenzioni di indentazione e struttura di un programma.
- Funzione `print()` e acquisizione di input con `input()`.

Esempio 1 – Primo programma

```
print("Benvenuti nel corso Python Backend!")nome = input("Inserisci il tuo nome: ")print(f"Ciao {nome}, iniziamo a programmare!")
```

Si introduce anche l'utilizzo delle f-string per la formattazione delle stringhe.

### 1.2 Variabili e tipi di dato

Testo guida per la lezione

In Python le variabili rappresentano riferimenti a oggetti presenti in memoria. Non è necessario dichiarare preventivamente il tipo di una variabile: il linguaggio utilizza il dynamic typing.

Vengono analizzati i principali tipi di dato:

- `int`: numeri interi.
- `float`: numeri decimali.
- `str`: stringhe.
- `bool`: valori booleani.
- `None`: assenza di valore.

Si approfondiscono inoltre:

- Assegnazione e riassegnazione.
- Conversione esplicita dei tipi (casting).
- Funzione `type()`.
- Concetto di mutabilità e immutabilità.
- Convenzioni per i nomi delle variabili (PEP 8).

Esempio 2 – Gestione di un prodotto

```
nome = "Notebook"prezzo = 899.90quantita = 5disponibile = Trueprint(type(nome))print(type(prezzo))totale = prezzo * quantitaprint(f"Prodotto: {nome}")print(f"Valore magazzino: {totale:.2f} euro")
```

### 1.3 Operatori ed espressioni

Testo guida per la lezione

Vengono presentati gli operatori utilizzati per costruire espressioni e condizioni:

- Aritmetici: `+`, `-`, `*`, `/`, `//`, `%`, `**`.
- Di confronto: `==`, `!=`, `<`, `>`, `<=`, `>=`.
- Logici: `and`, `or`, `not`.
- Di assegnazione: `=`, `+=`, `-=`, `*=`.
- Di appartenenza: `in`, `not in`.
- Di identità: `is`, `is not`.

Particolare attenzione sarà dedicata alla differenza tra confronto (`==`) e identità (`is`).

Esempio 3 – Verifica disponibilità

```
prezzo = 120quantita = 3budget = 150totale = prezzo * quantitaif totale <= budget and quantita > 0:    print("Acquisto possibile")else:    print("Budget insufficiente")
```

### 1.4 Strutture di controllo

Testo guida per la lezione

Le strutture di controllo consentono di modificare il flusso di esecuzione di un programma.

Saranno affrontati:

- Istruzioni condizionali `if`, `elif`, `else`.
- Ciclo `for` e funzione `range()`.
- Ciclo `while`.
- Istruzioni `break` e `continue`.
- Cicli annidati.
- Operatore ternario.

Esempio 4 – Calcolo del valore degli ordini

```
ordini = [120, 85, 250, 40, 310]totale = 0for importo in ordini:    if importo >= 100:        totale += importoprint(f"Totale ordini qualificati: {totale}")
```

### 1.5 Collezioni e strutture dati

Testo guida per la lezione

Python mette a disposizione diverse strutture dati per organizzare e manipolare insiemi di informazioni.

Vengono introdotte:

- Liste (`list`): collezioni ordinate e modificabili.
- Tuple (`tuple`): collezioni ordinate e immutabili.
- Set (`set`): collezioni di elementi univoci.
- Dizionari (`dict`): strutture basate su coppie chiave-valore.

Si affrontano le operazioni principali: inserimento, modifica, eliminazione, ricerca, iterazione e accesso agli elementi.

Esempio 5 – Gestione di un catalogo

```
prodotti = [    {"id": 1, "nome": "Mouse", "prezzo": 25.90},    {"id": 2, "nome": "Tastiera", "prezzo": 49.90},    {"id": 3, "nome": "Monitor", "prezzo": 189.00}]for prodotto in prodotti:    print(        prodotto["nome"],        prodotto["prezzo"]    )
```

### Laboratorio 1

Esercitazione: gestione di un piccolo catalogo prodotti

Gli studenti realizzeranno uno script Python che consenta di:

1. Definire una collezione di prodotti.
2. Visualizzare l'elenco dei prodotti.
3. Calcolare il valore complessivo del catalogo.
4. Individuare i prodotti con prezzo superiore a una soglia.
5. Ricercare un prodotto attraverso il suo identificativo.
6. Verificare la disponibilità in base alla quantità.

Competenze sviluppate: sintassi Python, variabili, operatori, condizioni, cicli e collezioni.

## Unità didattica 2 – Funzioni, modularità e organizzazione del codice

4 ore

Lezione 2

### Obiettivi formativi

- Suddividere un programma in funzioni.
- Definire parametri e valori restituiti.
- Comprendere lo scope delle variabili.
- Utilizzare funzioni integrate e funzioni personalizzate.
- Importare moduli e librerie.
- Organizzare il codice in più file.

### 2.1 Funzioni in Python

Testo guida per la lezione

Le funzioni consentono di organizzare il codice in blocchi riutilizzabili, ciascuno dedicato a uno specifico compito.

Vengono introdotti:

- Definizione di una funzione con `def`.
- Chiamata di una funzione.
- Parametri e argomenti.
- Valori di ritorno tramite `return`.
- Differenza tra `print()` e `return`.
- Parametri posizionali e keyword arguments.
- Parametri con valori predefiniti.
- Numero variabile di argomenti: `*args` e `**kwargs`.

Esempio 1 – Calcolo del prezzo di un ordine

```
def calcola_totale(prezzo, quantita):    return prezzo * quantitatotale = calcola_totale(25.90, 3)print(f"Totale: {totale:.2f} euro")
```

Si evidenzia come la funzione possa essere richiamata da diverse parti del programma, evitando duplicazioni.

Esempio 2 – Parametri opzionali

```
def applica_sconto(prezzo, percentuale=0):    sconto = prezzo * percentuale / 100    return prezzo - scontoprint(applica_sconto(100))print(applica_sconto(100, 20))
```

### 2.2 Scope e visibilità delle variabili

Testo guida per la lezione

Lo scope definisce la porzione di programma nella quale una variabile è accessibile.

Vengono analizzati:

- Variabili locali.
- Variabili globali.
- Parametri delle funzioni.
- Regole di risoluzione dei nomi (LEGB).
- Utilizzo di `global` e `nonlocal`.
- Buone pratiche per evitare dipendenze globali.

Esempio 3

```
aliquota = 22def calcola_iva(prezzo):    iva = prezzo * aliquota / 100    return ivaprint(calcola_iva(100))
```

Si discute perché, nei programmi ben progettati, sia preferibile passare esplicitamente i dati necessari alle funzioni anziché dipendere da variabili globali.

### 2.3 Funzioni come oggetti e strumenti del linguaggio

Introduzione a:

- Funzioni anonime `lambda`.
- Funzioni di ordinamento con `sorted()`.
- Funzioni `map()`, `filter()` e `enumerate()`.
- List comprehension.
- Docstring e documentazione delle funzioni.

Esempio 4 – Filtrare prodotti

```
prodotti = [    {"nome": "Mouse", "prezzo": 25},    {"nome": "Monitor", "prezzo": 180},    {"nome": "Tastiera", "prezzo": 50}]economici = [    p for p in prodotti    if p["prezzo"] < 100]print(economici)
```

### 2.4 Moduli e importazione

Testo guida per la lezione

Un modulo Python è un file contenente istruzioni, funzioni, classi e variabili che possono essere riutilizzate da altri programmi.

Vengono affrontati:

- Moduli standard della libreria Python.
- Istruzione `import`.
- Importazione selettiva con `from ... import`.
- Alias con `as`.
- Creazione di moduli personalizzati.
- Differenza tra modulo e package.
- Punto di ingresso `if __name__ == "__main__":`.

Esempio 5 – Separazione del codice

File `calcoli.py`:

```
def calcola_totale(prezzo, quantita):    return prezzo * quantita
```

File `main.py`:

```
from calcoli import calcola_totaletotale = calcola_totale(30, 4)print(totale)
```

### Laboratorio 2

Esercitazione: modularizzazione del catalogo prodotti

Gli studenti riprenderanno il programma realizzato nell'unità precedente e lo organizzeranno in più file.

Struttura proposta:

```
catalogo/
│
├── main.py
├── prodotti.py
└── funzioni.py
```

Attività:

1. Spostare i dati dei prodotti in un modulo dedicato.
2. Creare funzioni per ricerca e visualizzazione.
3. Realizzare una funzione per il calcolo del totale.
4. Importare le funzioni nel programma principale.
5. Verificare il corretto funzionamento dell'applicazione.

Competenze sviluppate: programmazione strutturata, riutilizzo del codice, modularità e organizzazione dei programmi.

## Unità didattica 3 – Programmazione orientata agli oggetti (OOP)

4 ore

Lezione 3

### Obiettivi formativi

- Comprendere il paradigma della programmazione a oggetti.
- Progettare classi e creare istanze.
- Definire attributi e metodi.
- Utilizzare costruttori e il parametro `self`.
- Applicare i principi di incapsulamento.
- Comprendere la differenza tra attributi di istanza e attributi di classe.

### 3.1 Introduzione alla programmazione orientata agli oggetti

Testo guida per la lezione

La programmazione orientata agli oggetti (Object-Oriented Programming – OOP) è un paradigma che permette di rappresentare elementi del mondo reale o concetti applicativi attraverso oggetti software.

Un oggetto è caratterizzato da:

- Stato: rappresentato dagli attributi.
- Comportamento: rappresentato dai metodi.
- Identità: consente di distinguere un oggetto dagli altri.

Una classe costituisce il modello utilizzato per creare oggetti, chiamati istanze.

Vengono introdotti i concetti di:

- Classe e istanza.
- Attributi e metodi.
- Stato e comportamento.
- Identità degli oggetti.
- Relazione tra classe e istanza.

Esempio 1 – Prima classe Python

```
class Prodotto:    def __init__(self, nome, prezzo):        self.nome = nome        self.prezzo = prezzo    def descrizione(self):        return f"{self.nome} - {self.prezzo} euro"p1 = Prodotto("Notebook", 899.90)p2 = Prodotto("Mouse", 25.90)print(p1.descrizione())print(p2.descrizione())
```

Spiegare nel dettaglio:

- `class`: definisce una classe.
- `__init__()`: inizializza una nuova istanza.
- `self`: rappresenta l'istanza corrente.
- `self.nome`: attributo dell'oggetto.
- `descrizione()`: metodo di istanza.

### 3.2 Costruttori, attributi e metodi

Testo guida per la lezione

Si approfondisce il ciclo di vita degli oggetti e la loro inizializzazione.

Argomenti:

- Metodo speciale `__init__()`.
- Creazione delle istanze.
- Attributi di istanza.
- Attributi di classe.
- Metodi di istanza.
- Metodi di classe con `@classmethod`.
- Metodi statici con `@staticmethod`.
- Rappresentazione degli oggetti con `__str__()` e `__repr__()`.

Esempio 2 – Attributi di istanza e di classe

```
class Utente:    totale_utenti = 0    def __init__(self, nome, email):        self.nome = nome        self.email = email        Utente.totale_utenti += 1    def __str__(self):        return f"{self.nome} ({self.email})"u1 = Utente("Mario", "mario@email.it")u2 = Utente("Anna", "anna@email.it")print(u1)print(u2)print(Utente.totale_utenti)
```

È importante chiarire che `totale_utenti` appartiene alla classe e viene condiviso dalle sue istanze, mentre `nome` ed `email` appartengono ai singoli oggetti.

### 3.3 Incapsulamento e proprietà

Testo guida per la lezione

L'incapsulamento è uno dei principi fondamentali della programmazione orientata agli oggetti.

Consiste nell'organizzare dati e comportamenti all'interno di una classe, controllando le modalità con cui lo stato interno di un oggetto può essere consultato o modificato.

Python adotta una convenzione basata sui nomi:

- Attributi pubblici: `nome`.
- Attributi protetti per convenzione: `_prezzo`.
- Attributi con name mangling: `__saldo`.

Si introduce inoltre la gestione controllata degli attributi mediante `@property`, `@nome.setter` e `@nome.deleter`.

Esempio 3 – Controllo del prezzo

```
class Prodotto:    def __init__(self, nome, prezzo):        self.nome = nome        self.prezzo = prezzo    @property    def prezzo(self):        return self._prezzo    @prezzo.setter    def prezzo(self, valore):        if valore < 0:            raise ValueError("Prezzo non valido")        self._prezzo = valorep = Prodotto("Monitor", 199.90)print(p.prezzo)p.prezzo = 249.90print(p.prezzo)
```

Si evidenzia che Python non implementa un sistema di accessibilità `private` identico a Java: l'incapsulamento è basato principalmente su convenzioni e meccanismi del linguaggio.

### 3.4 Relazioni tra oggetti: composizione

Testo guida per la lezione

Nella progettazione orientata agli oggetti, le classi possono collaborare attraverso relazioni.

Si introduce la composizione, che permette a un oggetto di contenere o utilizzare altri oggetti per realizzare le proprie funzionalità.

Il principio fondamentale è has-a: un oggetto possiede o utilizza altri oggetti.

Esempi applicativi:

- Un ordine contiene prodotti.
- Un ordine è associato a un cliente.
- Un carrello contiene elementi acquistabili.
- Un utente può avere un indirizzo di spedizione.

Esempio 4 – Ordine composto da prodotti

```
class Prodotto:    def __init__(self, nome, prezzo):        self.nome = nome        self.prezzo = prezzoclass Ordine:    def __init__(self, numero):        self.numero = numero        self.prodotti = []    def aggiungi_prodotto(self, prodotto):        self.prodotti.append(prodotto)    def totale(self):        return sum(            p.prezzo for p in self.prodotti        )p1 = Prodotto("Mouse", 25)p2 = Prodotto("Tastiera", 50)ordine = Ordine(1001)ordine.aggiungi_prodotto(p1)ordine.aggiungi_prodotto(p2)print(ordine.totale())
```

### Laboratorio 3

Esercitazione: trasformazione del catalogo in un modello a oggetti

Gli studenti convertiranno la precedente gestione dei prodotti in un'applicazione basata su classi.

Classi da realizzare:

1. `Prodotto`: nome, prezzo, quantità disponibile.
2. `Utente`: nome, email e identificativo.
3. `Ordine`: numero, utente e lista di prodotti.

Operazioni richieste:

- Creazione di prodotti e utenti.
- Visualizzazione delle informazioni.
- Inserimento dei prodotti in un ordine.
- Calcolo del totale dell'ordine.
- Verifica della disponibilità dei prodotti.

Competenze sviluppate: progettazione delle classi, istanziazione degli oggetti, incapsulamento e composizione.

## Unità didattica 4 – OOP avanzata, eccezioni e laboratorio integrato

4 ore

Lezione 4

### Obiettivi formativi

- Comprendere e applicare l'ereditarietà.
- Utilizzare il polimorfismo.
- Comprendere il ruolo delle classi astratte.
- Gestire correttamente le eccezioni.
- Utilizzare i type hints.
- Organizzare un progetto Python attraverso package e ambienti virtuali.
- Realizzare un'applicazione integrata basata sulla programmazione a oggetti.

### 4.1 Ereditarietà

Testo guida per la lezione

L'ereditarietà permette di definire una nuova classe partendo da una classe esistente, riutilizzandone attributi e metodi e introducendo funzionalità specifiche.

La classe da cui si eredita viene definita classe base o superclasse, mentre quella che eredita è chiamata sottoclasse.

Vengono introdotti:

- Relazione is-a.
- Classe padre e classe figlia.
- Ereditarietà singola.
- Ridefinizione dei metodi (method overriding).
- Utilizzo di `super()`.
- Ereditarietà multipla: cenni e MRO (Method Resolution Order).

Esempio 1 – Gerarchia degli utenti

```
class Utente:    def __init__(self, nome, email):        self.nome = nome        self.email = email    def descrizione(self):        return f"{self.nome} - {self.email}"class Cliente(Utente):    def __init__(self, nome, email, indirizzo):        super().__init__(nome, email)        self.indirizzo = indirizzo    def descrizione(self):        return (            f"{super().descrizione()} "            f"- {self.indirizzo}"        )cliente = Cliente(    "Mario",    "mario@email.it",    "Torino")print(cliente.descrizione())
```

### 4.2 Polimorfismo e classi astratte

Testo guida per la lezione

Il polimorfismo permette di utilizzare oggetti di classi differenti attraverso un'interfaccia comune, lasciando che ciascuna classe implementi il comportamento specifico.

In Python il polimorfismo è favorito dal cosiddetto duck typing: ciò che conta è il comportamento dell'oggetto e non necessariamente la sua appartenenza a una particolare gerarchia.

Si introducono:

- Method overriding.
- Polimorfismo attraverso metodi comuni.
- Duck typing.
- Modulo `abc`.
- Classi astratte con `ABC`.
- Metodi astratti con `@abstractmethod`.

Esempio 2 – Polimorfismo

```
class MetodoPagamento:    def paga(self, importo):        raise NotImplementedErrorclass CartaCredito(MetodoPagamento):    def paga(self, importo):        print(f"Pagamento carta: {importo} euro")class PayPal(MetodoPagamento):    def paga(self, importo):        print(f"Pagamento PayPal: {importo} euro")def esegui_pagamento(metodo, importo):    metodo.paga(importo)pagamenti = [    CartaCredito(),    PayPal()]for metodo in pagamenti:    esegui_pagamento(metodo, 100)
```

Si passa quindi alla versione con classe astratta.

Esempio 3 – Utilizzo di ABC

```
from abc import ABC, abstractmethodclass MetodoPagamento(ABC):    @abstractmethod    def paga(self, importo):        passclass CartaCredito(MetodoPagamento):    def paga(self, importo):        print(f"Carta: {importo}")class PayPal(MetodoPagamento):    def paga(self, importo):        print(f"PayPal: {importo}")
```

Spiegare che una classe astratta definisce un contratto che le sottoclassi concrete devono rispettare.

### 4.3 Gestione delle eccezioni

Testo guida per la lezione

Le eccezioni sono eventi che si verificano durante l'esecuzione e che interrompono il normale flusso del programma, se non gestiti.

Una buona applicazione deve prevedere situazioni anomale e gestirle in maniera controllata.

Vengono affrontati:

- Differenza tra errori sintattici ed eccezioni.
- Blocco `try`.
- Blocchi `except`.
- `else` e `finally`.
- Eccezioni integrate (`ValueError`, `TypeError`, `KeyError`, `ZeroDivisionError`).
- Sollevamento di eccezioni tramite `raise`.
- Creazione di eccezioni personalizzate.
- Principi di gestione degli errori nelle applicazioni backend.

Esempio 4 – Eccezione personalizzata

```
class ProdottoNonDisponibileError(Exception):    passclass Prodotto:    def __init__(self, nome, quantita):        self.nome = nome        self.quantita = quantita    def acquista(self, numero):        if numero > self.quantita:            raise ProdottoNonDisponibileError(                "Quantità non disponibile"            )        self.quantita -= numerop = Prodotto("Notebook", 3)try:    p.acquista(5)except ProdottoNonDisponibileError as e:    print(f"Errore: {e}")
```

### 4.4 Type hints e annotazioni

Testo guida per la lezione

Python è un linguaggio dinamicamente tipizzato, ma permette di specificare annotazioni di tipo attraverso i type hints.

Questi strumenti migliorano la leggibilità, la documentazione e la manutenzione del codice, facilitando inoltre l'utilizzo degli IDE e degli strumenti di analisi statica.

Argomenti:

- Annotazione delle variabili.
- Tipizzazione dei parametri.
- Tipizzazione dei valori restituiti.
- Utilizzo di `list`, `dict`, `tuple` e `set` nelle annotazioni.
- Tipi opzionali e union types.
- Annotazioni delle classi e dei metodi.
- Cenni a strumenti di controllo statico come mypy.

Esempio 5 – Funzione con type hints

```
def calcola_totale(    prezzi: list[float]) -> float:    return sum(prezzi)prezzi = [25.90, 49.90, 100.00]totale: float = calcola_totale(prezzi)print(totale)
```

Esempio 6 – Tipizzazione degli oggetti

```
class Prodotto:    def __init__(        self,        nome: str,        prezzo: float    ) -> None:        self.nome: str = nome        self.prezzo: float = prezzo    def descrizione(self) -> str:        return f"{self.nome}: {self.prezzo} euro"
```

È importante precisare che i type hints non introducono automaticamente controlli sui tipi durante l'esecuzione.

### 4.5 Package e ambienti virtuali

Testo guida per la lezione

Per sviluppare applicazioni Python strutturate è necessario organizzare il codice in moduli e package e gestire le dipendenze esterne.

Vengono affrontati:

- Organizzazione dei file e delle cartelle.
- Package Python.
- File `__init__.py`.
- Importazione tra package.
- Ambiente virtuale con `venv`.
- Installazione delle librerie con `pip`.
- Gestione delle dipendenze.
- File `requirements.txt`.
- Differenza tra ambiente globale e ambiente virtuale.

Esempio 7 – Creazione di un ambiente virtuale

```
# Creazione ambiente virtuale
python3 -m venv .venv

# Attivazione su Linux/macOS
source .venv/bin/activate

# Aggiornamento pip
python -m pip install --upgrade pip

# Installazione di una libreria
pip install requests

# Esportazione dipendenze
pip freeze > requirements.txt
```

Discutere l'importanza degli ambienti isolati nello sviluppo backend: progetti differenti possono utilizzare versioni diverse delle stesse librerie senza interferire tra loro.

### Laboratorio 4 – Progetto integrato

Titolo: progettazione di un sistema di gestione utenti, prodotti e ordini

L'attività conclusiva consiste nella realizzazione di una piccola applicazione Python che utilizzi tutti i concetti affrontati nel modulo.

Struttura progettuale proposta

```
ecommerce/
│
├── main.py
│
├── models/
│   ├── __init__.py
│   ├── utente.py
│   ├── prodotto.py
│   └── ordine.py
│
├── services/
│   ├── __init__.py
│   └── gestione_ordini.py
│
└── exceptions/
    ├── __init__.py
    └── errori.py
```

Classi da progettare

| Classe            | Responsabilità                                |
| ----------------- | --------------------------------------------- |
| `Utente`          | Gestione dei dati anagrafici e identificativi |
| `Cliente`         | Specializzazione dell'utente                  |
| `Prodotto`        | Gestione di prezzo e disponibilità            |
| `Ordine`          | Gestione dei prodotti acquistati              |
| `MetodoPagamento` | Definizione del contratto di pagamento        |
| `CartaCredito`    | Implementazione del pagamento                 |
| `PayPal`          | Implementazione del pagamento                 |

Funzionalità richieste

1. Creazione di utenti e clienti.
2. Inserimento e gestione dei prodotti.
3. Creazione di un ordine associato a un cliente.
4. Aggiunta di prodotti all'ordine.
5. Calcolo del totale.
6. Verifica della disponibilità.
7. Gestione delle eccezioni in caso di quantità insufficiente.
8. Esecuzione di un pagamento attraverso un'interfaccia comune.
9. Visualizzazione del riepilogo dell'ordine.

Vincoli tecnici

- Utilizzo delle classi e delle istanze.
- Incapsulamento degli attributi.
- Utilizzo della composizione.
- Applicazione dell'ereditarietà e del polimorfismo.
- Presenza di type hints.
- Gestione delle eccezioni.
- Organizzazione in moduli e package.

Competenze sviluppate: progettazione OOP, organizzazione di applicazioni Python, gestione degli errori e sviluppo di un primo modello software strutturato.

# 4. Riepilogo della distribuzione oraria

La seguente distribuzione permette di mantenere un equilibrio tra spiegazione, dimostrazione pratica ed esercitazione.

| Unità didattica             | Teoria e dimostrazioni | Laboratorio | Totale |
| --------------------------- | ---------------------- | ----------- | ------ |
| 1. Fondamenti Python        | 2 h                    | 2 h         | 4 h    |
| 2. Funzioni e modularità    | 2 h                    | 2 h         | 4 h    |
| 3. Programmazione OOP       | 2 h                    | 2 h         | 4 h    |
| 4. OOP avanzata e strumenti | 2 h                    | 2 h         | 4 h    |
| Totale                      | 8 h                    | 8 h         | 16 h   |

# 5. Metodologia didattica

Il modulo utilizzerà un approccio progressivo, basato sull'apprendimento attraverso esempi concreti e attività pratiche.

Le metodologie previste sono:

- Lezione dialogata: introduzione dei concetti teorici attraverso esempi e confronto con gli studenti.
- Live coding: sviluppo di programmi Python direttamente durante la lezione, mostrando progressivamente la costruzione del codice.
- Learning by doing: esercitazioni individuali per consolidare le conoscenze acquisite.
- Problem solving: risoluzione di problemi applicativi attraverso la progettazione di algoritmi e classi.
- Laboratorio incrementale: evoluzione di un unico progetto, inizialmente sviluppato con strutture dati semplici e successivamente trasformato in un'applicazione orientata agli oggetti.

Si potrà introdurre anche l'utilizzo di strumenti AI-assisted coding per supportare la comprensione degli errori, la generazione di esempi e il confronto tra differenti implementazioni. Sarà importante mantenere centrale la capacità dello studente di comprendere, verificare e modificare autonomamente il codice prodotto.

# 6. Verifica e valutazione degli apprendimenti

La valutazione sarà effettuata attraverso osservazione delle attività laboratoriali e realizzazione del progetto conclusivo.

| Indicatore                 | Evidenze da verificare                                                |
| -------------------------- | --------------------------------------------------------------------- |
| Conoscenza del linguaggio  | Utilizzo corretto di sintassi, tipi e strutture di controllo          |
| Programmazione strutturata | Capacità di definire funzioni e organizzare il codice                 |
| Programmazione OOP         | Progettazione e implementazione di classi e oggetti                   |
| Principi OOP               | Utilizzo di incapsulamento, composizione, ereditarietà e polimorfismo |
| Qualità del codice         | Utilizzo di type hints, modularità e gestione delle eccezioni         |
| Autonomia operativa        | Capacità di risolvere problemi e correggere errori                    |

Prova pratica conclusiva: realizzazione di una semplice applicazione di gestione ordini, con utenti, prodotti e metodi di pagamento, organizzata in package Python.

# 7. Competenze in uscita

Al termine delle 16 ore lo studente dovrà essere in grado di:

1. Sviluppare programmi utilizzando la sintassi e le strutture fondamentali di Python.
2. Manipolare collezioni di dati e utilizzare funzioni per organizzare la logica applicativa.
3. Progettare classi e istanze applicando i principi della programmazione orientata agli oggetti.
4. Utilizzare ereditarietà, composizione e polimorfismo per modellare situazioni applicative.
5. Gestire eccezioni e utilizzare annotazioni di tipo.
6. Organizzare un progetto Python attraverso moduli, package e ambienti virtuali.

# 8. Collegamento con i moduli successivi

Un aspetto importante della progettazione è evitare che questo modulo rimanga un corso introduttivo a Python fine a sé stesso.

Le 16 ore devono costituire la base tecnica per affrontare lo sviluppo backend.

Modulo 1 – 16 ore

Python e programmazione a oggetti

Linguaggio, strutture dati, funzioni, classi, oggetti, eccezioni e package.

Modulo successivo

Sviluppo backend con Python

Approfondimento dell'ecosistema Python, framework backend, gestione delle richieste e delle risposte HTTP.

Moduli successivi

API REST, database e persistenza

Progettazione di servizi, endpoint, accesso ai dati, ORM, validazione e gestione delle operazioni CRUD.

Progetto finale

Applicazione backend completa

Realizzazione di un servizio applicativo integrato, con API REST, database e funzionalità backend.
