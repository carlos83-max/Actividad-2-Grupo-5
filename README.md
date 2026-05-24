1. Introducción
Contexto. La obesidad es un fenotipo complejo influido por genes que participan en la regulación del apetito, el balance energético, la señalización hormonal y la función neuronal. En esta actividad se analizó un conjunto simulado de lecturas RNA-seq de personajes de Los Simpson para comparar el perfil de expresión de un grupo con sobrepeso/obesidad frente a un grupo normopeso.
Comparación trabajada. Se resolvió la comparación Obeso1 frente a Normopeso. El grupo Obeso1 estuvo conformado por Abraham Simpson y Homer Simpson; el grupo Normopeso por Bart Simpson, Lisa Simpson y Maggie Simpson.
2. Hipótesis y objetivos
Hipótesis. Los genes relacionados con la obesidad presentarán perfiles de expresión diferentes entre los individuos del grupo Obeso1 y los individuos normopeso, especialmente en vías vinculadas con señalización de leptina, melanocortina, saciedad y metabolismo energético.
Objetivo general. Identificar genes diferencialmente expresados entre Obeso1 y Normopeso a partir de datos simulados de RNA-seq, interpretar su relación con el fenotipo y presentar los resultados en formato de informe científico.
Objetivos específicos:
•	Realizar un control de calidad básico de las lecturas FASTQ.
•	Cuantificar la expresión por gen utilizando la correspondencia transcrito-gen.
•	Normalizar los conteos para compararlos entre muestras.
•	Identificar genes diferencialmente expresados y visualizarlos mediante volcano plot y heatmap.
•	Interpretar los genes clave en relación con obesidad y regulación metabólica.
3. Metodología
3.1 Diseño experimental
Tabla 1. Muestras usadas en la comparación Obeso1 frente a Normopeso.
Muestra	Condición	Edad	Sexo
AbrahamSimpson	Sobrepeso/Obeso1	80	Masculino
HomerSimpson	Sobrepeso/Obeso1	40	Masculino
BartSimpson	Normopeso	10	Masculino
LisaSimpson	Normopeso	8	Femenino
MaggieSimpson	Normopeso	1	Femenino
3.2 Pipeline bioinformático aplicado
•	Entrada: archivos FASTQ pareados R1/R2, archivo de diseño experimental, referencia transcriptómica y tabla Transcrito_a_Gen.tsv.
•	Control de calidad: número de lecturas, longitud, porcentaje GC, calidad Phred media, presencia de bases N y porcentaje de asignación a gen.
•	Cuantificación: extracción del identificador de transcrito codificado en cada lectura simulada y conversión a gen mediante Transcrito_a_Gen.tsv; se contó una vez cada par de lecturas para evitar duplicación R1/R2.
•	Normalización: cálculo de factores de tamaño tipo median-ratio; todos los factores fueron 1, por lo que las cuentas normalizadas coinciden con las cuentas observadas. Como verificación adicional se calcularon tamaños de biblioteca muy similares entre muestras.
•	Expresión diferencial: prueba exacta de Fisher sobre cuentas agregadas por grupo, con corrección de Benjamini-Hochberg para controlar FDR. Se consideró diferencial un gen con FDR < 0,05 y |log2FC| >= 0,58, equivalente aproximadamente a un cambio de 1,5 veces.
•	Visualización: volcano plot, heatmap de genes diferenciales y tabla de expresión por persona y gen.
Nota metodológica. Dado que el conjunto es didáctico y simulado, los encabezados FASTQ contienen el identificador de transcrito; por ello, la cuantificación se realizó de manera reproducible usando esa información y la tabla transcrito-gen proporcionada. En un análisis real, este paso se reemplazaría por Salmon, Kallisto, STAR/featureCounts o herramientas equivalentes.
4. Resultados
4.1 Control de calidad y cuantificación
Tabla 2. Control de calidad básico de las muestras comparadas.
Muestra	Pares leídos	Lecturas totales	Longitud lectura (bp)	GC (%)	Q medio	N (%)	Asignación a gen (%)
AbrahamSimpson	1320	2640	151	46.100	36.060	0.000	100.000
BartSimpson	1328	2656	151	46.200	36.090	0.000	100.000
HomerSimpson	1320	2640	151	45.980	36.040	0.000	100.000
LisaSimpson	1320	2640	151	46.230	36.010	0.000	100.000
MaggieSimpson	1328	2656	151	45.930	36.070	0.000	100.000
Interpretación del control de calidad. Todas las muestras tienen lecturas de 151 pb, calidad Phred media cercana a 36, porcentaje GC estable alrededor de 46 %, ausencia de bases N y asignación a gen del 100 %. Estos indicadores permiten continuar con la cuantificación sin aplicar recorte de baja calidad en esta simulación.
Tabla 3. Tamaño de biblioteca y factor de normalización.
Muestra	Cuentas totales por muestra	Factor de tamaño
AbrahamSimpson	1320	1.000
BartSimpson	1328	1.000
HomerSimpson	1320	1.000
LisaSimpson	1320	1.000
MaggieSimpson	1328	1.000
Interpretación de normalización. Los tamaños de biblioteca fueron muy cercanos entre sí, con 1320 a 1328 pares por muestra; los factores de tamaño calculados fueron 1, lo que indica ausencia de sesgo relevante por profundidad de lectura en esta simulación.
4.2 Genes diferencialmente expresados
Tabla 4. Genes diferencialmente expresados entre Obeso1 y Normopeso.
Gen	Media Obeso1	Media Normopeso	log2FC	p valor	FDR	Regulación en Obeso1
LEPR	56.000	18.667	1.535	1.99e-12	7.35e-11	Sobreexpresado
MC4R	8.000	26.667	-1.620	9.30e-07	1.72e-05	Subexpresado
PCSK1	56.000	32.000	0.788	3.82e-05	2.83e-04	Sobreexpresado
POMC	56.000	32.000	0.788	3.82e-05	2.83e-04	Sobreexpresado
SH2B1	56.000	32.000	0.788	3.82e-05	2.83e-04	Sobreexpresado
BDNF	32.000	56.000	-0.788	9.25e-05	3.80e-04	Subexpresado
CADM2	32.000	56.000	-0.788	9.25e-05	3.80e-04	Subexpresado
LEP	32.000	56.000	-0.788	9.25e-05	3.80e-04	Subexpresado
NTRK2	32.000	56.000	-0.788	9.25e-05	3.80e-04	Subexpresado
Resumen del resultado. Se detectaron 9 genes diferenciales: 4 sobreexpresados en Obeso1 y 5 subexpresados en Obeso1. Los cambios más marcados fueron LEPR sobreexpresado y MC4R subexpresado en Obeso1.
 
