# Registro de Incidencias: Manejo de Excepciones con NumPy

## 1. Descripción del Problema
Durante la ejecución del **Paso 9 (Colab y publicación)** correspondiente al LAB07 de Visión Computacional, el proceso de instalación de dependencias mediante el archivo `requirements-colab.txt` arrojó un error crítico que detuvo la ejecución:

> `ERROR: Could not find a version that satisfies the requirement numpy==2.9`
> `ERROR: No matching distribution found for numpy==2.9`

## 2. Causa Raíz
El entorno de ejecución en la nube (Google Colab corriendo bajo Python 3.13) presenta incompatibilidades de dependencias cruzadas (con librerías como `matplotlib`, `scikit-learn` y `scipy`) al intentar instalar versiones inestables o no soportadas de NumPy (como la 2.9 o 2.5.3). El entorno carece de las distribuciones precompiladas (*wheels*) necesarias para esas versiones específicas en esa arquitectura.

## 3. Solución Aplicada (Manejo de Excepción)
Para garantizar la reproducibilidad, estabilidad y el correcto funcionamiento del modelo convolucional (CNN), es obligatorio aplicar una restricción de control de versiones. Se comprobó que el entorno funciona de manera estable utilizando la rama **2.2** de NumPy, por lo que la versión a instalar debe ser **estrictamente menor a la 2.3**.

### Acción Correctiva en el Código
Se debe modificar el archivo `requirements-colab.txt`. Localice la línea donde se exige la instalación de NumPy y reemplácela con la siguiente restricción formal:

```text
numpy>=2.2.0,<2.3.0