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

![[Pastedimage20250923174736.png]]
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
![[Pasted image 20250923181539.png]]
```

```ad-important
title: visió del HW en aquest tema
![[Pasted image 20250923181922.png]]
```

1. Utilitzem els múltiples recursos disponibles per executar diferents processos i/o fluxos que col·laboren en la resolució d'un problema al mateix temps.
2. Els `treads` (que comparteixen recursos del procés) s'executen en processadors on es comparteix memòria i els `processos` (que són independents des del punt de vista dels recursos) s'executen en processadors independents.

## Model de memòria compartida

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

## Model de memòria distribuïda
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

### Programació paral·lela
#### Disseny d'aplicacions paral·leles
+ Aplicació, sistema i model de programació fortament relacionats
+ No es pot dissenyar una aplicació paral·lela sense tenir una idea bastant aproximada del sistema i model que s'utilitzarà

```ad-info
title: Arquitectura
+ Single instruction, Single data (SISD)
+ Multiple instructions, Single data (MISD)
+ Single instruction, multiple data (SIMD)
+ Multiple Instructions, Multiple Data (MIMD) 

  ![[Pasted image 20250924200649.png]]
```

```ad-info
title: Fonts de paralelisme
+ **Nivell de instruccions**: és el grà més fi
+ **Nivell de bucle**: utilitzar múltiples unitats aritmètiques en paralel, grà fi-mig
+ **Nivell de funcions**: al que alguns procediments del programa s'executen simultaniament. Grà mig.
+ **Nivell de programes**: quan el sistema paralel executa programes concurrentment, d'una mateixa aplicació o no. Grà gruixut.
```