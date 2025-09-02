# Clasificación de calidad de vino (Notebook)

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-%3E%3D1.3-0f4c81)](https://pandas.pydata.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-%3E%3D1.0-orange)](https://scikit-learn.org/)
[![xgboost](https://img.shields.io/badge/xgboost-%3E%3D1.6-red)](https://xgboost.readthedocs.io/)
[![imbalanced-learn](https://img.shields.io/badge/imbalanced--learn-SMOTE-lightgrey)](https://imbalanced-learn.org/)
[![matplotlib](https://img.shields.io/badge/matplotlib-%3E%3D3.4-CC2927)](https://matplotlib.org/)
[![seaborn](https://img.shields.io/badge/seaborn-%3E%3D0.11-purple)](https://seaborn.pydata.org/)
[![plotly](https://img.shields.io/badge/plotly-%3E%3D5.0-blueviolet)](https://plotly.com/)
[![Jupyter](https://img.shields.io/badge/Jupyter-notebook-orange)](https://jupyter.org/)

## Resumen

Este repositorio contiene un notebook que explora, procesa y modela el dataset de vino tinto (Wine Quality - red) para predecir la calidad del vino. Se realiza un EDA visual, se agrupan las etiquetas de `quality` en tres clases (`Baja`, `Media`, `Alta`), se corrige el desbalance con SMOTE y se comparan dos modelos: Random Forest y XGBoost. El objetivo es entregar un pipeline reproducible y recomendaciones prácticas para uso por enólogos o como proof-of-concept en proyectos ML.

---

## Estructura del repositorio

```
📁 repo/
  ├─ xgb_model.json                    # modelo XGBoost guardado
  ├─ notebook.ipynb                    # notebook principal
  ├─ requirements.txt                  # dependencias del proyecto
  └─ README.md                         # documento que estás leyendo
```

---

## Dataset

El dataset original no se incluye en este repositorio debido a su tamaño. Puedes descargarlo directamente desde el repositorio oficial de UCI Machine Learning:

🔗 [Wine Quality Dataset (UCI)](https://archive.ics.uci.edu/dataset/186/wine+quality)

Archivo a usar: **winequality-red.csv** (separador `;`).

Colócalo en la misma carpeta raíz del proyecto o ajusta la ruta en el notebook.

---

## Requisitos (entorno)

Se recomienda crear un entorno virtual (venv/conda) y usar Python 3.8+. Un `requirements.txt` básico ya está incluido en la raíz del proyecto:

```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
imblearn
joblib
```

Instalación rápida:

```bash
python -m venv .venv
source .venv/bin/activate   # o .venv\Scripts\activate en Windows
pip install -r requirements.txt
```

---

## Pipeline del Notebook (pasos principales)

1. **Carga de librerías y dataset**
2. **EDA**: scatter plots, series por índice, heatmap de correlación.
3. **Selección de features**
4. **Separación train/test**
5. **Reagrupación de etiquetas (Baja/Media/Alta)**
6. **Escalado con StandardScaler**
7. **Balanceo con SMOTE**
8. **Modelado**: RandomForest (baseline) y XGBoost (modelo final)
9. **Evaluación**: accuracy, classification\_report, confusion\_matrix
10. **Guardado de modelo**: `xgb_model.json`

---

## Resultados resumen

* **Random Forest (baseline)**

  * Accuracy: \~0.68
  * Weighted F1: \~0.70
  * Débil en clase `Baja`.

* **XGBoost (modelo final)**

  * Accuracy: \~0.765
  * Weighted F1: \~0.77
  * Fuerte en clase `Alta`, estable en `Media`, más o menos pobre en `Baja` por escasez de datos.

**Interpretación**: XGBoost es la mejor opción actual para predecir vinos de calidad `Alta` y `Media`, la `Baja` es algo peor.

---

## Próximos pasos recomendados

1. Probar nuevas features o transformaciones.
2. Implementar una API (FastAPI/Flask) para servir el modelo.

---

## Matriz de Confusión

<img width="649" height="547" alt="download" src="https://github.com/user-attachments/assets/074c9995-2150-44c1-abd4-d714825706da" />

### 🔎 Matriz de confusión (clases 0 = Baja, 1 = Media, 2 = Alta)

#### Clase 0 (Baja, fila 0):

- Predichos como 0 (correctos): 7
- Predichos como 1: 2
- Predichos como 2: 4

👉 Muy poquitos ejemplos de clase “Baja” y el modelo los confunde bastante.

#### Clase 1 (Media, fila 1):

- Predichos como 1 (correctos): 100
- Predichos como 0: 5
- Predichos como 2: 31

👉 El modelo reconoce bien la clase Media, pero confunde bastantes como “Alta”.

#### Clase 2 (Alta, fila 2):

- Predichos como 2 (correctos): 138
- Predichos como 1: 31
- Predichos como 0: 2

👉 El modelo también reconoce bastante bien la clase Alta, aunque a veces los manda a Media.

---


## Archivos generados

* `modelos/xgb_model.json` — modelo XGBoost entrenado.

---

## Licencia

MIT License — úsalo como base para tus experimentos y añade atribuciones si compartes resultados.
