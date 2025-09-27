
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
J(w)=J(w_{0},w_{1})=\frac{1}{2m}\sum_{i=0}^m(f(x^i;w)-y^i)^2
$$
```

````ad-caixa
title: Descens del gradient
S'uilitza per trobar un mínim de la funció de cost.
+ Comença amb uns valors dels pesos aleatòris
+ Modifica els pesos de manera que es redueixi el valorde $J(w)$ fins que s'arriba a un mínim.
  ```ad-code
  repeat until convergence{
	$w_{j}:=w_{j}-\alpha \frac{d}{dw_{j}}J(w_{0},\dots, w_{n})\quad$  (per $j=0,\dots,n$)
  }
  ```
  on:
	+ $\frac{d}{dw_{0}}J(w_{0},w_{1})=\frac{1}{m}\sum_{i=0}^m(w_{0}+w_{1}x^i-y^i)$
	+ $\frac{d}{dw_{1}}J(w_{0},w_{1})=\frac{1}{m}\sum_{i=0}^m(w_{0}+w_{1}x^i-y^i)x^i$
  
+ Cal mantenir $\alpha$ entre $[0,1]$ per suavitzar la derivada reduïnt el salt del gradient en una iteració 
	+ si $\alpha$ és massa petit, el descens serà molt lent i si és massa gran pot no disminuir en cada iteració i pot no convergir
	+ Si no funciona el descens $\implies$ disminuir $\alpha$
+ Acostuma a convergir en un mínim local
+ Declarem convergència quan $J(w)$ es redueixi en menys de $\varepsilon$ en una iteració.
+ Separem les dades per saber quin model és el millor
	+  **Set d'entrenament**: Utilitzat per determinar els paràmetres del model.
	$$J_{\text{train}}(w)=\frac{1}{2m}\sum_{i=0}^{m}(f(x^i;w)-y^i)^2$$
	+ **Setde cross validació**: Utilitzat per triar el millor model
	$$J_{\text{cv}}(w)=\frac{1}{2m_{\text{cv}}}\sum_{i=0}^{m_{\text{cv}}}(f(x_{\text{cv}}^i;w)-y_{\text{cv}}^i)^2$$
	+ **Set de test**: Utilitzat per comprovar que funciona
	$$J_{\text{test}}(w)=\frac{1}{2m_{\text{test}}}\sum_{i=0}^{m_{\text{test}}}(f(x_{\text{test}}^i;w)-y_{\text{test}}^i)^2$$
+ Escollim el model $f_{i}$ que doni el $J_{\text{cv}}(w)$ més petit (on $i$ és el nº de pesos que hi ha)
````

```ad-caixa
title: Regressió Lineal Multivariada
$$
f(x;w)=w_{0}+w_{1}x_{1}+w_{2}x_{2}+\dots+w_{n}x_{n}
$$
```

```ad-caixa
title: Regularització en Regressió Multivariada
```

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
title_ Notació Regressió Multivalorada
+ $n$: nº de característiques
+ $x^{(i)}$: mostra (característiques) de l'exemple $i$-èssim
+ $x_{j}^{(i)}$: valor de la característica $j$ de l'exemple $i$-èssim
```