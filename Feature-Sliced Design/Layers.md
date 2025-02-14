---
tags:
  - fsd
  - design
  - frontend
---
Di seguito un approfondimento sul concetto di **Layer** usato nel **Feature-Sliced Design**.

### Introduzione

I Layer rappresentano il primo livello organizzativo nella gerarchia del **FSD**, hanno lo scopo di separare il codice in base a due fattori:

1. Quantità e tipo di responsabilità richieste;
2. Numero di moduli dalla quale dipende;

Esistono 7 tipi di Layer all'interno del FSD: ^85829d

1. `app`
2. `processes` (**deprecato**)
3. `pages`
4. `widgets`
5. `features`
6. `entities`
7. `shared`

Nella pratica non è necessario utilizzare tutti i Layer disponibili, tipicamente un'applicazione frontend si compone dei Layer `app`, `pages` e `shared`.

### Gerarchia degli import dei Layer

I Layer sono composti da **Slice**, il secondo livello organizzativo nella gerarchia del FSD. Il FSD prevede una regola per definire lo *scope* degli *import* di un file presente in uno Slice all'interno di un Layer:

> Un modulo (un file) all'interno di uno Slice può importare solo gli Slice dei Layer sottostanti, secondo la gerarchia riportata [[#^85829d|poco sopra]].

Per esempio, con la seguente struttura

- 📂 `features`
	- 📁 `aaa`
		- 📂 `api`
			- `request.ts`
	- 📁 `bbb`
- 📁 `entities`
- 📁 `shared`

Il file `request.ts` non potrà importare il codice contenuto in `bbb`, ma potrà importare tutto quello che è contenuto nei Layer `entities` e `shared`.

### Definizioni

Di seguito la definizione per ognuno dei Layer riportati [[#^85829d|poco sopra]].

##### Shared

Questo Layer rappresenta la base per il resto dell'applicazione. In questo Layer troviamo tutto quello che collega l'applicazione frontend con il mondo esterno, ossia con il *backend*, `third-party libraries` e variabili d'ambiente. Inoltre, Shared rappresenta anche il Layer nel quale possiamo definire le nostre librerie, che utilizzeremo estensivamente nel resto dell'applicazione.

Assieme al Layer `app`, `shared` non contiene Slice; è composto soltanto da **Segment**, il terzo e ultimo livello organizzativo nella gerarchia del FSD. Questo perché `shared` non contiene logica di business, e questo significa quindi che i file presenti in `shared` possono importarsi tra loro.

Tipicamente in `shared` possiamo trovare questi Segment:

- `api` -- il client per effettuare richieste al backend, e, potenzialmente, le specifiche richiesta verso gli endpoint disponibili;
- `ui` -- le componenti UI dell'applicazione. Da ricordare che i componenti in questo Segment, come negli altri, NON devono contenere **business logic**;
- `lib` -- una collezione di librerie interne. Ogni libreria in questo Segment dovrebbe far riferimento ad un'area di azione, per esempio:
	- `dates`
	- `colors`
	- `text manipulation`
- `config` -- variabili d'ambiente, configurazioni globali dell'applicazione;
- `routes` -- self-explanatory;
- `i18n` -- setup per le traduzioni, file globali di traduzioni;

##### App

