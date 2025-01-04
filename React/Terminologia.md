---
tags:
  - react
  - frontend
---

### Separation of Concerns

Il termine `Separation of Concerns` è ampiamente usato nel contesto della programmazione. In generale, con Separation of Concerns si intende che l'implementazione di logiche che svolgono compiti differenti non dovrebbero essere raggruppate o combinate insieme. Un esempio pratico nel contesto di React è che le logiche di recupero di dati (da un server o da un'altra fonte qualsiasi) non dovrebbero essere mischiate con quelle di UI che li presentano all'utente.


### Prop Drilling

Con il termine `Prop Drilling` si intende la pratica ***SCORRETTA*** di passare prop di padre in figlio per molti livelli nella gerarchia dei componenti. Un esempio di Prop Drilling sarebbe, quindi, quello di un componente che inoltra una qualsiasi prop ad un componente figlio al di sotto di lui di 2 o più livelli.

### Custom Hook

I `Custom Hook` sono hook implementati dallo sviluppatore, e quindi non presenti tra quelli disponibili in React come `useState`, `useEffect` ecc., per coprire delle necessità non raggiungibili attraverso l'uso degli hook standard della libreria. Essendo degli hook a tutti gli effetti, anche i `Custom Hook` seguono le regole degli hook di libreria, in più, come convenzione, il loro nome deve cominciare **SEMPRE** con `use`.

Utilizzando i `Custom Hook` è possibile:
1. Condividere lo stesso blocco di logica tra più componenti;
2. Estrarre la logica da un componente ed incapsularla in un unico posto, facilitando quindi la manutenzione ed i test del codice estratto, e rendendo più snello il codice del componente dal quale la logica è stata estratta;

Riferimenti:
- [Reusing Logic with Custom Hooks](https://react.dev/learn/reusing-logic-with-custom-hooks#custom-hooks-let-you-share-stateful-logic-not-state-itself)