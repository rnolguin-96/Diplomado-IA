# Clase 2 — Cómo la IA representa el conocimiento

## Resumen

La clase exploró cómo los sistemas de inteligencia artificial convierten información del mundo en representaciones numéricas que los modelos pueden procesar y utilizar para aprender. Se recorrió el camino desde la asociación de conceptos hasta las representaciones usadas en Deep Learning, y se cerró con una introducción práctica a tensores y PyTorch.

## Temas principales

### 1. Asociar y representar conocimiento
- El cerebro aprende y recuerda mediante asociaciones; la memoria asociativa permite relacionar conceptos y reconocer patrones.
- Se introdujo la idea de representar conceptos mediante vectores y de que conceptos similares tengan representaciones cercanas.
- Se usó **K vecinos más cercanos (KNN)** para ilustrar cómo la cercanía entre representaciones puede servir para predecir o clasificar.
- Se discutieron límites de KNN: almacenar y comparar muchos ejemplos puede ser costoso, la búsqueda puede ser lenta y los datos de distintas características pueden mezclarse en el espacio.

### 2. De los datos a los números
- Los datos pueden ser números, categorías, texto, imágenes, audio o video; para trabajar con ellos, los modelos necesitan representaciones numéricas.
- Una fila de una tabla puede representar un dato y sus características.
- Las imágenes se representan como tensores de píxeles (por ejemplo, canales RGB); los videos agregan una dimensión temporal y el audio puede representarse mediante espectrogramas.
- En texto se revisaron tokens, IDs y **embeddings**: los tokens se convierten en identificadores y luego en vectores que pueden aprenderse.
- Se abordaron estrategias para manejar secuencias de longitud variable, como el *padding*, y dos ideas para procesar secuencias: recurrencia (RNN) y atención, que pondera información de distintos elementos.
- Se presentó la codificación *one-hot* y sus limitaciones: puede producir vectores muy grandes y no expresa por sí sola relaciones semánticas. Los embeddings ofrecen representaciones densas y aprendibles.
- Se explicó la intuición de las representaciones distribuidas: cada dimensión aporta una característica y un concepto queda representado por una combinación de valores.

### 3. Representaciones, aprendizaje y Deep Learning
- En lugar de diseñar manualmente todas las características, los modelos de Deep Learning pueden aprender representaciones directamente a partir de los datos.
- Se introdujeron los espacios semánticos y de hipótesis: las representaciones permiten organizar conceptos por similitud, mientras que el modelo define qué funciones o representaciones puede aprender.
- Se comentaron las exigencias computacionales del entrenamiento y el papel de las GPU para realizar muchas operaciones con tensores en paralelo.

### 4. Trabajo práctico con PyTorch
- Se presentó Google Colab como entorno de notebooks en el navegador y se mencionaron frameworks de Deep Learning, como TensorFlow, Keras, PyTorch y JAX. El diplomado utilizará **PyTorch**.
- Se trabajó conceptualmente con tensores, creación de tensores y sus dimensiones (`shape`).
- Se revisaron ejemplos de código para representar texto mediante IDs y embeddings, definir un modelo con `nn.Module` y comprender el ciclo de entrenamiento: predicción, cálculo de la pérdida, actualización de parámetros y repetición durante varias épocas.

## Conceptos clave

**Memoria asociativa · KNN · similitud y distancia · representación numérica · tensor · píxeles RGB · espectrograma · tokens · IDs · one-hot · embeddings · representaciones distribuidas · RNN · atención · espacio semántico · espacio de hipótesis · GPU · Google Colab · PyTorch · `nn.Module` · función de pérdida · ciclo de entrenamiento.**

## Idea central

Para que una IA pueda aprender, la información debe convertirse en una representación que el modelo pueda procesar. En Deep Learning, estas representaciones —como los embeddings— pueden aprenderse a partir de los datos, y los tensores constituyen una estructura fundamental para trabajar con ellas.
