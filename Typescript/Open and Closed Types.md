---
tags:
  - typescript
---
Javascript implementa il concetto di `duck typing`, ossia, un oggetto può contenere più proprietà rispetto a quelle richieste dal codice che interagisce con lui. Dal momento che le proprietà in più non verranno utilizzate nel codice che interagisce con l'oggetto, il funzionamento rimane invariato.

Per far fronte a questa caratteristiche di JS, Typescript implementa lo `structural typing`: se, per esempio, una funzione richiede un oggetto con determinate proprietà, e, come input, viene passato un oggetto che possiede le proprietà richieste più altre proprietà, il compilatore non darà errore, dal momento che le proprietà richieste sono presenti e che quindi il corretto funzionamento del codice è garantito.

Esempio:

```ts
interface Vector3D {
	x: number
	y: number
	z: number
}

function computerLengthL1(v: Vector3D) {
	return Math.abs(v.x) + Math.abs(v.y) + Math.abs(v.z)
}

const vect3Dish = {
	x: 1, 
	y: 2, 
	z: 3, 
	other: 'This property is not in Vector3D'
}

computeLengthL1(vect3Dish) // 6
```