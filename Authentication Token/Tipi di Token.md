---
tags:
  - webdev
  - tokens
---
### Access Token

L'Access Token (AT) è il tipo più comune di Token. Un utente o un servizio si autentica in qualche modo e, di conseguenza, il server l'Authorization Server (AS) dispone un Access Token. Asseconda della configurazione dell'AS, il Token è tipicamente un Opaque Token, o, altrimenti, potrebbe essere un JSON Web Token ([[Formati dei Token#JSON Web Tokens (JWT)|JWT]]).

L'applicazione in genere utilizza l'AS per identificare l'utente o il servizio. Questo tipo di Token a in genere una lifespan molto breve per motivi di sicurezza. Se un attaccante dovesse ottenere l'Access Token, potrebbe ottenere l'accesso impersonando l'utente o il servizio.

### Bearer Token

L'utilizzo più comune per gli Access Token è come Bearer Token. Con questo si intende che sarà garantito l'accesso al portatore (bearer) del Token. Con questo tipo di Token non sono presenti check da parte dell'applicazione o dall'API che ricevono il Token su chi invia il Token. Di conseguenza, un Token potrebbe essere dirottato da un attaccante, e usato per ottenere l'accesso all'applicazione o all'API. L'utilizzo dei Bearer Token impone più requisiti sull'applicazione in termini di sicurezza sul Token stesso.

### Refresh Token

Quando gli Access Token sono forniti agli utenti, essi richiedono uno step di autenticazione. Tuttavia, Token con un lifespan molto breve potrebbe risultare sconvenienti per l'utente, dal momento che in questa situazione l'utente dovrebbe costantemente re-autenticarsi per avere accesso a un nuovo Token attivo. In questo caso i Refresh Token risolvono la situazione.
Al momento di fornire un Access Token, l'Authentication Server può fornire anche un Refresh Token. Quando l'AT non è più valido e c'è bisogno di un nuovo Token, l'applicazione o l'API può richiedere un flow Refresh Token, che, se presentato, previene l'utente dal doversi autenticare di nuovo.