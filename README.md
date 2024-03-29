# **Algoritmos Metaheurísticos para el problema TSP**


---

La presente librería implementa los algoritmos metaheurísticos siguientes:
1. Algoritmo genético
2. Colonia de hormigas
3. Algoritmo tabú
4. Selección clonal
5. Recocido simulado


#### Propósito del la librería
> La presente liberería, fue creada con motivo educativos, y únicamente resuelve
el problema de TSP, tomando en cuenta las siguientes consideraciones:
1. Los algoritmos metaheurísticos utilizan un vector con N elementos, para almacenar la ruta a seguir en las N ciudades.
2. Los valores del vector nunca se repiten, el primer valor siempre es 1 (se asume que el vendedor parte de la ciudad 1)
3. Los datos de entrada deben ser del tipo TSP (coordenadas de ciudades en 2D)
4. Los archivos TSP pueden ser descargados de TSPLIB http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/tsp/
5. Tambien es posible utilizar de entrada Matrices de Distancias en archivo  Excel, sin cabecera y sin indice (en caso de usar matriz de distancias, no es posible graficar la ruta) 

*luis.palma@unsaac.edu.pe, Luis Beltran Palma Ttito, Universidad Nacional de San Antonio Abad del Cusco*

---

## Problema TSP "Travelling Salesman Problem" (Problema del Vendedor Viajante)
*Un viajero de comercio parte de una ciudad y las distancias a otras ciudades son conocidas, ¿cuál es la **ruta óptima** que debe seguir para visitar todas las ciudades y volver a la ciudad de partida?*

---

## **0. Pasos previos**

**Paso 1**: Instalación del la librería de algoritmos metaheuristicos
```
pip install meta-lbpt
```
**Paso 2**: Importación de librerías
```
from meta_lbpt.ag import AlgoritmoGenetico
from meta_lbpt.ch import ColoniaHormiga
from meta_lbpt.at import AlgoritmoTabu
from meta_lbpt.sc import SeleccionClonal
from meta_lbpt.rs import RecocidoSimulado
```

---

## **1. Algoritmo genético**

**Paso 1.1.** Ejecutar el algoritmo genético con TSP
```
# Parametros: Generaciones, Población, ProbMutación, PoblacionElite
# burma14.tsp: Archivo que contiene las N ciudades en formato TSP (coordenadas 2D)
AG = AlgoritmoGenetico(100, 500, 0.05, 2)
Solucion, Costo, Aptitud = AG.EjecutarTSP('burma14.tsp')
print('Ruta encontrada por el algoritmo genético: ', Solucion)
print('Costo: ', Costo)
print('Aptitud: ', Aptitud)
```

```
Ruta encontrada por el algoritmo genético:  [1, 2, 10, 9, 11, 8, 13, 7, 12, 6, 5, 4, 3, 14]
Costo:  32.44685100783281
Aptitud:  0.03081963176514712
```

**Paso 1.2.** Graficar la ruta solución
```
AG.GraficaRuta()
```


**Paso 1.3** Gráfica la evolución de costo
```
AG.GraficaCosto()
```

**Paso 1.4.** Ejecutar el algoritmo genético con Matriz de Distancias
```
# Parametros: Generaciones, Población, ProbMutación, PoblacionElite
# burma14.tsp: Archivo que contiene las N ciudades en formato TSP (coordenadas 2D)
AG = AlgoritmoGenetico(100, 500, 0.05, 2)
Solucion, Costo, Aptitud = AG.EjecutarDistancia('distancia.xlsx', 'Hoja1')
print('Ruta encontrada por el algoritmo genético: ', Solucion)
print('Costo: ', Costo)
print('Aptitud: ', Aptitud)
```

---

## **2. Colonia de hormigas**

**Paso 2.1.** Ejecutar el algoritmo colonia de hormigas con TSP
```
# Parametros: Iteraciones, PoblacionHormigas, Coef. evaporación, Coef. aprendizaje
# burma14.tsp: Archivo que contiene las ciudades en formato TSP
CH = ColoniaHormiga(50, 150, 0.061, 0.65)
Solucion, Costo = CH.EjecutarTSP('burma14.tsp')
print('Mejor ruta encontrada por la colonia de hormigas: ', Solucion)
print('Costo: ',Costo)
```
```
Mejor ruta encontrada por la colonia de hormigas:  [1, 2, 3, 4, 5, 6, 12, 14, 7, 13, 9, 11, 10, 8]
Costo:  32.76917155355312
```

**Paso 2.2.** Gráfica la ruta solución
```
CH.GraficaRuta()
```

**Paso 2.3.** Gráfica la evolución de costo
```
CH.GraficaCosto()
```
**Paso 2.4.** Ejecutar el algoritmo colonia de hormigas con Matriz de Distancias
```
# Parametros: Iteraciones, PoblacionHormigas, Coef. evaporación, Coef. aprendizaje
# burma14.tsp: Archivo que contiene las ciudades en formato TSP
CH = ColoniaHormiga(50, 150, 0.061, 0.65)
Solucion, Costo = CH.EjecutarDistancia('distancia.xlsx', 'Hoja1')
print('Mejor ruta encontrada por la colonia de hormigas: ', Solucion)
print('Costo: ',Costo)
```
---

