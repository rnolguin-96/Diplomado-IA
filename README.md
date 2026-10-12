# 🧠 Diplomado en Inteligencia Artificial (CENIA) 🚀

¡Bienvenido a mi centro de operaciones y desarrollo para el **Diplomado de Inteligencia Artificial** dictado por el **CENIA** (Centro Nacional de Inteligencia Artificial)!

Este repositorio ha sido diseñado bajo los estándares de la industria (*Cookiecutter Data Science*) para mantener un flujo de trabajo limpio, modular y altamente escalable. Aquí se alojarán todos los laboratorios, apuntes teóricos, arquitecturas de modelos de Deep Learning y experimentos matemáticos desarrollados a lo largo del programa académico.

---

## 🎯 Objetivo del Repositorio

El propósito de este espacio es doble:

1. **Académico:** Servir como bitácora y respaldo estructurado de los módulos cursados, garantizando la reproducibilidad de cada algoritmo.
2. **Profesional:** Consolidar un **portafolio técnico verificable** que demuestre mis habilidades en la manipulación de datos, entrenamiento de redes neuronales y despliegue de modelos de IA.

---

## 📂 Arquitectura del Proyecto y Estructura de Carpetas

La estructura de este directorio está optimizada para separar la experimentación en cuadernos de la construcción de código limpio y reutilizable:

```
Diplomado-IA/
├── 📄 .gitignore               # Excluye del control de versiones archivos pesados y del sistema
├── 📄 README.md                # Presentación general del proyecto (este archivo)
├── 📄 environment.yml          # Receta de Conda: nombre del entorno (cenia_ia), versión de Python (3.12) y enlace a requirements.txt
├── 📄 requirements.in          # Dependencias DIRECTAS del proyecto (las que yo elijo), sin versión fija. Se edita a mano
├── 📄 requirements.txt         # "Lock" generado con pip-compile: todas las librerías (directas y transitivas) con versión exacta (==). NO se edita a mano
│
├── 📂 datasets/                # Almacenamiento local de datos (Sincronizado en Google Drive, fuera de Git)
│   ├── 📥 raw/                 # Datasets originales e inmutables (datos puros)
│   └── ⚙️ processed/           # Matrices de datos limpias y transformadas listas para el modelo
│
├── 📂 modelos_guardados/       # Pesos y archivos binarios de redes neuronales (.pth, .pt, .h5, .pkl)
│
├── 📂 src/                     # CÓDIGO FUENTE REUTILIZABLE (Módulos independientes de Python)
│   ├── 📜 __init__.py          # Inicializador para permitir importaciones locales
│   ├── 📜 datos.py             # Funciones automatizadas para limpieza y preprocesamiento de datos
│   └── 📜 modelos.py           # Clases y arquitecturas custom de redes neuronales (PyTorch)
│
└── 📂 cursos/                  # Espacio dedicado a la malla académica del diplomado
    ├── 📂 C0-Seminario-Inicial/
    │   ├── 📂 clases/          # Documentación, PDFs y apuntes teóricos del profesor
    │   ├── 📂 laboratorios/    # Cuadernos interactivos (.ipynb) para experimentación rápida
    │   └── 📂 Material Complementario/   # Material que complementa la clase y no es entregado por el curso
    │       └── 📓 pytorch_desde_cero.ipynb   # Guía didáctica de PyTorch desde cero (tensores, autograd, nn, CNN)
    ├── 📂 C1-Conceptos-Fundamentales/
    │   └── ...
    └── 📂 C2-Grandes-Modelos-de-Lenguaje/
        └── ...
```

---

## ⚙️ Configuración del Entorno de Desarrollo (Setup)

El entorno local está montado sobre una arquitectura robusta para garantizar la máxima velocidad de cómputo en **macOS (Apple Silicon)**:

