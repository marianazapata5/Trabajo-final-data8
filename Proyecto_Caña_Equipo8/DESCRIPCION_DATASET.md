# Descripción del dataset

**Nombre:** Sugarcane Leaf Disease Classification Dataset.
**Publicador en Kaggle:** anant1302.
**Fuente:** https://www.kaggle.com/datasets/anant1302/sugarcane-leaf-disease-classification-dataset
**Versión descargada:** 1.
**Consulta y análisis:** 26 de octubre de 2026.
**Licencia indicada por la ficha:** MIT.

El conjunto contiene imágenes JPEG de hojas de caña de azúcar, organizadas en carpetas por categoría. Las siguientes interpretaciones corresponden a las etiquetas y descripciones del publicador; el equipo no confirmó patógenos mediante pruebas de laboratorio.

| Etiqueta original | Interpretación de la ficha | Imágenes originales | Tras retirar duplicados exactos |
|---|---|---:|---:|
| Asymptomatic | Sin síntomas visibles | 522 | 476 |
| Colletotrichosis | Categoría asociada a Colletotrichum y pudrición roja | 518 | 518 |
| Puccinia | Categoría asociada a roya | 514 | 447 |
| SCMV | Categoría asociada al virus del mosaico de la caña | 462 | 376 |
| SCYLV | Categoría asociada al virus de la hoja amarilla | 505 | 494 |
| **Total** | | **2.521** | **2.311** |

Las cantidades proceden del conteo real de archivos de esta descarga. Ningún archivo resultó ilegible y no se encontraron duplicados exactos con etiquetas contradictorias. Se retiraron 210 repeticiones de contenido de píxeles, conservando la primera según orden alfabético de ruta.

En las 2.311 imágenes conservadas, el ancho varía entre 240 y 1.600 píxeles y el alto entre 292 y 1.600. Son imágenes RGB con proporciones variables. La extracción de características reduce el lado mayor a 256 píxeles, sin deformar la relación de aspecto.

## Partición usada en el análisis

Partición estratificada por grupos de similitud (`StratifiedGroupKFold`, semilla 42, ejecución en Google Colab con scikit-learn 1.6.1):

| Etiqueta | Entrenamiento | Prueba |
|---|---:|---:|
| Asymptomatic | 383 | 93 |
| Colletotrichosis | 415 | 103 |
| Puccinia | 357 | 90 |
| SCMV | 301 | 75 |
| SCYLV | 395 | 99 |
| **Total** | **1.851** | **460** |

**Sesgo de captura detectado:** el tamaño de la imagen está asociado a la clase (por ejemplo, la mayoría de las fotos de Puccinia miden 780×1040 y las de SCYLV 493×1040). Un árbol de decisión que solo usa ancho y alto obtiene F1 macro de 0,48 en prueba, frente a 0,07 de la referencia (Sección 10 Notebook).

## Calidad y límites

El fondo incluye suelo, otras plantas, restos vegetales y variaciones de luz. Estas características pueden contribuir a la predicción. El conjunto permite un experimento de clasificación; no demuestra por sí solo que el modelo reconozca la causa biológica de los síntomas.

Tras eliminar duplicados exactos, se encontraron 25 pares muy similares según pHash (distancia máxima 4 bits), reunidos en grupos para evitar que se repartan entre entrenamiento y prueba. Se inspeccionó visualmente una lámina de esos pares; se observaron copias o tomas muy semejantes. El criterio es aproximado y puede no detectar todas las dependencias.

La descripción consultada no permite documentar con certeza el lugar y fecha de captura, variedad, identidad de cada planta o validación diagnóstica de las etiquetas. No atribuir esos datos a una región sin una fuente adicional. "Asintomática" no equivale a ausencia de infección demostrada.

Los archivos de `resultados/` (`inventario_original.csv`, `particion_imagenes.csv`, `pares_similares.csv` y `auditoria.json`) permiten rastrear los conteos y decisiones.
