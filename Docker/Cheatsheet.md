---
tags:
  - docker
  - tools
---
Di seguito una lista dei comandi più utilizzati in Docker, con spiegazione di ogni comando ed esempi di utilizzo.

### Immagini

| Comando                         | Spiegazione                                                                             | Esempio             |
| :------------------------------ | :-------------------------------------------------------------------------------------- | :------------------ |
| `docker pull <image_name>`      | Scarica un'[[Definizioni#Image\|immagine]] dal Docker Hub o da una repository specifica | `docker pull nginx` |
| `docker images`                 | Mostra una lista delle immagini scaricate                                               | `docker images`     |
| `docker rmi <image_name_or_id>` | Rimuove un'immagine dal sistema                                                         | `docker rmi nginx`  |

### Container

| Comando                                            | Spiegazione                                                                                      | Esempio                       |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------- |
| `docker run <image_name>`                          | Esegue il [[Definizioni#Container\|container]] relativo a partire dall'immagine fornita in input | `docker run nginx`            |
| `docker run -d <image_name>`                       | Esegue un container in *detached mode* (in background).                                          | `docker run -d nginx`         |
| `docker run -p <host-port>:<container-port> image` | Mappa una port della macchina host con la porta del container                                    | `docker run -p 8080:80 nginx` |
| `docker ps`                                        | Mostra in container in esecuzione                                                                | `docker ps`                   |
| `docker ps -a`                                     | Mostra tutti i container, inclusi quelli stoppati                                                | `docker ps -a`                |
| `docker stop <container_id_or_name>`               | Stoppa un container in esecuzione                                                                | `docker stop container_id`    |
| `docker start <container_id_or_name>`              | Effettua il *restart* di un container stoppato                                                   | `docker start container_id`   |
| `docker rm <container_id_or_name>`                 | Rimuove un container stoppato                                                                    | `docker rm container_id`      |

### Volume

| Comando                                                     | Speigazione                                                                            | Esempio                               |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------- |
| `docker volume create <volume_name>`                        | Crea un *named [[Definizioni#Volume\|volume]]* per avere un *data storage* persistente | `docker volume create my_volume`      |
| `docker volume ls`                                          | Mostra tutti i volume                                                                  | `docker volume ls`                    |
| `docker run -v <volume_name>:<container_path> <image_name>` | Collega un volume ad un container                                                      | `docker run -v my_volume:/data nginx` |

### Log

| Comando                                 | Spiegazione                                                            | Esempio                       |
| --------------------------------------- | ---------------------------------------------------------------------- | ----------------------------- |
| `docker logs <container_id_or_name>`    | Mostra i log relativi al container fornito in input                    | `docker logs container_id`    |
| `docker inspect <container_id_or_name>` | Mostra informazioni dettagliate riguardo al container fornito in input | `docker inspect container_id` |

### Docker compose
