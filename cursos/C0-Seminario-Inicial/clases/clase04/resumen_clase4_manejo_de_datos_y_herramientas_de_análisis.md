# Clase 4: Manejo de Datos y Herramientas de Análisis
**Diplomado en IA Generativa · CENIA (Centro Nacional de Inteligencia Artificial)**  
*Docente: Francesca Lucchini*  
*Fecha: 19 de octubre de 2026*  

---

## 📌 Resumen General de la Clase
La clase abordó el **flujo de desarrollo de Machine Learning (ML)**, enfocándose principalmente en la **Fase 2 (Recolección de datos)** y **Fase 3 (Preparación de datos)**. El objetivo fue comprender los diferentes tipos de datos, los desafíos prácticos de su limpieza y balance, el etiquetado y la aumentación de datos. 

La sesión se dividió en dos partes:
1. **Parte Expositiva:** Conceptos teóricos fundamentales sobre datos, recolección, filtrado, balanceo y aumentación.
2. **Parte Práctica:** Implementación desde cero en **Google Colab usando PyTorch** para resolver un problema real de clasificación con desbalance de clases.

---

## 📖 Contenido Teórico

### 1. Los Datos en Machine Learning
* **Definición:** Cualquier información que puede ser procesada por un algoritmo para aprender patrones y hacer predicciones.
* **Glosario Clave:**
  * **Dataset:** Conjunto de datos organizado para una tarea (se divide en *train*, *validation* y *test*).
  * **Corpus:** Colección grande de datos, muchas veces sin *label* (enfocado principalmente en lenguaje).
  * **Label / Etiqueta / Ground Truth:** La respuesta correcta asociada a un dato.
* **Filosofía "Garbage-in-garbage-out":** Si no tenemos buenos datos, no tendremos un buen modelo. Los datos deben ser diversos, representativos y de calidad.

### 2. Tipos de Datos
* **Estructurados:** Datos organizados en formato fijo tabular (filas = entradas, columnas = características o *features*). Ej: CSV, Excel, registros financieros.
* **No Estructurados:** No tienen formato predefinido y requieren procesamiento específico. Ej: Texto (NLP), Audio (Voz a texto), Imágenes (matrices de píxeles), Video, Grafos.
* **Semiestructurados:** Híbridos con formato tipo árbol (raíz, nodos y elementos anidados). Ej: Archivos JSON.

### 3. Fuentes de Recolección (Data Collection)
Cada fuente presenta *trade-offs* de costo, calidad, licencia y privacidad:
* **Public Datasets:** Repositorios abiertos (HuggingFace, Kaggle).
* **Scraping:** Extracción desde sitios web (librerías: `requests`, `BeautifulSoup`, `Scrapy`, `Playwright`, `crawl4ai`). *Importante: siempre revisar robots.txt y términos de uso.*
* **APIs:** Servicios que entregan datos ya estructurados (con límites de cuotas).
* **Datos Sintéticos:** Generados por simulación o mediante LLMs (ej: metodología de datos de *Phi-1* de Microsoft usando GPT-3.5).
* **Datos Propios:** Registros internos empresariales.
* *Nota Legal:* Cumplimiento de normativas vigentes (como la Ley 21.719 de Protección de Datos Personales en Chile: anonimización y consentimiento).

### 4. Limpieza, Filtrado y Feature Engineering
* **Data Leakage:** Error crítico que ocurre cuando los datos de entrenamiento contienen información que no estará disponible al momento de la inferencia.
* **Desbalance de Clases:** Uno de los problemas más comunes. Genera métricas engañosas (ej: alta *accuracy* sólo prediciendo la clase mayoritaria) y dificultades para generalizar.
* **Feature Engineering básico:**
  * **Escalamiento:** Normalizar valores (ej. de 0 a 1) para acelerar la convergencia del gradiente.
  * **Outliers:** Identificación y eliminación de valores extremos.
  * **One-Hot Encoding:** Convertir datos categóricos en vectores binarios numéricos.
  * **Binning:** Transformar valores continuos en rangos discretos.

