
## Regressió de dades
```ad-caixa
title: Què és?
+ Ens permet fer prediccions sobre valors numèrics
+ Aquesta predicció es fa a partir d'una combinació d'una o més variables
+ La seva tasca és construir un model $f$ que permeti predir una resposta numèrica a partir d'unes variables que defineixen un problema
```

Volem  fer $f(x;w)$ **proper** a $y$ pels $m$ exemples $(x,y)$ d'aprenentatge. Quantifiquem com de proper és amb una **funció de cost** (ens interessa minimitzar-la).

```ad-caixa
title: Amb una variable (recta)
$$
\hat{y}=f(x;w)=w_{0}+w_{1}x
$$
Funció de cost:
$$
J(w)=J(w_{0},w_{1})=\frac{1}{2m}\sum_{i=1}^m(f(x^i;w)-y^i)^2
$$
```

```ad-caixa
title: Regressió Lineal Multivariada
$$
f(x;w)=w_{0}+w_{1}x_{1}+w_{2}x_{2}+\dots+w_{n}x_{n}
$$
Funció de cost:
$$
J(w)=J(w_{0},w_{1}, \dots, w_{n})=\frac{1}{2m}\sum_{i=1}^m(f(x^i;w)-y^i)^2
$$
```

````ad-caixa
title: Descens del gradient
S'uilitza per trobar un mínim de la funció de cost.
+ Comença amb uns valors dels pesos aleatòris
+ Modifica els pesos de manera que es redueixi el valor de $J(w)$ fins que s'arriba a un mínim.
  ```ad-code
  repeat until convergence{
	$w_{j}:=w_{j}-\alpha \frac{d}{dw_{j}}J(w_{0},\dots, w_{n})\quad$  (per $j=0,\dots,n$)
  }
  ```
+ Cal mantenir $\alpha$ entre $[0,1]$ per suavitzar la derivada reduïnt el salt del gradient en una iteració 
	+ si $\alpha$ és massa petit, el descens serà molt lent 
	+ si $\alpha$ és massa gran pot no disminuir en cada iteració i pot no convergir
		+ Si no funciona el descens $\implies$ disminuir $\alpha$
+ Acostuma a convergir en un mínim local
+ Declarem convergència quan $J(w)$ es redueixi en menys de $\varepsilon$ en una iteració.
  ```ad-caixa
  title: Com triar bé el model?
    1. **Normalització**
     Fer que les característiques estiguin en una escala similar 
     ($-1\leq x_{i}\leq 1\implies x_{i_{\text{new}}}=\frac{\text{mida}-\mu_{i}}{\sigma_{i}}$)
	2. **Separem les dades en 3 conjunts**
		+  **Set d'entrenament**: Utilitzat per determinar els paràmetres del model.
	$$J_{\text{train}}(w)=\frac{1}{2m}\sum_{i=0}^{m}(f(x^i;w)-y^i)^2$$
		+ **Set de validació creuada**: Utilitzat per triar el millor model
	$$J_{\text{cv}}(w)=\frac{1}{2m_{\text{cv}}}\sum_{i=0}^{m_{\text{cv}}}(f(x_{\text{cv}}^i;w)-y_{\text{cv}}^i)^2$$
		+ **Set de test**: Utilitzat per comprovar que funciona
	$$J_{\text{test}}(w)=\frac{1}{2m_{\text{test}}}\sum_{i=0}^{m_{\text{test}}}(f(x_{\text{test}}^i;w)-y_{\text{test}}^i)^2$$
	3. **Avaluar els models sobre el conjunt de validació**
		+ Escollim el model $f_{i}$ que doni el $J_{\text{cv}}(w)$ més petit (on $i$ és el nº de pesos que hi ha) i comprovem que generalitzi bé amb $J_{\text{test}}(w)$.
		+ **Avaluar l'_overfitting/underfitting_ de cada model**
		Mirem $J_{\text{train}}(w)$ i $J_{\text{cv}}(w)$
			+ Si $J_{\text{train}}(w)=0$ o molt proper a 0
				+ Si $J_{\text{cv}}(w)$ és alt $\implies$ _OVERFITTING_
				+ Si $J_{\text{cv}}(w)$ és baix $\implies$ _CORRECTE_
			+ Si $J_{\text{train}}(w)$ és alt $\implies$ $J_{\text{cv}(w)}$ també serà alt i hi haurà _BIAS_ (model massa senzill)
	4. **Evitar _overfitting_**
	    1. Reduïr manualment el nº de paràmetres 
		    + Seleccuinem les característiques que ens volem quedar
		    + Apliquem algun algorisme de selecció automàtica de característiques
		2. Regularització automàtica 
			Penalitzem els models molt complexes, ara
			$$J(w)=\frac{1}{2m}\left[ \sum_{i=1}^m(f(x^i;w)-y^i)^2+\lambda \sum_{j=1}^n w_{j}^2 \right]$$
			+ Si $\lambda$ gran $\implies$ _UNDERFIT_
			+ Si $\lambda$ intermig $\implies$ _CORRECTE_
			+ Si $\lambda$ petita $\implies$ _OVERFIT_
	5. **Demanar més dades**
	L'overfitting pot anar be si tenim MOLTES dades (és dificil que al ficar mes dades sigugi diferent a les que tens)
  ```
