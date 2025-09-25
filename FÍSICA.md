# Itinerari A
## Restriccions
```ad-caixa
title: 
+  1 dimensió: $-\infty\leq x \leq +\infty$
+  temps universal: $-\infty\leq t \leq +\infty$
```


## Energia
L'energia d'una partícula $a$ $(E_{a})$ depèn de la seva massa inicial $(m_{a})$ i de la seva velocitat $(v_{a})$.
$$E\to E(m, v)$$

```ad-caixa
title: Energia cinètica
$$\boxed{T=\frac{1}{2}mv^2}$$
Zones (o posicions) accessibles: $\boxed{T(x)\geq 0}$ (al contrari són zones (o posicions) inaccessibles).
```

````ad-caixa
title: Energia potencial
(de l'objecte "a" degut a la interacció generada per l'objecte "b" a la posició "a")
 $$\boxed{U=q_aV_b}$$
 + Energia potencial gravitatòria: $U_{grav}=mg(x-x_0)$
 + Energia potencial elàstica: $U_{e}=\frac{1}{2}kx^2$
```ad-def
title: Potencial
Un objecte $b$ crea un potencial $V_{b}$ al seu voltant. Això governa una de les seves interaccions amb altres objectes.
$$V\to V(x,v,t,\dots)$$

+ Potencial gravitatori: $\boxed{V=g(x-x_{ref})}$
+ Potencial central: $V_{central}(r)\propto\frac{e}{r}$
	$\implies F\propto \frac{1}{x^2}$
```
````

```ad-caixa
title: Energia mecànica
+ A totes les posicions accessibles: $E_m=T+U$
+ A les posicions no-accessibles: $E_m<T+U$
```

````ad-caixa
title: Conservació de l'energia
$$
\Delta T_{a}=-\Delta U_{a}
$$
$$
\boxed{T_{a}(x_{a1})-T_{a}(x_{a2})=-q_{a}(V_{b}(x_{a1})-V_{b}(x_{a2}))}
$$
que també ho podem escriure com
$$
\boxed{T(x_{a1})+U(x_{a1})=T(x_{a2})+U(x_{a2})}
$$

```ad-caixa
title: Interaccions
Quan $a$ es mou, la seva energia cinètica canvia segons el canvi de potencial al qual està immers, escalat per la càrrega d'$a$.
```
````

## Equació d'Euler-Lagrange
$$
\boxed{\frac{d}{dt}\left( \frac{\partial L}{\partial v}\right)=\frac{\partial L}{\partial x}}
$$

on $L(x,v)=T(v)-U(x)$ és el Lagrangià.

La força (conservativa) que actua sobre l'objecte s'obté a partir de la derivada del potencial $F(x)=-\frac{dU}{dx}$.

````ad-def
title: Acció (S)
Ens interessa que l'acció $S$ sigui mínima.
 $$\boxed{S=\int^{t_{l}}_{t_{0}}L\;dt}$$

```ad-teo
title: Teorema de Noether
+ Si $L$ no depen del temps:
+ Si $L$ no depén de la posició:

```
````

```ad-caixa
title: Segona llei de Newton
$$
\boxed{F_{b\to a}=m_{a}a_{a}}
$$
```

## Parametrització de la posició en el temps

```ad-caixa
+ $x(t)=A\cos(\omega t+\delta)$
+ $v(t)=\frac{dx}{dt}=-A\omega \sin(\omega t+\delta)$
+ $a(t)=\frac{d^{2}x}{dt^2}=-A\omega^2\cos(\omega t+\delta)$
```


## Sistemes de partícules
Dividim en $n$ trossos el nostre objecte $a$. Sistema de n objectes on cada objecte $i$ té:
+ Massa: $m_{i}$ on $\boxed{\sum_{i}m_{i}=M}$
+ Posició: $\vec{x}_{i}$
+ Velocitat: $\vec{v}_{i}=\frac{d \vec{x}_{i}}{dt}$
+ Moment: $\boxed{\vec{p}_{i}=m_{i}\vec{v}_{i}}$
	$\boxed{\vec{p}_{total}=\sum_{i=1}^{n}\vec{p}_{i}=\sum_{i=1}^{n}m_{i}\vec{v}_{i}}$

````ad-caixa
title: Posició del centre de masses
$$
\boxed{\vec{x}_{CM}=\sum_{i} \frac{m_{i}}{M}\vec{x}_{i}}
$$
```ad-cite
title: Derivant
$M \vec{x}_{CM}=\sum_{i}m_{i}\vec{x}_{i}\implies \frac{d}{dt}(M \vec{x}_{CM})=\sum_{i} \frac{d}{dt}(m_{i}\vec{x}_{i})=\sum_{i}m_{i}\vec{v}_{i}=\sum_{i}\vec{p}_{i}$

Identifiquem:
+ $\vec{p}_{CM}=\sum_{i}\vec{p}_{i}=\frac{d}{dt}(M \vec{x}_{CM})$
+ $\vec{p}_{CM}=M \vec{v}_{CM}\implies \vec{v}_{CM}=\frac{\vec{p}_{CM}}{M}$
```

