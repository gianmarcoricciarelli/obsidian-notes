---
tags:
  - typescript
---
### Cosa sono i file `*.d.ts`?

I file `*.d.ts`, chiamati anche **declaration files**, permettono di aggiungere la definizione dei tipi per del codice Javascript in un ambiente Typescript. Al loro interno troviamo esclusivamente la dichiarazione dei tipi per funzioni, classi, variabili ecc. ecc., senza i dettagli implementativi. Questi file aiutano Typescript a capire i tipi del codice Javascript a cui si riferiscono, migliorando quindi **type checking**, **code suggestion** e **developer productivity**.

### Esempi

##### Type Declaration

Supponiamo di avere un modulo Javascript che esporta una funzione `greet`

```js
export function greet(name) {
	return `Hello ${name}`
}
```

Il file `d.ts` corrispondente sarà

```ts
declare function greet(name: string): string
export greet
```

##### Dichiarazione di una variabile globale

I file `d.ts` possono essere usati anche per dichiarare una variabile globale

```ts
declare const API_URL: string
```

In questo modo potremo usare la variabile `API_URL` ovunque all'interno della code base senza doverla tipizzare ogni volta, dal momento che la definizione del tipo è fornita dal file `d.ts`.

##### Aggiungere tipi ad una Libreria

Supponiamo di volere estendere le **type definition** di `express`, il file `d.ts` corrispondente sarà

```ts
import 'express'

declare module 'express' {
	interface Request {
		user?: {
			id: string
			name: string
		}
	}
}
```

In questo modo possiamo estende l'interfaccia `Request` di `express` in modo da includere una nuova proprietà `user`.

Il framework per component e e2e testing [Cypress](https://www.cypress.io/), usato in un contesto React, non mette a disposizione una dichiarazione per il tipo del metodo `mount`, usato per renderizzare un componente all'interno del DOM di test. Possiamo ovviare a questo problema con il seguente file `.d.ts` 

```ts
import { mount } from 'cypress/react'

declare global {
	namespace Cypress {
		interface Chainable {
			mount: typeof mount
		}
	}
}
```

### In che modo interagiscono con Typescript i file `d.ts`?

Typescript include automaticamente i file `d.ts` durante la compilazione. Se posizionati correttamente all'interno della code base questi file vengono inclusi automaticamente.

Se le dichiarazioni dei tipi all'interno di un file `d.ts` non sono racchiuse all'interno di un blocco `declare module` o `declare namespace` i tipi dichiarati saranno resi disponibili a tutta la code base.

Invece, se il blocco `declare module` viene fornito, i tipi vengono applicati soltanto al modulo dichiarato ([[#Aggiungere tipi ad una Libreria|esempio]]).

Quando una libreria viene importata, Typescript controlla la libreria alla ricerca di un file `d.ts` (all'interno dei `node_modules` dove la libreria viene scaricata da un package manager). Se tale file non viene trovato, Typescript può usare il nostro file di dichiarazione `.d.ts`.