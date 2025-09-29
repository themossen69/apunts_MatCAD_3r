## Conceptes bàsics
### Organització del processador

```ad-info
title: Vista general del HW
+ Registres de propòsit general 
	+ Registres de Dades 
	+ Registres d'adreçament 
+ Registres d'Instrucció 
	+ Program counter (PC) 
	+ Instruccion register (IR) 
+ Altres Registres 
	+ Stack Pointer 
	+ State Register 
+ Registres d'Accés a Memòria 
	+ Memory Acces Register 
	+ Memory Buffer Register 
+ Arithmetic Logic Unit 
+ Unitat de control

![[Pastedimage20250923174736.png|259x196]]
```

````ad-info
title: El que s'executa sobre el HW
```ad-note
title: Informació pròpia d'un flux
+ Comptador de programes (CP)
+ Pila
+ Registres
+ Estat del flux (en execusió, llest o bloquejat)
```

```ad-note
title: Els fluxos del mateix procés comparteixen
+ Espai de memòria
+ Variables globals
+ Obrir fitxers
+ Temporitzadors
+ Senyalització i semàfors
```

````

```ad-tip
title: visió més realista del HW
![[Pasted image 20250923181539.png|241x233]]
```

```ad-important
title: visió del HW en aquest tema
![[Pasted image 20250923181922.png]]
```

1. Utilitzem els múltiples recursos disponibles per executar diferents processos i/o fluxos que col·laboren en la resolució d'un problema al mateix temps.
2. Els `treads` (que comparteixen recursos del procés) s'executen en processadors on es comparteix memòria i els `processos` (que són independents des del punt de vista dels recursos) s'executen en processadors independents.

### Model de memòria compartida

És un model de programació paral·lela
```ad-info
title: 
+ Existeix un espai global de memòria
+ Els processos/fils d'aplicació comparteixen un espai de memòria
+ Els processos/fils de l'aplicació s'executen de manera independent i simultània
+ Necessitem mecanismes per controlar la creació/destrucció de threads
+ Necessitem mecanismes per distribuir el treball entre threads
+ Necessitem mecanismes per garantir l'exclusió mútua a l'hora d'accedir a recursis compartits (evitar condicions de carrera)
+ Necessitem mecanismes per sincronitzar els threads   
```

```ad-important
title: Condicions de carrera
Passa en sistemes concurrents (programes amb diversos fils o processos) quan dos o més tasques accedeixen i modifiquen una mateixa dada compartida alhora. 
Si no hi ha mecanismes de sincronització, el resultat pot variar segons l'ordre d'execusió. Genera errors difícils de reproduir.
```

```ad-important
title: Secció crítica
És la part del codi on s'accedeix o es modifica una dada compartida. 
```

Per evitar condicions de carrera, cal protegir la secció crítica amb mecanismes de sincronització (com semàfors o mutex), de manera que només un fil hi pugui entrar a la vegada.

S'han de garantir **tres condicions** per protegir un tram crític:
+ **Exclusió mútua**: Únicament un flux/procés pot estar a la seva SC simultàniament. Si un procés entra, cap altre podrà entrar, s'han d'esperar.
+ **Progrés**: Si cap flux/procés està a la seva SC, aleshores un flux/procés pot entrar a la seva sense espera.
+ **Espera limitada**: un procés no pot esperar de forma indefinida per entrar a la seva SC.

```ad-info
title: Semàfor
És un objecte de programació que només pot tenir un valor $\geq 0$ i amb dues operacions definifes:
+ **Wait (o P)**: Si un thread aplica aquesta operació en un semàfor que té un valor $>0$, es resta 1 del valor del semàfor i el thread continua executant-se; en cas contrari, el thread es bloqueja fins que el semàfor tingui un valor $>0$.
  
+ **Signal (o V)**: Si un thread aplica aquesta operació en un semàfor, s'afegeix 1 al seu valo i el fil continua la seva execusió. Tots els threads que estan bloquejats en una operació d'espera d'aquest semàfor es desbloquejen (i intenten esperar de nou). 
```

```ad-info
title: Mutex (**mut**ual **ex**clusion)
És un objecte de programació que pot estar en dos estats (obert o tancat) i amb dues operacions definides:
+ **Lock**: Si un thread aplica aquesta operació en un mutex **obert**, el mutex es mou a l'estat tancat i el thread continua executant-se; en cas contrari, el thread es bloqueja fins que el mutex passa a l'estat obert.
+ **Unlock**: Si un thread aplica aquesta operació en un mutex que es troba en estat **tancat**, el thread continua la seva execusió, el mutex passa a l'estat obert i es desbloquejen els threads que estan bloquejats en l'operació de bloqueig d'aquest mutex. 
```

