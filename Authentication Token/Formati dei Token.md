---
tags:
  - tokens
  - webdev
---
### Opaque Tokens

Gli Opaque Token, conosciuti anche come Reference Token, sono stringhe generate randomicamente, e per questo uniche, dall'Authorization Server. In genere, sia [[Tipi di Token#Access Token|Access Token]] che [[Tipi di Token#Refresh Token|Refresh Token]] sono opaque token, e di conseguenza non forniscono nessun dato all'applicazione o all'API. Questo aiuta a prevenire potenziali leak di informazioni contenute nel Token da parte delle applicazioni pubbliche. Un Opaque Token può essere passato in giro senza il rischio di rivelare Personally Identifiable Information (PI) riguardo all'utente.

Esempio di un Opaque Token: `087258a5-ddb2–487e-a38e-071698896ff9`

### JSON Web Tokens (JWT)

Il JSON Web Token (JWT) è un formato di Token molto diffuso. Consiste in un header, un body, un payload e una signature. Il formato JWT in base64 separa le tre sezioni con un punto.

Esempio di JSON Web Token: `xxxxx.yyyyy.zzzzz`

L'header contiene metadata riguardanti il Token e gli algoritmi utilizzati per generarlo, un esempio:

```
{
	"alg": "HS256", 
	"typ": "JWT"
}
```

Il payload consiste nei dati veri o propri e contiene informazioni riguardanti il creatore del Token, l'utente e l'autorizzazione dell'utente. Un esempio:

```
{ 
	"sub": "1234567890", 
	"name": "John Doe", 
	"admin": true 
}
```

Infine, la signature è usata per verificare l'integrità del Token e verrà utilizzata per garantire che il Token non sia stato manipolato.