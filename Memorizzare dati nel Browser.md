---
tags:
  - frontend
  - local
  - storage
  - session
---
La `Frontend`, possiamo memorizzare dati all'interno del Browser sfruttando due oggetti web tra di loro simili, ma con alcune differenze fondamentali: `localStorage` e `sessionStorage`. Tra i vantaggi di usare questo tipo di approccio per la memorizzazione dei dati abbiamo

1. I dati memorizzati utilizzando i due oggetti di storage non vengono inviati al server, e, per questo motivo, possiamo memorizzarne di più. Il limite di memorizzazione è intorno ai 2 MB, dipende dal browser.
2. Il server non può manipolare la memorizzazione degli oggetti tramite HTTP header; tutto viene fatto tramite Javascript.
3. L’archiviazione è legata alla sorgete (origin) (domain/protocol/port triplet). Questo perché, protocolli differenti o sotto domini deducono diverse archiviazioni a oggetti e non possono accedere ai dati tra di loro.

Le due archiviazioni a oggetti propongono stessi metodi e proprietà:

- `setItem(key, value)`: memorizza la coppia key/value.
- `getItem(key)`: lettura del valore dalla key.
- `removeItem(key)`: rimuove la key, ed il relativo value.
- `clear()`: rimuove tutti gli elementi.
- `key(index)`: lettura della key all’indice `index`.
- `length`: il numero di oggetti archiviati.

| `localStorage`                                                                      | `sessionStorage`                                                                                       |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| I dati sono condivisi tra tutte le tab e finestre provenienti dalla stessa sorgente | I dati sono condivisi soltanto all'interno di un tab del browser, incluso iframe della stessa sorgente |
| I dati sopravvivono al riavvio del browser                                          | I dati sopravvivono al refresh della pagina ma non alla chiusura della tab                             |