### Model de memòria distribuïda
És un model de programació paral·lela
```ad-info
title: 
+ Cada ordinador (node) té la seva pròpia memòria local
+ Si un node necessita dades de d'un altre, no hi pot accedir directament: ha d'enviar/recollir missatges
+ Sovint es fan servir **files fantasma** *(ghost rows)* per tenir les dades de les vores dels veïns.
```

````ad-example
title: Repartir una matriu entre ordinadors
+ Si divideixes una matriu entre nodes, cadascun calcula només la seva part.
+ Però als **extrems** (primera i última fila de la seva submatriu) necessita dades del veí.
+ Solució: abans de calcular, els nodes intercanvien les seves files de frontera.  
  ```ad-example
  title: Detall del bucle de Jacobi
	+ Hi ha dues matrius: `A` (iteració anterior) i `Anew` (la nova).
	+ El càlcul de `Anew[i][j]` només utilitza dades d'`A`, que ja son conegudes (per això no cal esperar que l'altre node calculi res: només cal tenir les seves files frontera d'`A`)
	+ Procés d'una iteració:
		1. Intercanviar les formteres d'`A` 
		2. Calcular la part local i escriure a `Anew`
		3. Substituir `A = Anew` i repetir.  
  ```
````

````ad-info
title: Intercanvi de dades entre nodes
Quan tens diversos ordinadors o processos, no comparteixen memòria, així que per passar dades has d’enviar-les amb **missatges**:
+ `send()`: envia dades d'un node a un altre.
+ `recieve()`: espera a rebre dades d'un altre node
```ad-example
![[Pasted image 20250924193727.png]]
```
````

## Programació paral·lela
### Disseny d'aplicacions paral·leles
+ Aplicació, sistema i model de programació fortament relacionats
+ No es pot dissenyar una aplicació paral·lela sense tenir una idea bastant aproximada del sistema i model que s'utilitzarà

```ad-info
title: Arquitectura
+ Single instruction, Single data (SISD)
+ Multiple instructions, Single data (MISD)
+ Single instruction, multiple data (SIMD)
+ Multiple Instructions, Multiple Data (MIMD) 

  ![[Pasted image 20250924200649.png|243x239]]
```

```ad-info
title: Fonts de paralelisme
+ **Nivell de instruccions**: és el grà més fi
+ **Nivell de bucle**: utilitzar múltiples unitats aritmètiques en paralel, grà fi-mig
+ **Nivell de funcions**: al que alguns procediments del programa s'executen simultaniament. Grà mig.
+ **Nivell de programes**: quan el sistema paralel executa programes concurrentment, d'una mateixa aplicació o no. Grà gruixut.
```

`````ad-teo
title: Mètode de Foster
Divideix el problema en 4 etapes:
```ad-caixa
title: Partició
1.  El còmput i les dades es descomponen en tasques
2. Es centra l'atenció en explotar oportunitats de paral·lelisme (ignorant aspectes com el nº de processadors)
3. S'han d'evitar cómputs i assignacions redundants per afavorir l'escalabilitat de l'algoritme.
```
````ad-caixa
title: Comunicació
1. Es determina la comunicació requerida per coordinar les tasques.
	   Es defineixen els canals que conecten les tasques que requereixen dades amb les que en generes
2. Es defineixen estructures i algoritmes de comunicació.
	   S'especifica la informació o missatges que s'han d'enviar i rebre en aquests canals
   ```ad-attention
   title: Consideracions
	+ **Memòria distribuïda**: les tasques interactuen enviant i rebent missatges
	+ **Memòria compartida**: S'han d'utilitzar mecanismes de sincronització per controlar l'accés a memòria (com semàfors, barreres, etc.).
   
   ```
````

```ad-caixa
title: Agrupació
+ S'evalua el resultat de les etapes anteriors en termes d'eficiència i costos d'implementació
+ S'agrupen les tasques petites en tasques majors (si és necessari)
+ Es revisa l'algoritme obtingut evaluant si pot ser útil agrupar tasques o replicar dades i/o cómputs d'acord a la plataforma seleccionada
+ Amb l'agrupament de tasques podem reduïr la quantitat de dades a enviar i així reduïr el nº de missatges a transmetre i el cost de comunicació
```

```ad-caixa
title: Mapping
+ Cada tasca s'assigna a un processador intentant maximitzar l'us d'aquests i reduïr el cost de comunicació
+ L'assignació pot ser:
	1. **Estàtica**: abans de l'execusió del programa.
	2. **Dinàmica**: a temps de l'execusió amb algoritmes de balanç de càrrega
```
`````

### Mètriques
````ad-def
title: Speed-Up
És el factor de millora del rendiment i es defineix com:
$$
\boxed{S(n)=\frac{T(1)}{T(n)}}
$$
on:
+ $n$ és el nº de processos/recurssos
+ $T(1)$ és el temps d'execisió de l'algoritme sequencial
+ $T(n)$ és el temps d'execussió de l'algoritme paral·lel utilitzant $n$ elements de processament (PE)
  ```ad-caixa
  title: Speed-Up ideal
  $$
\boxed{S(n)=n}  
  $$
  ```
