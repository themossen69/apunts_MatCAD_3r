# Itinerari A
## Restriccions
- 1 dimensió: $-\infty\leq x \leq +\infty$
- temps universal: $-\infty\leq t \leq +\infty$

## Energia
L'energia d'una partícula $a$ $(E_{a})$ depèn de la seva massa inicial $(m_{a})$ i de la seva velocitat $(v_{a})$.
$$E\to E(m, v)$$

### Energia cinètica
$$\boxed{T=\frac{1}{2}mv^2}$$
Zones (o posicions) accessibles: $\boxed{T(x)\geq 0}$ (al contrari són zones (o posicions) inaccessibles).


### Energia potencial
(de l'objecte "a" degut a la interacció generada per l'objecte "b" a la posició "a")
 $$\boxed{U=q_aV_b}$$
 + Energia potencial gravitatòria: $U_{grav}=mg(x-x_0)$
 + Energia potencial elàstica: $U_{e}=\frac{1}{2}kx^2$

#### Potencial
Un objecte $b$ crea un potencial $V_{b}$ al seu voltant. Això governa una de les seves interaccions amb altres objectes.
$$V\to V(x,v,t,\dots)$$

+ Potencial gravitatori: $\boxed{V=g(x-x_{ref})}$
+ Potencial central: $V_{central}(r)\propto\frac{e}{r}$
	$\implies F\propto \frac{1}{x^2}$

### Energia mecànica
+ A totes les posicions accessibles: $E_m=T+U$
+ A les posicions no-accessibles: $E_m<T+U$

### Conservació de l'energia
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
#### Interaccions
Quan $a$ es mou, la seva energia cinètica canvia segons el canvi de potencial al qual està immers, escalat per la càrrega d'$a$.

## Equació d'Euler-Lagrange
$$
\boxed{\frac{d}{dt}\left( \frac{\partial L}{\partial v}\right)=\frac{\partial L}{\partial x}}
$$

on $L(x,v)=T(v)-U(x)$ és el Lagrangià.

La força (conservativa) que actua sobre l'objecte s'obté a partir de la derivada del potencial $F(x)=-\frac{dU}{dx}$.

### Acció (S)
Ens interessa que l'acció $S$ sigui mínima.
 $$\boxed{S=\int^{t_{l}}_{t_{0}}L\;dt}$$

```ad-teorema
title: Teorema de Noether
+ Si $L$ no depen del temps:
+ Si $L$ no depén de la posició:

```
### Segona llei de Newton
$$
\boxed{F_{b\to a}=m_{a}a_{a}}
$$

## Parametrització de la posició en el temps

+ $x(t)=A\cos(\omega t+\delta)$
+ $v(t)=\frac{dx}{dt}=-A\omega \sin(\omega t+\delta)$
+ $a(t)=\frac{d^{2}x}{dt^2}=-A\omega^2\cos(\omega t+\delta)$

## Sistemes de partícules
Dividim en $n$ trossos el nostre objecte $a$. Cada objecte $i$ té:
+ Massa: $m_{i}$ on $\sum_{i}m_{i}=M$
+ Posició: $x_{i}$
+ Velocitat: $v_{i}$
+ Moment: $p_{i}=m_{i}v_{i}$
	$p_{total}=\sum_{i}m_{i}v_{i}$

### Posició del centre de masses
$$
x_{CM}=\sum_{i} \frac{m_{i}}{M}x_{i}
$$
```ad-cite
$Mx_{CM}=\sum_{i}m_{i}x_{i}\implies \frac{d}{dt}(Mx_{CM})=\sum_{i} \frac{d}{dt}(m_{i}x_{i})=\sum_{i}m_{i}v_{i}=\boxed{Mv_{CM}=p_{total}}$
```

Els trossos amb més massa contribueixen més a la posició del centre de masses de l'objecte.


## Apèndix
### Notació
+ $F_{b\to a}$: Força que exerceix l'objecte $b$ sobre l'objecte $a$.
### Altres fórmules
+ $v_{i}=\frac{x_{i}(t_{k+1})-x_{i}(t_{k})}{t_{k+1}-t_{k}}=\frac{\Delta x_{i}}{\Delta t}$
+ $\omega^{2}=\frac{k}{m}$
### Constants
+ $g=9.81 [\frac{J}{kg\cdot{m}}]$
+ $m_{electró}=9.1\times10^{-31}[kg]$

### Conversions
+ $1eV=1.602\times10^{-19}J$