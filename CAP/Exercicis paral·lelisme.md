## 1)
La infini-norma d'una matriu A ∈ Rn×n es defineix com el màxim de les sumes dels valors absoluts dels elements de cada fila:
$$
||A||_{\infty} = \max_{i=0,\dots,n-1}\left\{ \sum_{j=0}^{n-1}|a_{i,j}| \right\}
$$
Dissenyeu, seguint la metodologia de Foster (passes 1 i 2), un algorisme paral·lel per resoldre aquest problema. La vostra resposta ha d’indicar clarament quines són les tasques mínimes que cal realitzar, quines són les dependències entre elles i quina és l’acceleració (speedup) màxim al que podem aspirar.

````ad-caixa
```ad-caixa
title: Tasques
1. **Càlcul del valor absolut de cada element de la matriu**:
   Es pot fer en paral·lel per tots els $a_{i,j}$ amb $N^2$ elements de còmput $\implies\; O(1)$.
2. **Sumatori dels valors absoluts de cada fila**:
   Es pot fer en paral·lel per cada fila. Es pot aplicar un algorisme de reducció per fer el sumatori. També amb $N^2$ elements $\implies\;O(\log(N))$
3. **Càlcul del màxim**:
   També es pot fer amb un algorisme de reducció després de la segona tasca $\implies\;O(\log(N))$
```
Com que tenim $N^2$ elements de còmput podem resoldre el problema amb $O(1+2\log(N))$ si ho fem amb paral·lel, en cas contrari es resoldria amb $O(N^2)$.
$$
S(N^2)= \frac{O(N^2)}{O(\log(N^2))}
$$
````