````

````ad-teo
title: Llei d'Amdahl
Estableix que el màxim *Speed-Up* que es pot obtenir d'un programa està limitat per la fracció del programa que no es pot paral·lelitzar.
$$
{T(n)=T_{s}+T_{p}}
$$
on:
+ $T_{s}=f\cdot T(1)$
+ $T_{p}=\frac{(1-f)\cdot T(1)}{n}$
+ $f \in [0,1]$ és la fracció no paral·lelitzable.
+ $n$ és el nº de processadors/recursos
$$
\boxed{T(n)=f\; T(1)+ \frac{(1-f)\;T(1)}{n}}
$$

$\implies \boxed{S(n)=\frac{1}{f+\frac{1-f}{n}}} \implies \boxed{S(\infty)=\frac{1}{f}}$

```ad-teo
title: Llei de Gustafson
Te en compte la càrrega de treball
$$
\lim_{ \text{càrrega} \to \infty } f = 0 
$$
ara $T_{p}=(1-f)\;T(1)$
$\implies T(n)=T(1)\quad$ i $\quad T(1)=f\;T(1)+n(1-f)\;T(1)$
$\implies S(n)=f+n(1-f)$
```

```ad-warning
title: Generalització
1. Equació general del temps d'execusió
$$
\boxed{T_{\alpha\beta}(p)=\alpha T_{\text{ser}}+\beta T_{\text{par}}=\alpha fT(1)+\frac{\beta(1-f)T(1)}{n}}
$$
on $f$ és la fracció no paralelitzable i $\alpha$ i $\beta$ son factors d'escalabilitat respecte a la complexitat del problema.

2. Equació general Speedup
$$
S_{\alpha\beta}(n)=\frac{T_{\alpha\beta}(1)}{T_{\alpha\beta}(n)}=\frac{\alpha f+\beta(1-f)}{\alpha f+\frac{\beta(1-f)}{n}}
$$
suposant que $\boxed{\gamma=\frac{\beta}{\alpha}}$

$$
\boxed{S_{\gamma}(n)=\frac{f+\gamma(1-f)}{f+\frac{\gamma(1-f)}{n}}}
$$

_Amb $\gamma=1$ ($\alpha=n$) tenim la **Llei d'Amdahl**_
_Amb $\gamma=n$ ($\alpha=1$ i $\beta=n$) tenim la **Llei de Gustafson**_
```

````

```ad-def
title: Eficiència
L'eficiència per un sistema amb $n$ processadors es defineix com:
$$
\boxed{E(n)=\frac{S(n)}{n}=\frac{T(1)}{nT(n)}}\quad,\;\text{amb}\; \frac{1}{n}\leq E(n)\leq 1
$$

+ És una comparació del grau de Speed-up arribat amb el valor màxim.
+ Index d'utilització de la CPU a l'hora de resoldre el problema comparat amb el temps que es gasta en comunicació i sincronització
+ L'eficiència més baixa ($E(n)\to 0$) correspon al cas en que tot el programa s'executa en un sol processador en sèrie.
+ L'eficiència màxima ($E(n)=1$), s'obté quan tots els processadors estan sent completament utilitzats durant tota la execusió.
```

````ad-def
title: Escalabilitat
Un sistema és escalable per un determinat nombre de processadors ($1\dots n$), si és possible trobar un factor d'augment de la mida de treball que faci que l'eficiència $E(n)$ del sistema es mantingui **constant**.
El problema es pot expressar com:

$$
\boxed{E(n,p)=E(k\cdot n,x\cdot p)}
$$

on:
+ $n$ és el nº de recursos
+ $p$ la mida del problema (_workload_)
+ $k\;(>1)$ el percentatge d'increment de recursos
+ $x\;(\geq1)$ el percentetge d'augment de la mida del problema
  
  ```ad-nota
  + Si **x = 1**: problema fortament escalable (*Strong Scaling*)
  + Si **x = K**: problema fràgilment escalable (*WeakScaling*)
  ```
````

````ad-caixa
La part paralelitzable $(1-f)$ no és perfectament paral·lelitzable entre $n$ recursos. 
Existeix una sobecàrrega causada per la sincronització i comunicació entre recursos:
$$T_{p}=\frac{(1-f)T(1)}{n}+\boldsymbol{T_{\text{overhead}}}$$
```ad-def
title: Cost
$$
\text{Cost}=nT(n)
$$
Normalment $\text{Cost}>T(1)$, idelament $\text{Cost}=1$
```
```ad-def
title: *Overhead* global de l'algoritme
$$
\boxed{\text{Cost}-T(1)}
$$
```
````

