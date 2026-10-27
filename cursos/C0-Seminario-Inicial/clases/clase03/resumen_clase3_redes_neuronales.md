# Clase 1: Redes Neuronales y Aprendizaje Supervisado

¡Bienvenido al repositorio de apuntes del Diplomado en IA! Esta carpeta contiene el resumen técnico, las bases matemáticas y la implementación práctica de la primera sesión introductoria impartida en **CENIA** por *Alain Raymond*.

---

## 🎯 Objetivos de la Sesión
* Entender el concepto y estructura de una **neurona artificial** y una **red neuronal**.
* Comprender el **forward pass** como una operación de multiplicación de matrices.
* Conocer los componentes fundamentales del **aprendizaje supervisado**.

---

## 🧠 1. ¿Qué es una Red Neuronal?
Una **red neuronal** es un modelo computacional compuesto por una colección de unidades o nodos interconectados llamados **neuronas artificiales**. Aunque están inspiradas en las neuronas biológicas, en la práctica son módulos matemáticos parametrizados organizados en **capas**.

### De la Biología a las Matemáticas
La transición del modelo biológico al modelo matemático se define mediante la siguiente equivalencia:

| Componente Biológico | Componente Artificial | Función en la Fórmula |
| :--- | :--- | :--- |
| **Dendritas** (Reciben señales) | **Entradas** | Vector \(x = [x_1, x_2, x_3]\) |
| **Sinapsis** (Fuerza de conexión) | **Pesos** | Parámetros \(w = [w_1, w_2, w_3]\) |
| **Soma** (Junta las señales) | **Suma ponderada** | \(z = \sum_{i} w_i x_i + b\) *(donde \(b\) es el sesgo/bias)* |
| **Disparo** (¿Se activa o no?) | **Función de activación** | \(g(z)\) |
| **Axón** (Envía la señal) | **Salida** | Valor calculado \(y\) |

> ⚠️ **Nota:** La neurona biológica es solo una inspiración. Una neurona artificial es **mucho más simple** que una real.

### 📉 Funciones de Activación
Deciden cuánto se activa la neurona a partir de la suma ponderada \(z\):
*   **Sigmoide:** \(\sigma(z) = \frac{1}{1 + e^{-z}}\) (Aplasta todo en un rango entre 0 y 1).
*   **ReLU:** \(\text{ReLU}(z) = \max(0, z)\) (Si es negativo lo vuelve 0; si es positivo, lo deja igual. Es la más usada hoy).

---

## ➡️ 2. El Forward Pass y Álgebra Matricial
El **Forward Pass** es el viaje que hacen los datos desde el vector de entrada \(x\) a través de todas las capas de la red hasta llegar a la salida para generar una predicción (\(\hat{y}\)).

### Representación Matricial (Capa Lineal)
Para procesar múltiples neuronas en paralelo, multiplicamos el vector de entrada por una **matriz de parámetros \(W\)** y le sumamos un **vector de sesgos \(b\)**:

\[\text{Lineal}(x) = W \cdot x + b\]

Para una capa con **3 entradas y 2 neuronas**, la operación se ve así:

\[\text{Lineal}(x) = \begin{bmatrix} w_{1,1} & w_{1,2} & w_{1,3} \\ w_{2,1} & w_{2,2} & w_{2,3} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} + \begin{bmatrix} b_1 \\ b_2 \end{bmatrix} = \begin{bmatrix} w_{1,1}x_1 + w_{1,2}x_2 + w_{1,3}x_3 + b_1 \\ w_{2,1}x_1 + w_{2,2}x_2 + w_{2,3}x_3 + b_2 \end{bmatrix}\]

---

## ⚙️ 3. Parámetros de una Red
Aprender en IA significa **determinar los valores óptimos de los parámetros** (pesos y sesgos) mediante entrenamiento. El volumen de parámetros escala de forma drástica según la arquitectura:
*   **Red de ejemplo de la clase:** 3 capas (3 \(\rightarrow\) 6 \(\rightarrow\) 4 \(\rightarrow\) 1) = **57 parámetros**.
*   **GPT-3 (Brown et al., 2020):** **175.000 millones de parámetros**.

---

## 💻 4. Implementation en PyTorch
A continuación se detalla cómo estructurar la red exacta vista en el diagrama de clase usando `nn.Sequential`. PyTorch se encarga de crear los parámetros (al azar al principio) por nosotros:

```python
import torch
import torch.nn as nn

# 1. Definición de la arquitectura secuencial
red = nn.Sequential(
    nn.Linear(3, 6),  # Lineal 1: 3 entradas -> 6 neuronas ocultas
    nn.Sigmoid(),  # Activación de la Capa 1
    nn.Linear(6, 4),  # Lineal 2: 6 entradas -> 4 neuronas ocultas
    nn.Sigmoid(),  # Activación de la Capa 2
    nn.Linear(4, 1),  # Lineal 3: 4 entradas -> 1 neurona de salida
)

# 2. Vector de entrada de prueba (dimensión 3)
x = torch.tensor([0.1, -0.3, 1.4])

# 3. Ejecución del Forward Pass completo
y_hat = red(x)

print(f"Predicción final (y_hat): {y_hat.item()}")
```

---
*Apuntes del Diplomado en Inteligencia Artificial - CENIA (2026).*