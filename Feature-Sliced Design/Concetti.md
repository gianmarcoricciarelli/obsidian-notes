---
tags:
  - fsd
  - frontend
  - design
---
Reference: [Feature-Sliced Design](https://feature-sliced.design/).

Il **Feature-Sliced Design** è un tipo di architettura per progetti di applicazioni frontend. Ad alto livello, è un insieme di regole e convenzioni per l'organizzazione del codice.

### Layer, Slice e Segment

L'organizzazione del codice prevede l'utilizzo delle tre entità che compongono il FSD: i **Layer**, gli **Slice** e i **Segment**. Ogni entità può essere pensata come un contenitore delle entità successive, come mostrato nell'immagine sottostante:

![[concepts.jpg|Gerarchia delle tre entità del FSD, da leggersi da sinistra verso destra.]]

##### Layers

Sono le uniche entità standardizzate del FSD. Ne esistono 7 tipi, non è necessario usarli tutti durante la progettazione di un'applicazione frontend, ma i loro nomi sono importanti e vanno mantenuti durante l'organizzazione del codice. 

Come vediamo dall'immagine poco sopra, i 7 tipi sono: 
1. `app`*: tutto quello che permette all'app di funzionare - routing, entry point, global style e provider;
2. `processes` (deprecato);
3. `pages`: pagine o parti di pagine in routing annidati;
4. `widgets`: grandi porzioni di funzionalità o UI self-contained;
5. `features`: implementazioni riutilizzabili di feature di prodotto complete, ossia, azioni che portano business value all'utente;
6. `entities`: business entities utilizzate nel progetto, come, per esempio, `user` o `product`;
7. `shared`*: funzionalità riutilizzabili;

I layer contrassegnati dall'asterisco, **app** e **shared**, sono layer speciali: possono contenere soltanto dei segment.

Per un approfondimento sul concetto di Layer vedere [[Layers|il documento dedicato]].

##### Slices

Gli slice dividono il codice per **business domain**. Non hanno vincoli di nome, e se possono creare a piacimento. NON possono, tuttavia, utilizzare agli slice dello stesso layer. Nell'immagine poco sopra possiamo vedere che il layer **entities** è diviso in 3 **slice**: **user**, **post** e **comment**. Secondo quanto detto, il segment user non può usare funzionalità definite negli altri due segment e viceversa.

##### Segments

I segment dividono il codice di uno slice per il tipo di funzionalità. Similmente agli slice, non hanno vincoli di nome, anche se esistono convenzioni per i casi di utilizzo più comuni:
- `ui`: tutto quello che è collegato alla UI - componenti UI, date formatter, stili e quant'altro;
- `api`: tutto quello che permette di interagire con il backend;
- `model`: data model - *schema*, *interface*, *store* e *business logic*;
- `lib`: codice utilizzato da altri segment sullo stesso slice;
- `config`: file di configurazione e quant'altro;

### Esempio

* 📂 `app`
	* 📁 `routes`
	* 📁 `analytics`
* 📂 `pages`
	* 📁 `home`
	* 📂 `article-reader`
		* 📁 `ui`
		* 📁 `api`
	* 📁 `settings`
* 📂 `shared`
	* 📁 `ui`
	* 📁 `api`