Els trossos amb més massa contribueixen més a la posició del centre de masses de l'objecte.
````

```ad-caixa
title: Moviment dels components del sistema
$$
\boxed{\vec{x}_{i}=\vec{x}_{CM}+\vec{x}_{CM\to i}}
$$
on $\vec{x}_{CM\to i}$ és la posició de l'objecte *relativa* al centre de masses
$$
\vec{v}_{i}=\frac{d \vec{x}_{i}}{dt}=\frac{d \vec{x}_{CM}}{dt}+\frac{d \vec{x}_{CM\to i}}{dt}=\vec{v}_{CM}+\vec{u}_{i}
$$
on $\vec{u}_{i}$ és la velocitat de l'objecte *relativa* al centre de masses. És la velocitat en un sistema de referència que es mou amb $\vec{v}_{CM}$.
$$
\vec{p}_{i}=m_{i}\vec{v}_{i}=m_{i}\vec{v}_{CM}+m_{i}\vec{u}_{i}
$$
on $m_{i}\vec{u}_{i}$ és el moment de l'objecte expressat en un sistema de referència que es mou amb $\vec{v}_{CM}$.
```

```ad-caixa
title: Sistema de referència del centre de masses
Sumant sobre tots els objectes del sistema
$\vec{p}_{CM}=\sum_{i}\vec{p}_{i}=\sum_{i}(m_{i}\vec{v}_{CM})+\sum_{i}(m_{i}\vec{u}_{i})=M\vec{v}_{CM}+\sum_{i}(m_{i}\vec{u}_{i})$
$\implies \boxed{\sum_{i}^{n}(m_{i}\vec{u}_{i})=\vec{0}}$

La suma dels moments dels components del sistema és nula en el sistema de referències CM.
```

```ad-caixa
title: Forces sobre un sistema i moment
Considerant el sistema com un únic objecte "$a$":
$$\sum_{j}\vec{F}^{\text{ext}}_{j\to a}=\frac{d \vec{p}_{a}}{dt}$$

Considerant el sistema compost per n torssos:
$$\frac{d\vec{p_{a}}}{dt}=\frac{d}{dt}\left( \sum_{i=1}^{n}\vec{p_{i}} \right)=\sum_{i=1}^{n} \frac{d\vec{p_{i}}}{dt}=\sum_{i=1}^{n}\sum_{k\ne i}\vec{F}_{k\to i}$$

on $k$ etiqueta els components del sistema i els objectes externs: $k=1\dots n,n+1\dots m$
```

```ad-caixa
title: Forces externes i internes
$\frac{d\vec{p}_{a}}{dt}=\sum_{i=1}^n \sum_{k=1}^n \vec{F}_{k\to i}+\sum_{i=1}^n \sum_{k=n+1}^m \vec{F}_{k\to i}$

on $\sum_{i=1}^n \sum_{k=1}^n \vec{F}_{k\to i}=\vec{0}$.
```

```ad-caixa
title: La tercera llei de Newton
La suma de les forces internes del sistema es pot ordenar per parelles d'acció-reacció:
$$\sum_{i=1}^n \sum_{k=1}^n \vec{F}_{k\to i}=\vec{F}_{1\to2}+\vec{F}_{2\to1}+\vec{F}_{1\to3}+\vec{F}_{3\to1}+\dots+\vec{F}_{n-1\to n}+\vec{F}_{n\to n-1}$$

+ Si cada parell d'acció-reacció suma 0, la suma total serà nul·la.
+ Tercera llei de Newton: $\boxed{\vec{F}_{a\to b}=-\vec{F}_{b\to a}}$
+ Origen: La suma de les forces internes d'un sistema ha de ser nul·la.
```

```ad-caixa
title: "Conservació" de moment (linal)
+ La suma de les forces internes en un sistema és 0
+ La segona llei de Newton per un sistema és:
  $$\boxed{\frac{d \vec{p}_{a}}{dt}=\frac{d}{dt}\left( \sum_{i=1}^n \vec{p}_{i} \right)=\sum_{j}F_{j}^{\text{ext}}}$$
+ Si la suma de forces **externes** és nul·la, el moment total del sistema és constant:
  $$
  \frac{d}{dt}\left( \sum_{i=1}^n \vec{p}_{i} \right) = \vec{0} \implies \sum_{i=1}^n \vec{p}_{i}= \text{vector constant}
$$
```



## Apèndix
```ad-not
title: Notació
+ $F_{b\to a}$: Força que exerceix l'objecte $b$ sobre l'objecte $a$.
```

```ad-caixa
title: Altres fórmules
+ $v_{i}=\frac{x_{i}(t_{k+1})-x_{i}(t_{k})}{t_{k+1}-t_{k}}=\frac{\Delta x_{i}}{\Delta t}$
+ $\omega^{2}=\frac{k}{m}$
```

```ad-caixa
title: Constants
+ $g=9.81 [\frac{J}{kg\cdot{m}}]$
+ $m_{electró}=9.1\times10^{-31}[kg]$
```

```ad-caixa
title: Conversions
+ $1eV=1.602\times10^{-19}J$
```
