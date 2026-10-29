# Práctica: ¿Cómo lee una red neuronal?

Tres notebooks de Colab, en el mismo orden que la clase, para **mostrar en vivo** durante la práctica. El código ya está completo. En total son unos 90 minutos (estimación interna).

| Notebook | Acto | Tiempo | Qué muestra |
|---|---|---|---|
| [01_tokenizacion.ipynb](01_tokenizacion.ipynb) | 1 · Tokenización | ~30 min | Tokenización por palabras (`[UNK]`) y por caracteres, **BPE desde cero**, tiktoken / GPT-2 / BETO / XLM-R, el "impuesto" del español, **un tokenizador entrenado con el Quijote** y `nn.Embedding` = one-hot × matriz. |
| [02_rnn_lstm.ipynb](02_rnn_lstm.ipynb) | 2 · Memoria | ~30 min | Una **RNN como `for` loop** comparada con `nn.RNN`, la **medición del gradiente que se desvanece** (RNN, GRU, LSTM y LSTM con la puerta de olvido abierta) y una **LSTM que escribe como el Quijote**, con temperatura. |
| [03_seq2seq_atencion.ipynb](03_seq2seq_atencion.ipynb) | 3 · Seq2Seq | ~30 min | Un encoder–decoder que **invierte secuencias**, la **medición del cuello de botella**, la **atención de Bahdanau** con su mapa de calor y un **traductor español → inglés**. |

## Cómo abrirlos

- En [colab.research.google.com](https://colab.research.google.com), ve a **Archivo → Subir notebook**. También pueden copiarse a Google Drive o a un repositorio de GitHub y compartir el enlace de Colab.
- Para los notebooks 2 y 3, activa **Entorno de ejecución → Cambiar tipo de entorno de ejecución → T4 GPU**. El notebook 1 no la necesita.
- No hay que instalar nada: Colab ya trae `torch`, `transformers`, `tokenizers` y `tiktoken`.
- Usan internet para descargar el Quijote (Project Gutenberg), los pares es–en (zip del tutorial de TensorFlow, con un respaldo en Hugging Face) y tres tokenizadores de Hugging Face.

## Estructura de cada notebook

- **Código completo:** se corre celda por celda (o con "Ejecutar todo") y funciona de punta a punta.
- **💡 Explicaciones:** notas cortas en el texto, para comentar mientras corren las celdas.
- **Celdas para probar en vivo** con frases que propongan en el chat: el "impuesto" del español (notebook 1), la temperatura (notebook 2) y traducir frases propias (notebook 3).
- **⭐ Extra:** suman ~10 min y se saltan si el tiempo está justo. Son el espectro del tamaño de vocabulario (notebook 1) y RNN simple vs LSTM (notebook 2).

## Tiempos de ejecución medidos

Ejecutando todo de punta a punta en un Mac M4 con Metal:

| Notebook | Tiempo |
|---|---|
| 1 | ~15 s |
| 2 | ~1 min 10 s |
| 3 | ~4 min, de los cuales el traductor son ~3 min (5 épocas) |

## Ideas tomadas de otros cursos

- **BPE desde cero** y re-entrenar el tokenizador de GPT-2 con `train_new_from_iterator`: curso de 🤗 Hugging Face, cap. 6.2 y 6.5.
- **Embedding = one-hot × matriz**: Raschka, *LLMs from Scratch*, cap. 2.
- **RNN a mano comparada con `nn.RNN`**: d2l.ai.
- **Modelo de lenguaje de caracteres** y evolución de las muestras durante el entrenamiento: Karpathy, *The Unreasonable Effectiveness of RNNs*.
- **Encoder–decoder con atención de Bahdanau** y mapa de atención: tutorial de PyTorch *Translation with a Sequence to Sequence Network and Attention*.
- **Tarea de juguete** antes de los datos reales: d2l y Coursera *Deep Learning Specialization*.
- **Medición del gradiente por paso** y la puerta de olvido abierta: experimento propio, que conecta con las diapositivas de la clase.
