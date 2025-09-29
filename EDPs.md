## Introducció
Una EDP descriu una relació entre una funció desconeguda i les seves derivades parcials.

```ad-def
title: Definició: ordre
L'ordre d'una equació en derivades parcials és (en analogia amb les EDOs) l'ordre de la derivada més gran que apareix a l'equació.
```


No se per on anem
29-09-2025
````ad-caixa
title: Lleis de conservació: L'equació del trànsit
$\rho(x,t)$: densitat (de vehicles, però també de molècules, partícules, etc.)
$$
\frac{\partial \rho}{\partial t}+ \frac{\partial Q}{\partial x}=0
$$
on $Q(x,t)$ és el flux (massa que trevessa x per unitat de temps)
Tindrem $Q(x,t)=\rho(x,t)V(x,t)$ on $V(x,t)$ és la velocitat (unicament positiva).
A més establim una relació entre la velocitat i densitat: $V(x,t)=v(\rho(x,t))$, amb $v(\rho)$ decreixent.
$$
0=\frac{\partial \rho}{\partial t}(x,t)+\frac{\partial}{\partial x}q(\rho(x,t))=\frac{\partial \rho}{\partial t}+q'(\rho) \frac{\partial \rho}{\partial x}=\frac{\partial \rho}{\partial t}+ \frac{\partial \rho}{\partial x}v(\rho)+\rho v'(\rho) \frac{\partial \rho}{\partial x}=
$$

$$
\boxed{\frac{\partial \rho}{\partial t}+[v(\rho)+\rho v'(\rho)] \frac{\partial \rho}{\partial x}=0}
$$

on $q(\rho(x,t))=\rho(x,t)v(\rho(x,t))$
```ad-caixa
Suposem que $q''(\rho)<0\;,\;\forall \rho \in [0,\rho_{max}]$
```
````


## Apèndix
```ad-not
title: Notació
+ $u_{x_i}=\partial_{x_i}u=\frac{\partial u}{\partial x_i}$
+ $D^{\alpha}u=\frac{\partial^{\left\lvert \alpha \right\rvert}u}{\partial^{\alpha_1}_{x_1}\dots\partial^{\alpha_n}_{x_n}}$
	+ $\alpha = (\alpha_1, \dots, \alpha_n)\in \mathbb{N}^n$, és un multi-índex
	+ $\left\lvert \alpha \right\rvert=\sum_{i}\alpha_{i}$
  
```


$\frac{ \partial y }{ \partial x }$
$\left\lvert \alpha \right\rvert$
$D^{\alpha}u=\frac{\partial^{\left\lvert \alpha \right\rvert}u}{\partial^{\alpha_1}_{x_1}\dots\partial^{\alpha_n}_{x_n}}$
$\mathbb{N}^2$
$\left\lvert \alpha \right\rvert=\sum_{i}\alpha_{i}$