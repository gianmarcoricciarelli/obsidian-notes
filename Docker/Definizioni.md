---
tags:
  - docker
  - tools
---
Di seguito alcune definizioni dei termini utilizzati nel contesto di Docker. 
Per approfondire consultare il [roadmap.sh](https://roadmap.sh/docker) dedicato a Docker.

### Image

Un'**Immagine** Docker è un file *standalone* e immutabile contenente il codice, le dipendenze, le librerie, le variabili di ambiente e i file di configurazione necessari per eseguire un'applicazione. Può essere pensato come un template per la creazione dei Container.

### Container

Un **Container** viene creato a partire da un'Immagine e rappresenta la *running instance* dell'Immagine dal quale viene creato. È un ambiente di esecuzione *standalone* che include tutto il necessario per l'esecuzione di un'applicazione in modo totalmente isolato. Il Container è isolato sia rispetto al sistema nel quale si trova sia rispetto agli altri Container. Ogni volta che un Container viene stoppato, o rimosso, perde tutti i suoi dati (*ephemeral storage*).

### Volume

Un **Volume** rappresenta un meccanismo di *data storage* usato per garantire la persistenza dei dati generati o usati all'interno di un Container. Differentemente dai container, caratterizzati dall'*ephemeral storage*, i Volume forniscono un modo per garantire che i dati non vengono perduti ogniqualvolta un Container viene stoppato o rimosso. 