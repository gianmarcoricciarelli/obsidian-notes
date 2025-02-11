---
tags:
  - fsd
  - design
  - frontend
---
Di seguito un approfondimento sul concetto di **Layer** usato nel **Feature-Sliced Design**.

### Definizione

I Layer rappresentano il primo livello organizzativo nella gerarchia del **FSD**, hanno lo scopo di separare il codice in base a due fattori:

1. Quantità e tipo di responsabilità richieste;
2. Numero di moduli dalla quale dipende;

Esistono 7 tipi di Layer all'interno del FSD:

1. `app`
2. `processes` (**deprecato**)
3. `pages`
4. `widgets`
5. `features`
6. `entities`
7. `shared`

