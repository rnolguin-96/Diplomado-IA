# 🧠 Diplomado en Inteligencia Artificial (CENIA) 🚀

¡Bienvenido a mi centro de operaciones y desarrollo para el **Diplomado de Inteligencia Artificial** dictado por el **CENIA** (Centro Nacional de Inteligencia Artificial)! 

Este repositorio ha sido diseñado bajo los estándares de la industria (*Cookiecutter Data Science*) para mantener un flujo de trabajo limpio, modular y altamente escalable. Aquí se alojarán todos los laboratorios, apuntes teóricos, arquitecturas de modelos de Deep Learning y experimentos matemáticos desarrollados a lo largo del programa académica.

---

## 🎯 Objetivo del Repositorio

El propósito de este espacio es doble:
1. **Académico:** Servir como bitácora y respaldo estructurado de los módulos cursados, garantizando la reproducibilidad de cada algoritmo.
2. **Profesional:** Consolidar un **portafolio técnico verificable** que demuestre mis habilidades en la manipulación de datos, entrenamiento de redes neuronales y despliegue de modelos de IA.

---

## 📂 Arquitectura del Proyecto y Estructura de Carpetas

La estructura de este directorio está optimizada para separar la experimentación en cuadernos de la construcción de código limpio y reutilizable:

```text
Diplomado-IA/
├── 📄 .gitignore               # Excluye del control de versiones archivos pesados y del sistema
├── 📄 README.md                # Presentación general del proyecto (este archivo)
├── 📄 requirements.txt         # Registro de las librerías exactas utilizadas en el entorno
│
├── 📂 datasets/                # Almacenamiento local de datos (Sincronizado en Google Drive, fuera de Git)
│   ├── 📥 raw/                 # Datasets originales e inmutables (datos puros)
│   └── ⚙️ processed/           # Matrices de datos limpias y transformadas listas para el modelo
│
├── 📂 modelos_guardados/       # Pesos y archivos binarios de redes neuronales (.pth, .h5, .pkl)
│
├── 📂 src/                     # CÓDIGO FUENTE REUTILIZABLE (Módulos independientes de Python)
│   ├── 📜 __init__.py          # Inicializador para permitir importaciones locales
│   ├── 📜 datos.py             # Funciones automatizadas para limpieza y preprocesamiento de datos
│   └── 📜 modelos.py           # Clases y arquitecturas custom de redes neuronales (PyTorch)
│
└── 📂 cursos/                  # Espacio dedicado a la malla académica del diplomado
    ├── 📂 curso1/              
    │   ├── 📂 clases/          # Documentación, PDFs y apuntes teóricos del profesor
    │   └── 📂 laboratorios/    # Cuadernos interactivos (.ipynb) para experimentación rápida
    ├── 📂 curso2/
    │   └── ...
    └── 📂 curso3/
        └── ...
```

---

## ⚙️ Configuración del Entorno de Desarrollo (Setup)

El entorno local está montado sobre una arquitectura robusta para garantizar la máxima velocidad de cómputo en **macOS (Apple Silicon)**:

*   **Gestor de Entornos:** `Miniconda` (Aislamiento de dependencias por compartimentos estancos).
*   **Entorno Virtual:** `cenia_ia` corriendo sobre **Python 3.12**.
*   **Ecosistema Core:** `PyTorch` optimizado mediante **MPS (Metal Performance Shaders)** para exprimir al máximo la potencia de la GPU integrada de los procesadores M-Series de Apple de forma local.
*   **Respaldo automatizado:** Sincronización híbrida en tiempo real mediante la integración de la carpeta raíz con **Google Drive**, permitiendo saltar al cómputo de alto rendimiento en la nube (**Google Colab / Kaggle Kernels**) sin perder consistencia en la estructura de archivos.

---

## 🛠️ Cómo Replicar este Entorno

Para levantar este entorno en otra máquina, clona el repositorio y ejecuta los siguientes comandos en la terminal:

```bash
# 1. Crear el entorno virtual con Conda
conda create --name cenia_ia python=3.12 -y

# 2. Activar el entorno
conda activate cenia_ia

# 3. Instalar las dependencias oficiales
pip install -r requirements.txt
```

---
🛸 *Desarrollado con dedicación por **Roberto Andrés** — Estudiante de IA en el CENIA.*