+ Regularització + descens de gradient
```ad-code
Repeat{
$w_{0}:=w_{0}-\frac{\alpha}{m}\sum_{i=0}^m(f(x^i;w)-y^i)$
$w_{j}:=w_{j}-\frac{\alpha}{m}\left[\sum_{i=1}^m (f(x^i,w)-y^i)·x_{j}^i - \lambda w_{j}\right]$
}
```
````


## Classificació
Busquem etiquetar dades segons patrons
```ad-def
title: Definició del problema
+ **Entrada**: les dades d'aprenentatge són parelles $(x_{i},y_{i})$ d'atributs $x_{i}$ i d'etiquetes $y_{i}$ amb la classe coneguda
+ **Sortida**: Un classificador $f$ que pot predir l'etiqueta de la classe a partir d'una mostra
+ **Tasca**: Predir el valor de la funció per a una nova mostra, després d'haver vist un número d'exemples d'aprenentatge
+ L'aprenentatge ha de generalitzar a partir de les dades disponibles cap a noves situacions no observades, d'una manera raonable  
```

`````ad-caixa
title: Classificació **binària**
+ Funció **sigmoidea**
$$
f(x;w)=\frac{1}{1+e^{-w^Tx}}
$$
on $w^Tx$ és el polinomi $w_{0}+w_{1}x_{1}+w_{2}x_{2}+\dots+w_{n}x_{n\quad}$ i $\quad0\leq f(x;w)\leq 1$
  - Si $f(x;w)\leq 0.5\implies\text{Classe1}$
  - Si $f(x;w)> 0.5\implies\text{Classe2}$

+ Funció de cost
  $$
\text{Cost}(f(x^i;w),y^i)=
\begin{cases} 
-\log(f(x^i;w)) & \text{si}\;y=1 \\
-\log(1-f(x^i;w)) & \text{si}\; y=0
\end{cases} 
$$

+ Descens de gradient
  $$
J(w)=-\frac{1}{m}\left[ \sum_{i=1}^m y^i\log(f(x^i;w))+(1-y^i)\log(1-f(x^i;w)) \right]
$$
```ad-code
Repeat{
$w_{j}:=w_{j}-\alpha \frac{d}{dw_{j}}J(w_{0},w_{1},\dots,w_{n})$
$w_{j}:=w_{j}-\frac{\alpha}{m}\sum_{i=1}^m(f(x^i;w)-y^i)x_{j}^i$
}
```
````ad-caixa
title: Màquines de vectors de suport (SMV)
Generen una frontera que separa les classes. Pot ser tant lineal com no lineal.
Donat un conjunt de dades numèriques d'aprenentatge:
$(\vec{x}_{1},y_{1}),\dots,(\vec{x}_{n},y_{n}),\vec{x} \in \mathbb{R}^d, y \in \{-1,1\}$

Volem trobar $w$: $-1\leq f(x;w)\leq_{1}$
que millor aproxima la funció de classificació desconeguda.

El  vector $w$ representarà una separació lineal de l'hiperplà on:
$$
f(x;w)=b+w_{1}x_{1}+w_{2}x_{2}+\dots+w_{n}x_{n}=b+w^Tx
$$
1. Assigna per producte escalar cada mostra a una classe
	+ $>1$ per mostres de la classe +1
	+ $<-1$ per mostres de la classe -1 
2. Maximitza els marges de separació entre classes
$$
d(x,w)= \frac{b+w^Tx}{||w||} = \frac{1}{||w||}
$$
$$
\text{marge}=d^++d^- = \frac{2}{||w||}
$$
$\implies \boxed{\text{min}\; \frac{1}{2}||w||^2}$
3. Les mostres més properes entre classes s'anomenen **vectors de suport**
   
Hi ha màquines de vectors de suport que se'n diuen _Soft margin_ que permeten errors per maximitzar el marge entre classes.

També existeixen SVM no-lineals on trobem els anomenats _**Kernels**_
````
`````

