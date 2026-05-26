# Detección de anomalías en telemetría de picosatélites

Estudio comparativo de técnicas de Deep Learning para la detección de anomalías puntuales en el subsistema de potencia de picosatélites, a partir de datos reales de telemetría.

Trabajo Fin de Máster — Máster Universitario en Inteligencia Artificial (UNIR). Proyecto en grupo de 3 personas.

## Objetivo

Construir un dataset de telemetría real de satélites y comparar el rendimiento de distintos modelos de detección de anomalías, evaluando cómo se comporta cada enfoque según el tipo de anomalía y el conjunto de datos.

## Pipeline técnico

**1. Obtención de datos (web scraping)**
Recolección automatizada de telemetría real desde la plataforma open-source TinyGS durante 2 semanas. Proceso en dos fases: extracción de URLs de paquetes y descarga del contenido JSON de cada uno. Selección de 3 satélites (Polytech_Universe-3, CSTP-1.1, CSTP-1.2) según la calidad y completitud de su telemetría.

**2. Análisis exploratorio y preparación**
Limpieza de duplicados y registros erróneos (~8.800 paquetes finales), análisis de correlación de Pearson para eliminar variables redundantes, reducción de 73 campos al subconjunto relevante del subsistema de potencia, one-hot encoding de variables categóricas y selección de características.

**3. Etiquetado de anomalías**
Generación de dos versiones del dataset con métodos de etiquetado distintos: clustering K-means (con método del codo para seleccionar K) y anomalías generadas sintéticamente. Cada versión se divide por satélite y por partición (train/validación/test).

**4. Modelado y comparativa**
Implementación y evaluación de 6 modelos, con optimización de hiperparámetros mediante optimización bayesiana:

- Isolation Forest (baseline de ML clásico)
- Autoencoder (AE)
- Variational Autoencoder (VAE)
- Denoising Autoencoder (DAE)
- Red LSTM
- LSTM-Autoencoder

**5. Evaluación**
Comparativa sistemática mediante matrices de confusión y métricas de clasificación (F1 como métrica principal) sobre los distintos datasets y tipos de anomalía.

## Conclusión principal

El rendimiento de los modelos de reconstrucción depende fuertemente de los datos de evaluación: los enfoques basados en aprender y replicar patrones normales requieren anomalías claramente diferenciadas para funcionar de forma óptima.

## Contenido del repositorio

Este repositorio recoge el código y los datos correspondientes a los modelos LSTM y LSTM-Autoencoder, desarrollados íntegramente por el autor, así como los notebooks de preparación de datos y EDA.

```
models/                        # Implementación de los modelos LSTM y LSTM-Autoencoder
  hyperparameter-tuning/       # Notebooks de exploración y optimización bayesiana de hiperparámetros
data/
  data_preparation/            # Notebooks de limpieza, EDA y preparación del dataset
  dataset1/                    # Dataset con anomalías etiquetadas mediante K-means, dividido por satélite
  dataset2/                    # Dataset con anomalías generadas sintéticamente, dividido por satélite
```

El trabajo completo incluye además la memoria académica con el marco teórico, el estado del arte, la implementación del resto de modelos y el análisis comparativo de resultados.

## Stack

Python · TensorFlow/Keras · scikit-learn · Pandas · NumPy · Matplotlib
