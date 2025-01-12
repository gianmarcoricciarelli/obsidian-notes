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

### Docker Compose

**Docker Compose** è un tool per definire e organizzare applicazioni docker *multi-container*. Al posto di eseguire ripetutamente il comando `docker run` per ogni Container, possiamo definire tutti i Container, Network e Volume in un singolo file **YAML** chiamato `docker-compose.yml`. Con un singolo comando Docker Compose può avviare e gestire tutti questi componenti assieme.

Esempio:

```yaml
version: "3.9" # Specify Docker Compose file format version 
services: 
	web: 
		image: python:3.9-slim 
		container_name: flask_app 
		ports: 
			- "5000:5000" # Map host port 5000 to container port 5000 
		volumes: 
			- ./app:/app # Mount local directory to container 
		working_dir: /app # Set working directory inside the container 
		command: python app.py 
		depends_on: 
			- redis # Ensure Redis starts before the web service 
	redis: 
		image: redis:6.2 # Redis image 
		container_name: redis_db
```