Figura 1. Volcano plot de la comparación Obeso1 frente a Normopeso. Los genes etiquetados cumplen FDR < 0,05 y |log2FC| >= 0,58.
 
Figura 2. Heatmap de genes diferenciales. La línea vertical separa las muestras Obeso1 de las normopeso; los valores representan z-score de log2(cuentas normalizadas + 1).
 
Figura 3. Promedio de expresión normalizada en genes diferenciales por grupo.
Tabla 5. Expresión por persona y gen para los genes diferenciales.
Gen	AbrahamSimpson	HomerSimpson	BartSimpson	LisaSimpson	MaggieSimpson
LEPR	56	56	16	24	16
PCSK1	56	56	32	32	32
POMC	56	56	32	32	32
SH2B1	56	56	32	32	32
BDNF	32	32	56	56	56
LEP	32	32	56	56	56
CADM2	32	32	56	56	56
NTRK2	32	32	56	56	56
MC4R	8	8	32	16	32
5. Discusión e interpretación biológica
Patrón general. Los resultados muestran un patrón coherente con alteraciones en vías de regulación del apetito y balance energético. En Obeso1 se observó aumento de LEPR, POMC, PCSK1 y SH2B1, y disminución de MC4R, BDNF, NTRK2, LEP y CADM2. En conjunto, estos resultados sugieren que el fenotipo simulado de Obeso1 se asocia con cambios en señalización leptina-melanocortina, procesamiento neuroendocrino y señalización neurotrófica.
 
