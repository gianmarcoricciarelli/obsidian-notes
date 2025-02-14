---
tags:
  - design
---
SOLID è l'acronimo che definisce i 5 principi fondamentali per lo sviluppo software nel mondo **Object Oriented**. Creati da [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin), ogni principio rappresenta una pratica da seguire durante lo sviluppo software per evitare di ricadere in *bad practice* e, in generale, seguire un percorso armonico e coerente.

Vengono definiti nel modo seguente:

- S - [[#^b76aac|Single-Responsability Principle]];
- O - [[#^14aab8|Open-Closed Principle]];
- L - Liskov Substitution Principle;
- I - Interface Segregation Principle;
- D - Dependency Inversion Principle;

### Single-responsability Principle

^b76aac

> *A class should have one and only one reason to change, meaning that a class should have only one job.*

Ossia, idealmente, ogni classe, o funzione se ci trovassimo in un contesto funzionale piuttosto che in un contesto OO (*Object Oriented*), deve avere soltanto uno scopo, e quindi un solo motivo per cambiare il proprio stato.

### Open-Closed Principle

^14aab8

> *Objects or entities should be open for extension but closed for modification*

