---
tags:
  - typescript
---

### Type Aliases

Typescript permette di assegnare degli alias ai tipi che uno sviluppatore può definire, la sintassi è la seguente:

```ts
type Meters = number
type Name = string;
type IsOperational = boolean;
type Payload = {
	name: Name;
	mass: Kilograms;
};
```

In questo esempio, il tipo primitivo `number` è stato assegnato all'alias `Meters`. Gli alias però non devono essere usati eccessivamente, o quando non sono necessari.

### Index Signatures

Permettono di definire il tipo delle chiavi di un oggetto.
La sintassi utilizza le parentesi quadre per la definizione del tipo della singola chiave, ed è la seguente:

```ts
type GroceryList = {
	[groceryItem: string]: number
};
```

Da notare: in Javascript, le chiavi di un oggetto sono **sempre** stringhe, nonostante si possano utilizzare numeri e altri tipi per indicizzare gli oggetti. Questo perché Javascript **converte** i tipi utilizzati in stringe (*type coercion*). Nonostante Typescript permetta di usare numeri come chiavi di oggetti, in realtà non è possibile, dal momento che Javascript si comporta come spiegato precedentemente.

### Type Unions

È possibile assegnare ad un tipo Typescript l'unione di 2 o più tipi con la seguente sintassi:

```ts
type Meters = {
	unit: 'meters';
	value: number;
};
type Miles = {
	unit: 'miles';
	value: number;
};
type Foots = {
	unit: 'feet',
	value: number,
}

type Distance = Meters | Miles | Foots;

type Position = 'top' | 'bottom' | 'left' | 'right'
```

### `typeof` Operator

L'operatore `typeof` permette di mettere in comunicazione il mondo Javascript con quello Typescript estraendo il tipo di un tipo Typescript, oppure direttamente di una variabile Javascript, per esempio, in Javascript:

```js
console.log(typeof "Euler's Number"); // -> logs the string `'string'`
```

E, in Typescript:

```ts
const createPoint = (x: number, y: number) => ({ x, y });
type CreatePoint = typeof createPoint;
```

### `keyof` Operator

L'operatore `keyof` permette  di estrarre da un tipo una *type union* contenete le chiavi del tipo fornito in input all'operatore. La sintassi è la seguente:

```ts
const casettesByArtist = { 'Alanis Morissette': 2, 'Mariah Carey': 8, 'Nirvana': 3, 'Oasis': 2, 'Radiohead': 3, 'No Doubt': 3, 'Backstreet Boys': 3, 'Spice Girls': 2, 'Green Day': 2, 'Pearl Jam': 5, 'Metallica': 5, "Guns N' Roses": 2, 'U2': 3, 'Aerosmith': 4, 'R.E.M.': 4, 'Blur': 3, 'The Smashing Pumpkins': 5, 'Britney Spears': 3, 'Whitney Houston': 3, };

type CasettesByArtist = typeof casettesByArtist;
type Artists = keyof CasettesByArtist;

// in one line --> const Artists = keyof typeof casettesByArtist; 
```

### in Operator

L'operatore `in` viene usato per verificare se un oggetto contiene o no una proprietà. Restituisce un valore booleano, e, in generale, viene usato per implementare il `type narrowing` all'interno di un blocco `if`.

```ts
interface Square {
	width: number
}
interface Rectangle extends Square {
	height: number
}
type Shape = Square | Rectangle

const s: Shape = { height: 5, width: 4 }

if ('height' in s) {
	// s is a Rectangle
} else {
	// s is a Square
}
```

### Mapped Object Types

Come Javascript ha i costrutti per i loop `while` e `for`, similmente Typescript permette di iterare le proprietà (o le chiavi) di un tipo con la seguente sintassi:

```ts
type MoviesByGenre = {
	action: 'Die Hard';
	comedy: 'Groundhog Day';
	sciFi: 'Blade Runner';
	fantasy: 'The Lord of the Rings: The Fellowship of the Ring';
	drama: 'The Shawshank Redemption';
	horror: 'The Shining';
	romance: 'Titanic';
	animation: 'Toy Story';
	thriller: 'The Silence of the Lambs';
};
type MovieInfoByGenre<T> = {
	[K in keyof T]: {
		name: string,
		year: number,
		director: string
	}
};
const test_MoviesInfoByGenre: MovieInfoByGenre<MoviesByGenre> = {
	action: {
		name: 'Die Hard',
		year: 1988,
		director: 'John McTiernan',
	},
	comedy: {
		name: 'Groundhog Day',
		year: 1993,
		director: 'Harold Ramis',
	},
	...
};
```

### Iterare un Array

È possibile iterare gli elementi di un Array attraverso una combinazione di [[#Index Signatures]], dell'operatore Typescript *in* e del tipo primitivo *number*. Di seguito un esempio:

```ts
type TupleToObject<T extends readonly (string | number | symbol)[]> = {
	[K in T[number]]: K
}
```

Attraverso l'iterazione dell'Array `T` fornito in input al tipo `TupleToObject` otteniamo un oggetto in cui le chiavi e i valori sono uguali, ossia:

```ts
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

TupleToObject<typeof tuple> = {
	'tesla': 'tesla',
	'model 3': 'model 3',
	...
}
```