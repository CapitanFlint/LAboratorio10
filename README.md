Bruno Romero
Laboratorio 10
----

# Glosario

+ RMSD: Significa 'root-mean-square deviation of atomic positions', y es el cálculo de las distancias entre átomos de una proteína en función de su movimiento a través del tiempo (frames) a partir de una coordenada inicial.

+ SaltBridge: Es una herramienta que busca los puentes salinos que se generan entre los residuos de una proteína a través del tiempo. Considera un rango de formación de puentes salinos entre 0 y 3.2 Angstrom.

+ NAMD Energy: Es una herramienta que calcula las energías internas de la proteína a analizar en función del tiempo y en relación con un ligando o por si misma. De entre las opciones de cálculo se encuentran (obtenido de la página oficial): '_bonds, angles, dihedrals, impropers, vdW energy, electrostatic energy, conformational energy (bonds, angles, dihedrals, and impropers), nonbond energy (vdW and electrostatic energy), or all (all other energies)'_.

+ Hbonds: Básicamente calcula los puentes de hidrógeno que ocurren entre los residuos y átomos de una proteína en función del tiempo (considera trayectoria al igual que todos los otros parámetros). En su algoritmo de cálculo, considera átomo dador y aceptor y se puede personalizar la búsqueda por secciones o regiones de la proteína.


# Sección RMSD
----

### Proteína
Luego de cargar la proteína, se compararon los parámetros'backbone vs noH' en el cálculo de RMSD. Se vió que existe una diferencia cuantitativa entre las distancias de los átomos para los distintos parámetros en función del tiempo (frames). Sin embargo, el patrón de trayectoria o comportamiento de trayectoria es bastante similar, por lo que la diferencia de ausencia y presencia de hidrógenos es mayoritariamente cuantitativa y no cualitativa (__Imagen 1__). Los resultados sugieren que los hidrógenos juegan un rol significativo en la estructura espacial a través del tiempo de la proteína. Esta hipótesis se puede respaldar por el efecto que tienen los hidrógenos en la estructura espacial o terciaria de la proteína (es decir, modela junto a otros factores el plegamiento de la proteína), ya que ejercen una fuerza electrostática entre los residuos de la proteína que modelarán la estructura de la misma. Por lo que, al eliminar completamente el efecto de los hidrógenos en el cálculo de RMSD, el efecto electrotático relacionado con los mismos no estará presente y genera el resultado observado en el gráfico, mostrando que el aumento en las distancias (en Angstrom) de los átomos por 'frame', probablemente se deba a que las fuerzas electrotaticas de puentes de hidrógeno que acoplan a la proteína genera un distanciamiento sistemático entre los residuos de la proteína.

### Ligando 

Al cargar el ligando y configurar el script con los parámetros a comparar: 'resname SUV and noH vs protein and noH', se ve que hay un aumento significativo de las distancias entre las coordenadas ubicadas entre los 'frames' 55 y 60 (__Imagen 2__). Esto sugiere que a partir del 'frame' 60, la interacción proteína-ligando produce un cambio conformacional que cambia drásticamente el patrón de movimiento atómico. Es probable de que ambas, plegamiento proteico y coordenadas del ligando para ese tiempo en específico, tengan la energía de activación y los parámetros fisicoquímicos adecuados para producir ese cambio conformacional, que se reproduce en un aumento de las distancias entre átomos.

# Sección Salt Bridge
----

Al cargar la proteína en el VMD, se utilizó la herramienta Salt Bridge y se hallaron los puentes salinos para todos los 'frames'. Se obtuvieron 14 resultados y cada uno de éstos representa la interacción entre dos residuos de la proteína desde el tiempo inicial hasta el final. Los archivos creados por el script, indican que los puentes salinos de forman exclusivamente a partir de aminoácidos polares y esto coincide con la información entregada en la página oficial del programa: "_A salt bridge is considered to be formed if the distance between any of the oxygen atoms of acidic residues and the nitrogen atoms of basic residues are within the cut-off distance (default 3.2 Angstroms) in at least one frame_".

Luego, seleccioné uno de los archivos creados (GLU288-LYS284) y los valores que entregaba el archivo se analizaron en un gráfico (__Imagen 3__).
La elección del archivo fue aleatoria, debido a que no pude encontrar referencia en literatura sobre la interacción específica de orexina-SUV. Encontré varias direcciones en la página pdb, pero ninguno de los archivos .pdb concordaban con la proteína que utilizamos en este trabajo, por lo que al no poder encontrar el sitio activo exacto, tuve que escoger cualquiera. En la imagen se ve que el patrón de formación de puentes salinos es bastante uniforme, sin embargo al inicio (específicamente entre los frames 5-35) se ve una disminución significativa. A pesar, luego del frame 60 se ve que se vuelve a estabilizar.
Pienso que la información que aporta no es significativa ya que no tengo la certeza de que esa relación entre esos residuos esté y/o se deba a que se encuentra en el sitio activo.

# Sección NAMD Energy

Como se ve en la __Imagen 4__, los valores y comportamientos para los parámetros 'energía electrostática, Van der Waal y energía total' son bastante uniformes a través del tiempo. Entre los frames 30-70 se ve que hay un leve aumento en la energía total, y esto se correlaciona con el aumento de la energía electrostática y de Van der Waal para el mismo rango. En general, el comportamiento es bastante uniforme, y además, el gráfico sugiere que las energías de Van der Waal influyen más que las energías electrostáticas, y esto quizá sugiera que el plegamiento de la proteína es bastante convergente.

# Sección Hydrogen bonds

La formación de puentes de hidrógeno para los parámetros en _default_ se muestran en la __Imagen 5__. Se ve que existe un _gap_ bastate amplio entre las dos primeras formaciones y las demás. Cada _peak_ representa la formación y _destrucción_ de un puente de hidrógeno entre un dador y aceptor. Luego, para hacer un análisis comparativo, realicé el mismo procedimiento pero esta vez aumenté en 3.2 y 3.5 Angstrom la distancia máxima de interacción Dador-aceptor y consecuentemente, formación de puentes de hidrógeno. En la __Imagen 6__ se ve que no solo el eje Y aumenta, sino que además aparecen nuevas formaciones de puentes de hidrógeno. A pesar, el número de puentes de hidrógeno formados es similar en casi todas las coordenadas medidas (es sistemáticamente similar en la mayoría de los frames). 
Los puentes de hidrógeno deberían formarse entre los residuos con zonas polares (oxígeno, por ejemplo), tanto como aceptores como dadores.

# Conclusión

En general, pienso que la estabilidad (estrictamente cuando el ligando ya está en el sitio activo) es bastante significativa, ya que tal como lo muestran los distintos gráficos, tanto la movilidad como formaciones de enlaces electrostáticos y no electrostáticos es bastante uniforme a lo largo de los 101 frames que se obtuvieron en el programa VMD. Además, la molécula se visualizaba muy encerrada en la proteína, indicando que tal vez sea una causal implicada en que en primer lugar las fuerzas de interacción sean relativamente estables y en segundo lugar que no hayan diferencias significativas entre dichas fuerzas. Por otra parte, se ve que la relación entre los parámetros medidos no es tácito, sino que más bien están bastante relacionados y eso se demostró en la similitud del comportamiento de las trayectorias.
Finalmente pienso que las mediciones de estos parámetros sirven para analizar la naturaleza de la relación proteína-ligando, de forma cuantitativa como cualitativa y así tener un control e hipótesis _a priori_ del experimento _in vivo_.