Tabla 6. Interpretación funcional de genes clave.
Gen	Dirección	Interpretación funcional breve
LEPR	Sobreexpresado	Receptor de leptina; participa en señalización de leptina, metabolismo de grasas y regulación del peso corporal.
PCSK1	Sobreexpresado	Convertasa que procesa prohormonas; relacionada con metabolismo energético y regulación neuroendocrina.
POMC	Sobreexpresado	Precursor de péptidos anorexigénicos implicados en la vía melanocortina y el control de la ingesta.
SH2B1	Sobreexpresado	Proteína adaptadora asociada a señalización de leptina e insulina; variantes se han vinculado con obesidad.
BDNF	Subexpresado	Factor neurotrófico vinculado a plasticidad neuronal y regulación de apetito/saciedad.
LEP	Subexpresado	Leptina; hormona adipocitaria que informa reservas energéticas y regula apetito mediante el eje leptina-melanocortina.
CADM2	Subexpresado	Molécula de adhesión celular con asociaciones reportadas con rasgos metabólicos y comportamiento alimentario.
NTRK2	Subexpresado	Receptor de BDNF; participa en señalización neurotrófica relacionada con regulación alimentaria.
MC4R	Subexpresado	Receptor melanocortina 4; su señalización hipotalámica reduce la ingesta y favorece balance energético.
Genes sobreexpresados en Obeso1. LEPR mostró el mayor incremento. Esto puede interpretarse como una posible respuesta compensatoria o alteración de la vía de leptina en el grupo con sobrepeso/obesidad. POMC y PCSK1 pertenecen a una ruta neuroendocrina que participa en el procesamiento de péptidos implicados en saciedad; SH2B1 se relaciona con la señalización de leptina e insulina, por lo que su aumento también es compatible con cambios en regulación metabólica.
Genes subexpresados en Obeso1. La disminución de MC4R es relevante porque este receptor participa en la vía melanocortina y en el control de la ingesta. También disminuyeron BDNF y NTRK2, componentes de la señalización neurotrófica vinculada con regulación neuronal del apetito. LEP aparece menor en Obeso1 en estos datos simulados; aunque en obesidad humana suele describirse hiperleptinemia en muchos contextos, este resultado debe interpretarse como una señal específica del dataset simulado y no como una generalización clínica.
Relación con el fenotipo. El perfil obtenido apoya la hipótesis de que los individuos Obeso1 tienen un patrón de expresión diferente en genes relacionados con obesidad. La combinación de LEPR alto y MC4R/BDNF/NTRK2 bajos apunta a una posible disrupción de circuitos de saciedad, señalización hormonal y regulación de la ingesta.
6. Análisis funcional cualitativo y rutas implicadas
•	Vía leptina-melanocortina: LEP, LEPR, POMC, PCSK1 y MC4R.
•	Regulación neuronal del apetito y saciedad: BDNF y NTRK2.
•	Señalización metabólica y respuesta a hormonas: SH2B1 y LEPR.
•	Rasgos conductuales/metabólicos asociados a ingesta o adiposidad: CADM2.
Este enriquecimiento se presenta como interpretación cualitativa porque el conjunto diferencial contiene pocos genes y procede de una simulación. En un estudio real se recomienda usar g:Profiler, Enrichr, clusterProfiler o KEGG/Reactome para obtener términos enriquecidos con significancia estadística.
7. Conclusiones
•	El control de calidad fue adecuado: lecturas de 151 pb, Q medio cercano a 36, GC estable y ausencia de bases N.
•	La cuantificación generó una matriz de 37 genes relacionados con obesidad; los tamaños de biblioteca fueron muy similares entre muestras.
•	Se identificaron 9 genes diferencialmente expresados entre Obeso1 y Normopeso con FDR < 0,05 y |log2FC| >= 0,58.
•	Los genes sobreexpresados en Obeso1 fueron LEPR, POMC, PCSK1 y SH2B1; los genes subexpresados fueron MC4R, BDNF, NTRK2, LEP y CADM2.
•	Los resultados apoyan la hipótesis de diferencias en vías relacionadas con leptina, melanocortina, saciedad y regulación metabólica; sin embargo, al tratarse de datos simulados, la interpretación debe considerarse didáctica.
8. Limitaciones y mejoras
•	El número de réplicas es reducido, especialmente en Obeso1, con solo dos individuos.
•	La cuantificación se realizó usando identificadores simulados; en datos reales se debe alinear o pseudoalinear contra una referencia con herramientas especializadas.
•	La prueba exacta de Fisher sobre cuentas agregadas es una aproximación didáctica; para publicación se recomienda DESeq2, edgeR o limma-voom con estimación de dispersión.
•	El análisis no incluye covariables como sexo o edad, que podrían influir en la expresión génica.
•	Sería recomendable validar genes clave con otro conjunto de datos o mediante qPCR.
9. Anexo: matriz de expresión completa de la comparación
Tabla 7. Matriz de cuentas por gen y por muestra usada para el análisis principal.
Gen	AbrahamSimpson	HomerSimpson	BartSimpson	LisaSimpson	MaggieSimpson
ADCY3	32	32	32	32	32
AGRP	32	32	32	32	32
ANKRD27	32	32	32	32	32
ANO4	32	32	32	32	32
BDNF	32	32	56	56	56
CADM1	32	32	32	32	32
CADM2	32	32	56	56	56
CALCR	32	32	32	32	32
CNR1	64	64	64	64	64
CREBRF	32	32	32	32	32
DPP9	32	32	32	32	32
FTO	32	32	32	32	32
GIPR	32	32	32	32	32
GPR151	64	64	64	64	64
GPR75	32	32	32	32	32
KIAA0586	32	32	32	32	32
KIAA1109	32	32	32	32	32
KSR2	32	32	32	32	32
LEP	32	32	56	56	56
LEPR	56	56	16	24	16
MC4R	8	8	32	16	32
MRAP2	32	32	32	32	32
NRP1	32	32	32	32	32
NRP2	32	32	32	32	32
NTRK2	32	32	56	56	56
PCSK1	56	56	32	32	32
PDE3B	32	32	32	32	32
PHIP	32	32	32	32	32
POMC	56	56	32	32	32
PPARG	32	32	32	32	32
ROBO1	32	32	32	32	32
SH2B1	56	56	32	32	32
SIM1	32	32	32	32	32
SPARC	32	32	32	32	32
TMEM18	32	32	32	32	32
UBR2	32	32	32	32	32
UHMK1	32	32	32	32	32
10. Referencias bibliográficas
1.	Anders, S., & Huber, W. (2010). Differential expression analysis for sequence count data. Genome Biology, 11, R106.
2.	Benjamini, Y., & Hochberg, Y. (1995). Controlling the false discovery rate: a practical and powerful approach to multiple testing. Journal of the Royal Statistical Society: Series B, 57(1), 289-300.
3.	Love, M. I., Huber, W., & Anders, S. (2014). Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. Genome Biology, 15, 550.
4.	Patro, R., Duggal, G., Love, M. I., Irizarry, R. A., & Kingsford, C. (2017). Salmon provides fast and bias-aware quantification of transcript expression. Nature Methods, 14, 417-419.
5.	NCBI Gene. Ficheros data_report.jsonl y secuencias FASTA proporcionados en TallerGrupal_Ficheros, genes humanos relacionados con obesidad.
6.	OMIM, GeneCards y PubMed. Bases de datos recomendadas para interpretación funcional de genes asociados a obesidad.
