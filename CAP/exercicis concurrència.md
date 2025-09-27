
## 1)
Dos pobles veïns es troben separats per un riu molt cabalós que només pot ser creuat fent servir un pont romà. Per aquest pont només poden creuar fins a 20 persones alhora en el mateix sentit. Això vol dir que:   
+ Si una persona vol creuar en un sentit i hi han persones creuant en l’altre, caldrà que esperi fins que el pont quedi lliure.  
+ Si una persona vol creuar en un sentit i davant seu hi han 20 persones creuant en el mateix sentit, caldrà que esperi a que el nombre de persones creuant sigui menor que 20 per no sobrecarregar el pont.  
  
L’acció de creuar el pont està modelada per una rutina (que no cal implementar) que anomenarem `creuar()`.

```C
int creuant_p12 = 0;
int creuant_p21 = 0;
tsem lliure = 20;
tmutex m_p12;
tmutex m_p21;

Persona_p12{
    lock(m_p12);
        creuant_p12++;
        if(creuant_p12 == 1){
            lock(m_p21);
        }
    unlock(m_p12);

    wait(lliure);
        creuar();
    signal(lliure);

    lock(m_p12);
        creuant_p12--;
        if (creuant_p12==0){
            unlock(m_p21);
        }
    unlock(m_p12);
}


```

## 2)
El govern d’un estat fictici està avaluant la possibilitat de construir un nou aeroport. Inicialment volen veure com funcionaria si es dotés amb tres pistes que podrien ser utilitzades tant per aterrar com per enlairar-se, però, evidentment, només per un avió alhora. En aquest projecte, ens encarreguen escriure un pseudo-codi basat en l’ús de semàfors i/o mutexs que descrigui el protocol que hauria de fer servir un avió que vulgui enlairar-se per accedir a una de les tres pistes. Tenim la següent informació:  
  
+ Les pistes tenen noms (A, B i C),  
+ L’acció d’enlairar-se està modelada per una rutina (que no cal implementar) que anomenarem `Enlairar(n)`, la qual rep com a paràmetre el nom de la pista que es farà sevir.  
+ L’estat del sistema està descrit per tres variables compartides anomenades `estat_pA`, `estat_pB` i `estat_pC`. Si la variable val `1`, vol dir que la pista corresponent és lliure (cap avió la fa servir per aterrar o enlairar-se en aquest moment), si val `0`, vol dir que la pista està ocupada.

```C
int estat_pA = 1; // 1 significa lliure, 0 ocupada
int estat_pB = 1;
int estat_pC = 1;

tsem lliure = 3; // capacitat aeroport
tmutex m;

Enlairar_avió{
    char pista; //lletra de la pista que ocuparà
    wait(lliure);
        lock(m);
            if (estat_pA){
                pista = "A";
                estat_pA = 0;
            } else if (estat_pB){
                pista = "B";
                estat_pB = 0;
            } else {
                pista = "C";
                estat_pC = 0;
            }
        unlock(m);

        enlairar(pista); // equivalent a despegar()

        lock(m);
            if (pista == "A"){
                estat_pA = 1;
            } else if (pista == "B"){
                estat_pB = 1;
            } else {
                estat_pC = 1;
            }
        unlock(m);
    signal(lliure);
}
```



Hola Àjan, molt bona feina! Veiem que aquest any t'estàs implicant molt amb les assignatures i estàs intentant portar-ho tot al dia, excel·lent! Ens alegrem que estiguis fent apunts tant bonics i tant currats, ets un 10!

Et donem molts records des del Satorras! 
Atentament, 
Jaume Bachs i Anna Sanchís.