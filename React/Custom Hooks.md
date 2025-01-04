---
tags:
  - react
  - custom
  - hook
  - frontend
---
Raccolgo qui una serie di [[Terminologia#Custom Hook|custom hooks]] trovati in tutorial o articoli.

##### useMediaQuery

`useMediaQuery` permette di applicare stili o logiche specifiche basandosi sulle [media query CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries) applicate alla *size* del device ascoltato.

```tsx
import { useEffect, useState} from 'react'

function useMediaQuery(query: string) {
	const [matches, setMatches] = useState(false)

	useEffect({
		const mediaQuery: MediaQueryList = window.matchMedia(query)
		setMatches(mediaQuery.matches)

		function handler(event) {
			setMatches(event.matches)
		}
		mediaQuery.addEventListener('change', handler)

		return () => {
			mediaQuery.removeEventListener('change', handler)
		}
	}, [])
}
```

Riferimenti:
- [window.matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia)
- [MediaQueryList](https://developer.mozilla.org/en-US/docs/Web/API/MediaQueryList)