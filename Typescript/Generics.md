---
tags:
  - typescript
  - generics
---

### Generic Type Arguments
Tramite i *generic* possiamo rendere dinamici la gestione dei tipi di un tipo, o di un'interfaccia. Possiamo pensare all'utilizzo dei generic in un tipo come a quello dei parametri in una funzione, il comportamento è pressoché lo stesso. La sintassi è la seguente:

```ts
interface Row<T> {
	label: string,
	value: T,
	disabled: boolean
}
```

### Generic Function Arguments
Similmente alla sezione precedente, possiamo utilizzare i generic anche per tipizzare i parametri passati ad una funzione. La sintassi prevede di inserire i generic tra parentesi angolate prima della dichiarazione della funzione, in questo modo:

```ts
const identity <T>(x: T) => x;

const mapArray = <ItemType, ReturnType>(
	arr: ItemType[], 
	fn: (x: ItemType) => ReturnType
) => arr.map(fn);
```

### Generic Type Constraints

Si usano per vincolare un tipo generico ad uno o più tipi. 
La sintassi utilizza la keyword `extends`, ed è la seguente:

```ts
type AllowString<T extends string> = T;
type AllowNumber<T extends number> = T;

type LoggerFunction = (input: number) => void;
type CreateLogger<T extends LoggerFunction> = {
	log: T,
	exit: () => void
};
```

### The Extends Keyword
La keyword `extends` ha una varietà di utilizzi, dipendenti dal contesto in cui viene utilizzata:

- Nei [[#Generic Type Constraints]] per restringere il tipo che stiamo definendo a un sottoinsieme di tipi;
- Nei [Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) funziona allo stesso modo di un `if`;
- Nelle [[Basics#Type Unions|Type Unions]] distribuisce il controllo ad ogni elemento facente parte dell'unione;

Di seguito un esempio del terzo caso per le [[Basics#Type Unions|Type Unions]]:

```ts
type Filter<T, U> = T extends U ? never : T;
type Result = Filter<'a' | 'b' | 'c', 'a' | 'c'>; // Result = 'b'