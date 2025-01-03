---
tags:
  - react
  - design
  - frontend
---
### Container/Presentational Pattern

In generale, viene considerata una pratica sbagliata quella di implementare logiche di UI per presentare dei dati o dei contenuti e logiche di recupero o manipolazione di questi dati o contenuti nello stesso componente. Utilizzando il Presentational Pattern possiamo rafforzare il concetto di [[Terminologia#Separation of Concerns|Separation of Concerns]], separando quindi questi due tipi di logiche.

##### Definizione

Il Presentational Pattern prevede la separazione delle logiche di UI da quelle di business tramite l'implementazione di due componenti:

1. **Presentational Component**: il componente che si occuperà di come i dati vengono presentati all'utente. Riceve i dati da presentare attraverso le **prop** e si occupa soltanto di mostrarli all'utente applicando gli stili corretti, senza modificare i dati ricevuti in input.
2. **Container Component**: il componente che si occuperà di recuperare, manipolare e decidere che tipo di dati vengono presentati all'utente. L'unica sua funzione è quella di passare i dati recuperati e, eventualmente, manipolati, al Presentational Component, che è contenuto al suo interno. Dal momento che di per sé non effettua render di alcun tipo, non prevede l'uso di stili o altro che possa essere definito UI.

Per facilitare lo sviluppo, se le logiche di recupero e manipolazione dei dati diventano complesse e difficili da mantenere con il crescere della code base, è buona pratica racchiuderle all'interno di un [[Terminologia#Custom Hook|custom hook]].

##### Esempio

```tsx
// Presentational Component: Transaction in Transaction.tsx

interface TransactionProps {
	id: number,
	amount: number,
	name: string,
}

export default function Transaction({ id, amount, name }: TransactionProps) {
	const _className = // Styles' implementation
	
	return (
		<div className={_className}>
			{/* UI Implementation  */}
		</div>
	)
}
```

```tsx
// Container Component: Transactions in Transactions.tsx

export default function Transactions() {
	const transactions = fetchTransactions() // get the data

	return (
		<div>
			{
				transactions.map((transaction) => ( // pass the data
					<Transaction
						key={transaction.id}
						id={transaction.id}
						amount={transaction.amount}
						name={transaction.name}
					/>
				))
			}
		</div>
	)
}
```

### Composition Pattern

In uno scenario nel quale abbiamo un componente che, con il passare del tempo e con il cambiare dei [[Frontend System Design#Functional Requirements|functional requirement]], diventa complesso da mantenere per via dell'aumento del numero di prop e, di conseguenza, delle sue logiche interne, possiamo usare il Composition Pattern per facilitare lo sviluppo ed il mantenimento del codice.

##### Definizione

Il Composition Pattern prevede di spezzare un componente *monolitico* in una serie di sotto-componenti, tutti accessibili allo sviluppatore, la cui unione permetterà di creare facilmente varianti del componente originale. 
Inoltre, tramite il Composition Pattern, sarà più facile gestire la logica e lo stile del componente originale, dal momento che sarà sufficiente andare a modificare singolarmente i sotto-componenti, piuttosto che dover aggiungere codice al componente monolitico.

Riassumendo, utilizzando il Composition Pattern abbiamo i seguenti vantaggi:

1. Riduzione del [[Terminologia#Prop Drilling|Prop Drilling]]
2. Facilità di controllo dei singoli sotto-componenti
3. Facilità nella creazioni di varianti del componente originale
4. Più chiarezza nella struttura del componente composito

##### Esempio di implementazione

Supponiamo di avere un componente *CallToActionButton* che, all'occorrenza, oltre a mostrare un testo all'interno del bottone, può anche mostrare un'icona sulla destra, sulla sinistra o da entrambi i lati del testo. Un'implementazione *composita* del componente potrebbe essere la seguente:

```tsx
// CallToActionButton.tsx

interface CallToActionRootProps extends React.ComponentProps<'button'> {
	variant?: 'primary' | 'secondary';
	size?: 'small' | 'large';
}

function CallToActionRoot({
	variant = 'primary',
	size = 'small',
	className,
	children,
	onClick
}: CallToActionRootProps) {
	const classes = ... // Define styles based on variant, size, and className

	return (
		<button className={classes} onClick={onClick}>
			{children}
		</button>
	);
}

export function CallToActionIcon({ props }: {props: React.ComponentProps<'Icon'>} ) {  
	return <Icon {...props} />;  
};

export function CallToActionText({ children, ...props }: React.ComponentProps<'span'>) {
	return <span {...props}>{children}</span>
}

export const CallToActionButton = {
	Root: CallToActionRoot,
	Icon: CallToActionIcon,
	Text: CallToActionText,
};
```

Avendo definito così il componente composito, l'utilizzo sarà il seguente:

```tsx
// anotherFile.tsx

// Variant with the Icon placed on the left
<CallToActionButton.Root>
	<CallToActionButton.Icon name="+" color="red" size{20} />
	<CallToActionButton.Text>Add more</CallToActionButton.Text>
</CallToActionButton.Root>

// Variant with the Icon placed on the right
<CallToActionButton.Root>
	<CallToActionButton.Text>Add more</CallToActionButton.Text>
	<CallToActionButton.Icon name="+" color="red" size{20} />
</CallToActionButton.Root>

// Other variants...
```

### High Order Components (HOC)