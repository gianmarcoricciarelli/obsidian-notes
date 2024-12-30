---
tags:
  - frontend
  - vite
  - plugin
---
Di seguito una collezione di plugins per [Vite](https://vite.dev/):
- [vite-tsconfig-paths](https://github.com/aleclarson/vite-tsconfig-paths#readme): abilita l'uso dei [path alias](https://www.typescriptlang.org/tsconfig/#paths) di Typescript per i progetti che usano Vite come bundler;
- [vite-plugin-svgr](https://github.com/pd4d10/vite-plugin-svgr#readme): permette di trasformare gli SVG in componenti React, utilizzando [svgr](https://github.com/gregberge/svgr) per la conversione. Una volta aggiornato il file di configurazione di vite, per utilizzare il plugin è necessario importare i file SVG utilizzando il query parameter `?react`. Così facendo viene segnalato al bundler di convertire il file SVG in componente React;