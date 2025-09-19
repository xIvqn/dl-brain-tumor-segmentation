# Segmentación de Tumores Cerebrales con CNNs

Este repositorio contiene el Jupyter Notebook del trabajo descrito en el artículo "Segmentación de Tumores Cerebrales con CNNs". Este proyecto se ha realizado como parte de la asignatura de **Aprendizaje Profundo** del Máster Universitario de Investigación en Inteligencia Artificial de la Universidad Internacional Menéndez Pelayo.

---

## Resumen del Proyecto

El proyecto se centra en la aplicación de técnicas de **aprendizaje profundo** para la segmentación precisa de tumores cerebrales a partir de resonancias magnéticas (MRI). El objetivo principal es superar un valor de referencia de 0.60 en el coeficiente de similitud Dice, evaluando la capacidad de los modelos para generar segmentaciones precisas y localizar tumores en las imágenes de resonancia magnética. Para ello, se diseñan y comparan dos arquitecturas de redes neuronales convolucionales (CNN).

El conjunto de datos utilizado incluye secuencias de MRI T1, T2, Tice y FLAIR, junto con sus correspondientes máscaras de segmentación binaria.

---

## Modelos y Metodología

Se han diseñado dos modelos de CNN para abordar la tarea de segmentación:

### CNN1 (CNN simple)

Se desarrolló una red más simple para evaluar el rendimiento de una arquitectura de baja complejidad en la segmentación de máscaras binarias. Para evitar el sobreajuste, se aplicó dropout después de las capas de pooling. El entrenamiento se llevó a cabo utilizando el algoritmo Adam y el método de *early stopping* para evitar el sobreentrenamiento. Este modelo logró un desempeño aceptable, superando el *baseline* en casi todas sus configuraciones.

### CNN2 (CNN profunda)

Esta arquitectura más sofisticada está inspirada en el modelo **U-Net**, que utiliza un enfoque de codificador-decodificador con *skip connections*. Esto permite combinar información de bajo y alto nivel para recuperar la resolución espacial y delinear con mayor precisión los contornos tumorales. El entrenamiento de este modelo también utilizó *early stopping* y el algoritmo Adam, e incluyó un aprendizaje por fases con tasas de aprendizaje variables. Este modelo demostró ser más robusto y preciso, alcanzando valores del coeficiente Dice superiores a 0.9 en todas las configuraciones probadas.

---

## Entrenamiento y Optimización

Para prevenir el sobreajuste y mejorar la estabilidad del entrenamiento, se aplicaron las siguientes técnicas:

* **Data Augmentation:** Se amplió el conjunto de datos de entrenamiento rotando y volteando las imágenes originales para hacerlo más diverso.
* **Normalización:** Los valores de las imágenes se normalizaron para mejorar la estabilidad de los entrenamientos.
* **Algoritmo de optimización:** Se utilizó el algoritmo **Adam** por su adaptabilidad y buen rendimiento en tareas de visión por computadora.
* **Early Stopping:** Para evitar el sobreentrenamiento, el proceso se detuvo cuando la métrica de validación dejaba de mejorar.
* **Función de pérdida:** Se utilizó la inversa de la métrica Dice para priorizar su maximización durante el entrenamiento.

---

## Contenido del Repositorio

* `article.pdf`: El artículo original que detalla el proyecto.
* `DL_BrainTumorSeg.ipynb`: El Jupyter Notebook que contiene el código del proyecto.
* `presentation.pdf`: Una presentación que resume el trabajo y los hallazgos del proyecto.
* `README.md`: Este archivo.

---

## Resultados y Conclusiones

Ambos modelos lograron superar el *baseline* de 0.60 en el coeficiente Dice. El modelo **CNN1**, a pesar de su simplicidad, tuvo un desempeño aceptable , mientras que el **CNN2** demostró ser considerablemente más preciso, alcanzando valores de Dice superiores a 0.9. Las segmentaciones del CNN2 fueron superiores, ya que lograron delinear los contornos de los tumores con mayor precisión.

Se observó que la mejor configuración para ambos modelos fue con una tasa de *dropout* de 0.0, lo que sugiere que un uso excesivo de esta técnica podría no haber sido beneficioso. Además, la estrategia de entrenamiento con tasas de aprendizaje variables en el CNN2 influyó significativamente en la estabilidad del aprendizaje en las primeras etapas.

---

## Posibles Mejoras

Se han identificado varias líneas de mejora para futuros trabajos:

* **Explorar una configuración adecuada para las tasas de aprendizaje variables** que permita un entrenamiento rápido en las primeras etapas sin causar inestabilidad.
* **Analizar el efecto del *dropout* utilizando menos capas** para determinar su utilidad real en los modelos.

---

El trabajo se realizó en el entorno de Google Colab.