- **Gestor de Entornos:** `Miniconda` (aislamiento de dependencias por compartimentos estancos).
- **Entorno Virtual:** `cenia_ia` corriendo sobre **Python 3.12**.
- **Ecosistema Core:** `PyTorch` optimizado mediante **MPS (Metal Performance Shaders)** para exprimir al máximo la potencia de la GPU integrada de los procesadores M-Series de Apple de forma local.
- **Dependencias con versión fija:** todas las librerías quedan fijadas con `==` en `requirements.txt`, de modo que el entorno sea idéntico en cualquier máquina y en cualquier momento (ver la sección [Gestión de dependencias](#-gestión-de-dependencias)).
- **Respaldo automatizado:** sincronización híbrida en tiempo real mediante la integración de la carpeta raíz con **Google Drive**, permitiendo saltar al cómputo de alto rendimiento en la nube (**Google Colab / Kaggle Kernels**) sin perder consistencia en la estructura de archivos.

---

## 🛠️ Cómo Replicar este Entorno

Para levantar este entorno en otra máquina, clona el repositorio y ejecuta los siguientes comandos **desde la raíz del proyecto**:

```bash
# 1. Crear el entorno con Conda (instala Python 3.12 y todas las librerías fijadas)
conda env create -f environment.yml

# 2. Activar el entorno
conda activate cenia_ia

# 3. (Opcional) Registrar el entorno como kernel de Jupyter
python -m ipykernel install --user --name cenia_ia --display-name "Python (cenia_ia)"
```

> 💡 `environment.yml` ya incluye la instalación de `requirements.txt`, por lo que no hace falta ejecutar `pip install` aparte.

**Alternativa manual** (si ya tienes un entorno de Python 3.12 creado):

```bash
conda activate cenia_ia
pip install -r requirements.txt
```

### ✅ Verificar la instalación

```bash
python --version
python -c "import torch; print(torch.__version__, '| MPS disponible:', torch.backends.mps.is_available())"
```

En un Mac con Apple Silicon debería imprimir `MPS disponible: True`.

---

## 📦 Gestión de dependencias

Se usa un patrón de **dos archivos** para tener control sin perder reproducibilidad:

| Archivo | Contenido | ¿Quién lo escribe? |
|---|---|---|
| `requirements.in` | Solo las librerías que yo elijo instalar (`torch`, `numpy`, ...) | Yo, a mano |
| `requirements.txt` | Esas librerías **y todas sus dependencias**, cada una con versión exacta | Se genera con `pip-compile` |

### Agregar o actualizar una librería

```bash
# 0. Una sola vez: instalar la herramienta
pip install pip-tools

# 1. Agregar el paquete a requirements.in (o cambiar su restricción)

# 2. Regenerar el archivo con las versiones exactas
pip-compile requirements.in --output-file requirements.txt

# 3. Instalar lo que quedó fijado
pip install -r requirements.txt

# 4. Probar los notebooks y, si todo funciona, hacer commit de ambos archivos
git add requirements.in requirements.txt
git commit -m "Actualizar dependencias"
```

Para actualizar **solo un paquete** (por ejemplo `torch`) sin mover el resto:

```bash
pip-compile --upgrade-package torch requirements.in --output-file requirements.txt
```

### ⚠️ Consideraciones

- `requirements.txt` fue generado en **macOS (Apple Silicon)**: es específico de esa plataforma. En **Google Colab / Kaggle** (Linux con CUDA) `torch` ya viene preinstalado, por lo que ahí solo conviene instalar lo que falte.
- `torch` y `torchvision` deben ser versiones compatibles entre sí; el archivo de lock se encarga de mantenerlas emparejadas.
- Siempre se versionan **ambos** archivos (`requirements.in` y `requirements.txt`).

---

## 📓 Material destacado

| Notebook | Descripción |
|---|---|
| [`pytorch_desde_cero.ipynb`](cursos/C0-Seminario-Inicial/Material%20Complementario/pytorch_desde_cero.ipynb) | Guía didáctica de PyTorch desde cero: qué es y por qué usarlo, CPU vs GPU (CUDA/MPS), tensores, comparación con NumPy, autograd, `torch.nn`, `Dataset`/`DataLoader`, entrenamiento de MLP y CNN, guardado de modelos y buenas prácticas. Incluye ejercicios con solución. |

---

🛸 *Desarrollado con dedicación por **Roberto Andrés** — Estudiante de IA en el CENIA.*