## **3. Algoritmo tabú**

**Paso 3.1.** Ejecutar el algoritmo tabú con TSP
```
# Parametros: Ciclos
burma14.tsp: Archivo que contiene ciudades en formato TSP
AT = AlgoritmoTabu(20)
Solucion, Energia= AT.EjecutarTSP('burma14.tsp')
print('Mejor ruta encontrada por algorítmo tabú: ', Solucion)
print('Energía: ', Energia)
```
```
Mejor ruta encontrada por algorítmo tabú:  [1, 8, 13, 7, 12, 6, 5, 4, 3, 14, 2, 10, 9, 11]
Energía:  31.226915109427544
```
**Paso 3.2.** Graficar la ruta solución
```
AT.GraficaRuta()
```

**Paso 3.3.** Graficar la evolución de costo
```
AT.GraficaEnergia()
```

**Paso 3.4.** Ejecutar el algoritmo tabú con TSP con Matriz de Distancias
```
# Parametros: Ciclos
burma14.tsp: Archivo que contiene ciudades en formato TSP
AT = AlgoritmoTabu(20)
Solucion, Energia= AT.EjecutarDistancia('distancia.xlsx', 'Hoja1')
print('Mejor ruta encontrada por algorítmo tabú: ', Solucion)
print('Energía: ', Energia)
```

---

## **4. Selección clonal**

**Paso 4.1.** Ejecutar el algoritmo selección clonal con TSP
```
#Parametros: Iteraciones, Población, CantClones, CantIndividuoAltaAfinidad, ProbMutacion, IncProbMutacion
burma14.tsp: Archivo con datos de ciudades en formato TSP
SC = SeleccionClonal(30, 150, 10, 5, 0.8, 1.38)
Solucion, Afinidad = SC.EjecutarTSP('burma14.tsp')
print('Ruta solución: ', Solucion)
print('Afinidad: ', Afinidad)
```
```
Ruta solución:  [1, 9, 10, 2, 14, 3, 4, 5, 6, 12, 7, 13, 11, 8]
Afinidad:  32.81277804469343
```
**Paso 4.2.** Graficar la ruta solución
```
SC.GraficaRuta()
```

**Paso 4.3.** Graficar la evolución de costo
```
SC.GraficaAfinidad()
```

**Paso 4.4.** Ejecutar el algoritmo selección clonal con Matriz de Distancias
```
#Parametros: Iteraciones, Población, CantClones, CantIndividuoAltaAfinidad, ProbMutacion, IncProbMutacion
burma14.tsp: Archivo con datos de ciudades en formato TSP
SC = SeleccionClonal(30, 150, 10, 5, 0.8, 1.38)
Solucion, Afinidad = SC.EjecutarDistancia('distancia.xlsx', 'Hoja1')
print('Ruta solución: ', Solucion)
print('Afinidad: ', Afinidad)
```

---

## **5. Recocido simulado**

**Paso 5.1.** Ejecutar el algoritmo recocido simulado con TSP
```
# Parametros: TempInicial, TempFinal, ConstanteDecremento, TiempoEnfriamiento, Cte. Bolztman
burma14.tsp: Archivo con ciudades en formato TSP
RS = RecocidoSimulado(0.99, 0.02, 0.99, 44, 0.97)
Solucion, Costo = RS.EjecutarTSP('burma14.tsp')
print('Mejor solución obtenido por enfriamiento simulado: ',Solucion)
print('Costo: ',Costo)
```
```
Mejor solución obtenido por enfriamiento simulado:  [1, 10, 9, 11, 8, 13, 7, 14, 12, 6, 5, 4, 3, 2]
Costo:  31.828317520454547
```

**Paso 5.2.** Graficar la ruta solución
```
RS.GraficaRuta()
```

**Paso 5.3.** Graficar la evolución de costo
```
RS.GraficaEnergia()
```

**Paso 5.4.** Ejecutar el algoritmo recocido simulado con Matriz de Distancias
```
# Parametros: TempInicial, TempFinal, ConstanteDecremento, TiempoEnfriamiento, Cte. Bolztman
burma14.tsp: Archivo con ciudades en formato TSP
RS = RecocidoSimulado(0.99, 0.02, 0.99, 44, 0.97)
Solucion, Costo = RS.EjecutarDistancia('distancia.xlsx', 'Hoja1')
print('Mejor solución obtenido por enfriamiento simulado: ',Solucion)
print('Costo: ',Costo)
```

---

En caso de existir consultas, escribanos al email: luis.palma@unsaac.edu.pe, Luis Beltran Palma Ttito (autor)
