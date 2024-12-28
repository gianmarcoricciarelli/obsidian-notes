---
tags:
  - frontend
  - design
  - webdev
  - project
---
Questo documento contiene alcune linee guida per impostare un progetto frontend. Lo scopo è quello di delineare una serie di punti fermi, che dovranno essere rispettati durante la fase di sviluppo, in modo da evitare che lo sviluppo prenda una strada sbagliata e che il prodotto finale sia in linea con le aspettative del team/cliente.

### Requirements

- **Component Structure**: delineare i componenti principali dell'architettura frontend e in che modo si relazionano tra di loro;
- **State Management**: delineare in che modo lo stato dell'applicazione verrà gestito all'interno dell'applicazione frontend;
- **User Authentication**: discutere in che modo gestire l'autenticazione dell'utente in modo da garantire l'accesso sicuro all'applicazione ([[Tipi di Token]]);
- **UI/UX Considerations**: discutere le varie considerazioni riguardo le user interface e la user experience (responsive design, dark mode, ecc. ecc.);

IMPORTANTE: In questa fase si può scendere nel dettagli ed evidenziare le varie tecnologie che si potrebbero usare in ogni punto, ma è IMPORTANTE mantenere la discussione ad alto livello, dal momento la fase di implementazione sarà in uno step successivo.

##### Functional Requirements

Sono le feature del prodotto che gli sviluppatori devono implementare al fine di soddisfare i requisiti dell'utente.

Alcuni esempi:
- L'applicazione deve mandare un'email di conferma ogni volta che un ordine viene creato;
- L'applicazione deve permettere ai visitatori del blog di sottoscriversi alla newsletter con la loro email;
- L'applicazione deve permettere agli utenti di verificare il loro account usando il loro numero di telefono;

##### Non-Functional Requirements

Fanno parte dei Non-Functional Requirements cose come:
- **Ottimizzazione delle performance**: l'applicazione deve garantire il livello più alto possibile di performance, in modo da fornire un'esperienza utente ottimale;
- **Scalabilità**: l'applicazione deve poter gestire grandi quantità di dati senza impattare sull'esperienza utente;
- **Security**: deve essere garantito un accesso sicuro all'applicazione;

### Data Model

In questa fase viene delineato l'aspetto che i dati dovranno avere all'interno dell'applicazione. Per esempio, nel caso di una chat simile a WhatsApp, la fase di Data Modeling potrebbe essere simile al seguente blocco di codice:

```ts
interface User {
	id: string;
	name: string;
	image?: string;
	status: 'offline' | 'online';
	lastSeen?: Date;
}

interface Message {
	id: string;
	clientId: string;
	conversationId; string;
	content: string;
	sentAt: Date;
	sender: User['id'];
	status: 'sending' | 'sent' | 'delivered' | 'read' | 'failed';
	retryCount?: number;
}

interface Conversation {
	id: string;
	partecipants: User[];
	lastMessage?: Message;
	lastMessageAt?: Date;
}
```