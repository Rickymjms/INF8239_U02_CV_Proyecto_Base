# INF-8239 · Unidad 02 · Proyecto de visión Computacional

**Asignatura:** INF-8239 - Ciencia de Datos II  
**Unidad 02:** Procesamiento de Lenguaje Natural, redes y visión  
**Autor académico:** Edwin Ramón José Nolasco
**Replicado y realizado por:** Manuel De Jesus Mañana Santana
**Universidad:** Universidad Autónoma de Santo Domingo (UASD)  
**Gestor de entorno:** `uv` (Python 3.12)  
Proyecto base del LAB07 (Visión Computacional) para INF-8239 (UASD). Compara el rendimiento y costo computacional (Green AI) de una CNN frente a un baseline denso usando Fashion-MNIST. Incluye auditoría de errores, Model Card restrictivo y reproducibilidad total gestionada con uv y pytest.


## Inicio rápido

### Entorno Local (CPU)

Adecuado para todos los estudiantes.

```
uv python install 3.12
uv sync --extra cpu
uv run python scripts/check_runtime.py
uv run python scripts/train_cv.py --epochs 8

```

### Entorno Local (GPU)

La ruta GPU se utiliza solamente en WSL2/Linux con NVIDIA correctamente configurada:

```
uv sync --extra gpu

```

### Ejecución en la Nube (Google Colab) y Manejo de Excepciones

Para ejecutar el entrenamiento en la nube, es necesario aplicar una restricción formal a la versión de NumPy debido a incompatibilidades cruzadas detectadas en entornos con Python 3.13.
Asegúrese de que su archivo `requirements-colab.txt` establezca la versión estrictamente menor a la 2.3:

```
numpy>=2.2.0,<2.3.0

```

Posteriormente, ejecute la instalación en su celda:

```
%pip install -r requirements-colab.txt

```

## Evaluación y Métricas (Model Card)

### Modelo y Uso Previsto

Red Neuronal Convolucional (CNN) secuencial construida con TensorFlow/Keras 2.21.0. Diseñado de forma exclusiva como benchmark de laboratorio para la demostración y evaluación estructural de redes neuronales convolucionales. Clasifica prendas de vestir en 10 categorías estandarizadas utilizando imágenes preprocesadas en escala de grises de 28x28 píxeles.
Totalmente descartado para extrapolar su funcionamiento a la detección de imágenes médicas, validación biométrica para vigilancia o reconocimiento de caracteres (OCR).

### Resultados Predictivos

* **Desempeño Global (CNN):** F1-macro de 0.789 y Accuracy de 0.793 en la evaluación final.

* **Baseline Denso:** F1-macro de 0.863.

* **Clases con alto desempeño:** Pantalones (Clase 1, F1: 0.959), Bolsos (Clase 8, F1: 0.927) y Botines (Clase 9, F1: 0.915).

* **Clase con mayor debilidad:** Las camisas (Clase 6) mostraron el rendimiento más deficiente (F1: 0.428, Recall: 0.374), registrando un alto volumen de falsos negativos por confusión directa con abrigos (Clase 4) y pulóveres (Clase 2).

### Comparación de Costo Computacional (Green AI)

* **Parámetros entrenables:** La CNN estructuró 19,466 parámetros entrenables frente a los 50,890 del Baseline denso.

* **Tiempo de entrenamiento:** La CNN consumió 89.03 segundos para 8 épocas, siendo 10 veces más lenta que el Baseline (8.69 segundos).

* **Tiempo de inferencia:** La CNN procesó imágenes a 0.103 milisegundos por unidad, duplicando el tiempo de respuesta del Baseline (0.046 ms).

## Cierre Interpretativo

* **Resultado principal:** Se entrenó y evaluó una CNN para clasificar el corpus Fashion-MNIST, comparándola bajo la misma partición contra un modelo Baseline denso.

* **Evidencia predictiva:** Contrario a la expectativa teórica, la CNN tuvo un desempeño inferior al Baseline denso.

* **Costo comparado y Green AI:** El modelo Baseline demostró superar a la CNN en precisión, requiriendo una fracción de la potencia computacional para entrenar e inferir.

* **¿La mejora justifica el costo?:** No. Bajo el principio de Green AI, el despliegue de esta CNN queda descartado.

* **Limitación del benchmark:** La arquitectura está profundamente limitada por la matriz de baja resolución (28x28). La carencia de detalles finos provoca una superposición geométrica casi idéntica en los mapas de características de prendas superiores, induciendo al modelo a errores de ambigüedad.