`````ad-caixa
title: Regressió logística multiclasse
Podem fer-ho entrenant un classificador $f^i(x;w)=\mathbb{P}(y=i|x;w)$ per cada classe $i$ per predir la probabilitat que $y=i$.
En una nova mostra $x$, per fer la predicció, escollim la classe $i$ que maximitza:
$$\max_{i}f^i(x;w)$$
````ad-caixa
title: Bagging & Boosting
Es pot donar el cas que hi hagi confusió entre classes i, per exemple, dues funcions donin molt properes a 1 (i no sabem quina triar).
Per solucionar això, utilitzem un conjunt de classificadors simples per cada classe i que cada un es centri en un cert parametre de la classe. Per cada mostra escollim la classe que hagi predit la majoria dels classificadors d'aquesta.
+ **BAGGING**
  Construeix diferents classificadors a partir de diferents dades, fent que cada classificador es centri en un aspecte concret de la nostra distribució. S'entrenen els classificadors amb dades diferents.
	1. Modifica el conjunt d'aprenentatge mitjançant la **selecció aleatòria** d'elements d'aquest conjunt, construint així les dades per a cada classificador.
	2. Els classificadors són agregats calculant el vot majoritari
	```ad-not
	title: 
	Tenim $B$ classificadors $\in \{-1,1\}: c^1,c^2,\dots,c^B$
	El classificador agregat és:
	$$
	\boxed{c_{\text{bag}}(x)=\text{sign}\left(  \frac{1}{B}\sum_{b=1}^B c^b(x) \right)}
	$$
	```
+ **BOOSTING**
  A partir de totes les dades s'apren un primer classificador. Aleshores mira quins errors s'han comés i crea un altre classificador que s'espaciellitza amb els errors que ha comés el primer classificador. Amb els errors d'aquest últim es crearà un tercer de la mateixa manera, etc.
	1. Dades resamplejades adaptivament: **pujar els pesos** dels patrons mal classificats, baixar-los si estan ben classificats.
	2. Els classificadors són agregats per votació ponderada
	```ad-not
	title: 
	+ Inicialitzar els pesos: $w_{i}^1=\frac{1}{N}$
	+ Calcular el classificador amb aquests pesos
	+ Calcular nous pesos: $w_{i}^{b+1}=w_{i}^{b}\exp[-y_{i}f_{b}(x_{i})]$
	+ El classificador agregat és:
	$$
	\boxed{c_{\text{boost}}=\text{sign}\left[ \sum_{b=1}^B f_{b}(x) \right]}
	$$

	```
````
`````

## Apèndix
```ad-not
title: Notació Regressió lineal
+ $m$: nº d'exemples d'entrenament
+ $x$: variable d'entrada (característiques)
+ $y$: variable de sortida (resposta, objectiu)
+ $w_{i}$: Paràmetres, coeficients, o pesos
+ $\varepsilon$: Tolerància
```

```ad-not
title: Notació Regressió Multivalorada
+ $n$: nº de característiques
+ $x^{(i)}$: mostra (característiques) de l'exemple $i$-èssim
+ $x_{j}^{(i)}$: valor de la característica $j$ de l'exemple $i$-èssim
```

```ad-not
title: Notació regresió logística
+ Conjunt d'entrenament: $\{(x^{(1)},y^{(1)}),(x^{(2)},y^{(2)}),\dots,(x^{(m)},y^{(m)})\}$
+ $m$ exemples:
  $$
x \in
\begin{bmatrix}
x_{0} \\
x_{1} \\
\vdots \\
x_{n}
\end{bmatrix}
\quad x_{0}=1,\;y \in\{0,1\}
$$
```