### 5. Data Labeling (Anotación)
Es la única clase del diplomado enfocada en el etiquetado. Los modelos supervisados requieren datos anotados a mano, lo que exige muchas horas-hombre.  
* **Soluciones tecnológicas:**
  * **Label Studio:** Plataforma amigable para múltiples anotadores conectada a fuentes como AWS S3.
  * **CVAT (Computer Vision Annotation Tool):** Especializada en datos visuales, permite anotación automática mediante modelos preentrenados y despliegue en Docker.

### 6. Splits de Datos y Aumentación (Data Augmentation)
* **División Estándar:**
  * **Train:** Datos con los que el modelo aprende.
  * **Validation (Dev set):** Monitorear el entrenamiento y elegir hiperparámetros.
  * **Test:** Se usa una sola vez al final para reportar métricas definitivas.
* **Aumentación de Datos:** Aplicar transformaciones para generar nuevos datos similares pero no idénticos. **Regla de oro: Se aplica SOLO sobre el conjunto de Train, después del split.**
  * *Imágenes:* Rotación, recorte, brillo/contraste, adición de ruido.
  * *Texto:* Reemplazo por sinónimos, embeddings contextuales (BERT), *Back-translation* (espanol ➔ inglés ➔ español), prompts con LLMs.
  * *Tabulares:* **SMOTE** (*Synthetic Minority Over-sampling Technique*), que genera puntos sintéticos interpolando de manera vectorial entre los vecinos más cercanos de la clase minoritaria.

---

## 💻 Laboratorio Práctico: Inspección de Planchas de Acero

El caso práctico consistió en clasificar automáticamente **7 tipos de falla** en planchas de acero utilizando el dataset **Steel Plates Faults** (1.941 ejemplos, 27 características geométricas y de luminosidad).

### Objetivos y flujo del código:
1. **Carga y Análisis Exploratorio (EDA):** Descarga del dataset desde UCI Repository, transformación de columnas *one-hot* a índices de clases (0 a 6) mediante PyTorch. Verificación de nulos y duplicados.
2. **Split Estratificado a Mano:** Separación proporcional por clase en Train (70%), Validation (15%) y Test (15%) para evitar que las clases minoritarias queden ausentes en los subconjuntos.
3. **Normalización correcta:** Cálculo de la media ($\mu$) y desviación estándar ($\sigma$) **únicamente** sobre el conjunto de Train, aplicando luego dicha transformación a Validation y Test para prevenir el *Data Leakage*.
4. **Implementación de SMOTE:** Balanceo de las clases de entrenamiento generando ejemplos sintéticos vectoriales basados en vecinos cercanos ($k$-NN).
5. **Estructuras de PyTorch desde cero:** Creación personalizada de clases heredadas de `Dataset` y configuración de `DataLoader` para manejar mini-batches.
6. **Entrenamiento y Early Stopping:** Definición de una Red Neuronal Perceptrón Multicapa (MLP) con dos capas ocultas utilizando activación ReLU. Entrenamiento optimizado con Adam y CrossEntropyLoss, implementando un sistema de parada temprana (*Early Stopping*) para detener el entrenamiento cuando la *Validation Loss* deja de disminuir.
7. **Evaluación:** Cálculo manual de la matriz de confusión, *Precision*, *Recall* y *F1-Score* para mitigar el sesgo del desbalance del dataset original.

---

## 🛠️ Herramientas y Librerías Utilizadas
* **PyTorch (`torch`, `nn`, `DataLoader`, `Dataset`):** Motor principal para la manipulación de tensores, normalización, splits, arquitectura del modelo MLP y optimización.
* **Pandas & Numpy:** Carga de datos tabulares y manipulación de estructuras iniciales.
* **Matplotlib:** Visualizaciones de distribución de clases y curvas de pérdida (*loss*).
* **Ucimlrepo:** Importación automatizada del repositorio de UC Irvine.
