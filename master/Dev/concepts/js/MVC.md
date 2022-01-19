![Model–view–controller - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/MVC-Process.svg/1200px-MVC-Process.svg.png)

```mermaid
graph TD;

	A[models]
	B[views]
	C[controllers]
	
	D[pubsub]-->A
	E[state]-->A
	F[factories]-->A
	G[renderList]-->B
	H[canvas]-->B
	I[piano]-->B
	J[eventhandler]-->C
	K[themeHandler]-->C
	
	
```