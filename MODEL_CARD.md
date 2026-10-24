# Model Card · Fashion-MNIST CNN

## Modelo y versión
Red Neuronal Convolucional (CNN) secuencial construida con TensorFlow/Keras 2.21.0.

## Uso previsto
Clasificación automatizada de prendas de vestir en 10 categorías estandarizadas. Diseñado de forma exclusiva como benchmark de laboratorio para la demostración y evaluación estructural de redes neuronales convolucionales.

## Usos fuera de alcance
Inadecuado para el análisis de fotografías en color, imágenes de alta resolución o sujetos insertos en fondos complejos y ruidosos. Totalmente descartado para extrapolar su funcionamiento a la detección de imágenes médicas, validación biométrica para vigilancia o reconocimiento de caracteres (OCR)[cite: 1, 6].

## Dataset y particiones
*   **Corpus:** Fashion-MNIST[cite: 1].
*   **Volumen:** 60,000 imágenes para entrenamiento y 10,000 imágenes de prueba bajo la misma partición[cite: 1].
*   **Formato de entrada:** Imágenes preprocesadas en escala de grises, perfectamente centradas y encuadradas en 28x28 píxeles[cite: 1].

## Preprocesamiento
Adaptación del tensor de entrada a la forma `(28, 28, 1)` exigida por las capas de convolución, conservando la carga estructural del canal de color único.

## Métricas globales y por clase
*   **Desempeño Global:** F1-macro de 0.789 y Accuracy de 0.793 en la evaluación final.
*   **Clases con alto desempeño:** Pantalones (Clase 1, F1: 0.959), Bolsos (Clase 8, F1: 0.927) y Botines (Clase 9, F1: 0.915).
*   **Clase con mayor debilidad:** Las camisas (Clase 6) mostraron el rendimiento más deficiente (F1: 0.428, Recall: 0.374), registrando un alto volumen de falsos negativos por confusión directa con abrigos (Clase 4) y pulóveres (Clase 2).

## Comparación de costo
*   **Hardware:** Entorno Windows con CPU Intel Core i7-10750H @ 2.60GHz, 8.00 GB de RAM. Ejecución nativa basada en CPU[cite: 1, 7].
*   **Parámetros:** La CNN estructuró 19,466 parámetros entrenables frente a los 50,890 del Baseline denso[cite: 7].
*   **Tiempo de entrenamiento:** La CNN consumió 89.03 segundos para 8 épocas, siendo 10 veces más lenta que el Baseline (8.69 segundos)[cite: 7].
*   **Tiempo de inferencia:** La CNN procesó imágenes a 0.103 milisegundos por unidad, duplicando el tiempo de respuesta del Baseline (0.046 ms)[cite: 7].

## Limitaciones y riesgos
La arquitectura está profundamente limitada por la matriz de baja resolución (28x28). La carencia de detalles finos (botones, texturas de cuello o tipos de cierre) provoca una superposición geométrica casi idéntica en los mapas de características de prendas superiores, induciendo al modelo a errores de ambigüedad. Asumir que este desempeño es suficiente para operar sistemas logísticos o comerciales reales supone un riesgo crítico de fallas.

## Supervisión y monitoreo
Bajo el principio de Green AI, el despliegue de esta CNN queda descartado. El modelo Baseline demostró superar a la CNN en precisión (F1 0.863 vs 0.789), requiriendo una fracción de la potencia computacional para entrenar e inferir[cite: 7]. Cualquier trabajo derivado debe aplicar supervisión manual prioritaria a las inferencias emitidas para las clases 0, 2, 4 y 6, o migrar la arquitectura empleando técnicas de transferencia de aprendizaje con redes preentrenadas.