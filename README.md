## Análisis de expresión diferencial de genes relacionados con la obesidad mediante RNA-seq (Actividad-2-Grupo-5)


La obesidad se asocia a inactividad física y a la dieta, pero en general es una condición multifactorial asociada a alteraciones metabólicas y a cambios en la regulación de múltiples genes. El análisis de expresión génica mediante RNA-seq permite estudiar estos cambios a nivel transcriptómico e identificar genes diferencialmente expresados entre distintos fenotipos. En este trabajo se analizaron perfiles de expresión simulados para evaluar diferencias asociadas a obesidad en personajes del universo de *Los Simpson*, aplicando herramientas bioinformáticas para su cuantificación, normalización e interpretación biológica.

### 1. Introducción
Contexto. La obesidad es un fenotipo complejo influido por genes que participan en la regulación del apetito, el balance energético, la señalización hormonal y la función neuronal. En esta actividad se analizó un conjunto simulado de lecturas RNA-seq de personajes de Los Simpson para comparar el perfil de expresión de un grupo con sobrepeso/obesidad frente a un grupo normopeso.
Comparación trabajada. Se resolvió la comparación Obeso1 frente a Normopeso. El grupo Obeso1 estuvo conformado por Abraham Simpson y Homer Simpson; el grupo Normopeso por Bart Simpson, Lisa Simpson y Maggie Simpson.
### 2. Hipótesis y objetivos
**Hipótesis**: Los genes relacionados con la obesidad presentarán perfiles de expresión diferentes entre los individuos del grupo Obeso1 y los individuos normopeso, especialmente en vías vinculadas con señalización de leptina, melanocortina, saciedad y metabolismo energético.

**Objetivo general**: Identificar genes diferencialmente expresados entre Obeso1 y Normopeso a partir de datos simulados de RNA-seq, interpretar su relación con el fenotipo y presentar los resultados en formato de informe científico.

**Objetivos específicos**:

•	Realizar un control de calidad básico de las lecturas FASTQ.

•	Cuantificar la expresión por gen utilizando la correspondencia transcrito-gen.

•	Normalizar los conteos para compararlos entre muestras.
•	Identificar genes diferencialmente expresados y visualizarlos mediante volcano plot y heatmap.
•	Interpretar los genes clave en relación con obesidad y regulación metabólica.
### 3. Metodología
#### 3.1 Diseño experimental

Tabla 1. Muestras usadas en la comparación Obeso1 frente a Normopeso.

|Sample  |Condition  |Age  |Sex  |
|--|--|--|--|
| **Abraham Simpson**| Sobrepeso/Obeso1| 80| Masculino|
| **Homer Simpson**| Sobrepeso/Obeso2| 40| Masculino|
| Marge Simpson| Sobrepeso/Obeso2| 38| Femenino|
| Bart Simpson| Normopeso| 10| Masculino|
| Lisa Simpson| Normopeso| 8| Femenino|
| Maggie Simpson| Normopeso| 1| Femenino|
| Patty Bouvier| Sobrepeso/Obeso2| 40| Femenino|
| Selma Bouvier| Sobrepeso/Obeso2| 40| Femenino|

Para el control de calidad usamos [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/), esta herramienta está hecha con el lenguaje de programación JAVA, la podemos descargar para nuestro sistema operativo, desde este [enlace](https://www.bioinformatics.babraham.ac.uk/projects/download.html#fastqc) y trabajar localmente en nuestras computadoras.
En este apartado usamos según nuestro grupo No. 5, Grupo Obeso1 (Familia 1, Sobrepeso/Obeso): Abraham Simpson y Homer Simpson encontramos los resultados que se muestran en las siguientes imágenes, así en cada pestaña aparecen los resultados:
<img width="600" height="300" alt="work_flow" src="src/images/FastQC.png" />

El análisis de control de calidad mediante FastQC mostró lecturas de buena calidad, sin secuencias marcadas como baja calidad y con contenido GC dentro de los rangos esperados. No se consideró necesario realizar trimming.

#### 3.2 Pipeline bioinformático aplicado
•	**Entrada**: archivos FASTQ pareados R1/R2, archivo de diseño experimental, referencia transcriptómica y tabla Transcrito_a_Gen.tsv.

•	**Control de calidad**: número de lecturas, longitud, porcentaje GC, calidad Phred media, presencia de bases N y porcentaje de asignación a gen.

•	**Cuantificación**: extracción del identificador de transcrito codificado en cada lectura simulada y conversión a gen mediante Transcrito_a_Gen.tsv; se contó una vez cada par de lecturas para evitar duplicación R1/R2.

•	**Normalización**: cálculo de factores de tamaño tipo median-ratio; todos los factores fueron 1, por lo que las cuentas normalizadas coinciden con las cuentas observadas. Como verificación adicional se calcularon tamaños de biblioteca muy similares entre muestras.

•	**Expresión diferencial**: prueba exacta de Fisher sobre cuentas agregadas por grupo, con corrección de Benjamini-Hochberg para controlar FDR. Se consideró diferencial un gen con FDR < 0,05 y |log2FC| >= 0,58, equivalente aproximadamente a un cambio de 1,5 veces.

•	**Visualización**: volcano plot, heatmap de genes diferenciales y tabla de expresión por persona y gen.
Nota metodológica. Dado que el conjunto es didáctico y simulado, los encabezados FASTQ contienen el identificador de transcrito; por ello, la cuantificación se realizó de manera reproducible usando esa información y la tabla transcrito-gen proporcionada. En un análisis real, este paso se reemplazaría por Salmon, Kallisto, STAR/featureCounts o herramientas equivalentes.


## Secuenciación y Ómicas de Próxima Generación

### Grupo No. 5, Integrantes:
|Nombre  |
|--|
| Deivis Martínez|
| Carlos Pérez|
| Freddy Rodríguez|

<div style="text-align: center;">
<img width="300" height="200" alt="Logo UNIR" src="https://upload.wikimedia.org/wikipedia/commons/d/df/Logo_UNIR.png" />
</div>

