# Taller Grupal — Ciencia de Datos
## Estudio Comparativo de Modelos de Regresión sobre NASA93 (COCOMO)

**Maestría en Ingeniería en Software — Mención en Sistemas Inteligentes e Intensivos en Datos**
**Universidad Estatal de Milagro (UNEMI)**

**Integrante:** Escobar, Erick
**Docente:** Guillermo Baquerizo Palma, M.Sc.
**Asignatura:** Ciencia de Datos — Actividad A1
**Fecha de entrega:** 15 de mayo de 2026

---

## Contenido del Paquete

| Archivo | Descripción |
|---|---|
| `Taller_Grupo01.pdf` | Informe académico (9 páginas, 8 de contenido sin portada) |
| `Taller_Grupo01.tex` | Código fuente LaTeX del informe |
| `Taller_Grupo01_notebook.ipynb` | Notebook Jupyter reproducible con outputs ejecutados |
| `nasa93.arff` | Dataset original (PROMISE, DOI 10.5281/zenodo.268419) |
| `nasa93_clean.csv` | Dataset preprocesado (cost drivers mapeados a multiplicadores COCOMO) |
| `fig1_eda.png`–`fig5_comparacion.png` | Figuras del informe en alta resolución |

---

## Reproducir el Análisis desde Cero

### Requisitos

```
Python 3.10+
pip install numpy pandas matplotlib scikit-learn scipy statsmodels jupyter
```

### Ejecución

```bash
# 1. Asegurarse de que nasa93.arff está en el mismo directorio
# 2. Lanzar el notebook
jupyter notebook Taller_Grupo01_notebook.ipynb

# O ejecutar todo desde línea de comandos:
jupyter nbconvert --to notebook --execute Taller_Grupo01_notebook.ipynb
```

Todos los resultados son reproducibles con `random_state=42`.

### Compilar el LaTeX

```bash
pdflatex Taller_Grupo01.tex
pdflatex Taller_Grupo01.tex  # segunda pasada para referencias cruzadas
```

Requiere distribución TeX Live con paquetes: `babel`, `amsmath`, `graphicx`,
`tabularx`, `longtable`, `booktabs`, `xcolor`, `colortbl`, `listings`,
`hyperref`, `enumitem`, `fancyhdr`, `float`, `caption`.

---

## Resultados Principales

| Modelo | R² Train | R² Test | R² CV (log) | MAE Test (PM) | RMSE Test (PM) |
|---|---|---|---|---|---|
| OLS | 0.874 | 0.673 | 0.738 ± 0.159 | 107.45 | 202.72 |
| Polinómica | 0.867 | 0.701 | 0.731 ± 0.160 | 105.06 | 193.83 |
| **Ridge (α* = 4.71)** | **0.794** | **0.799** | **0.791 ± 0.107** | **94.69** | **159.06** |

**Conclusión:** Ridge con α = 4.71 es el modelo recomendado.
Justificación: mejor generalización (brecha train-test eliminada),
menor varianza en CV repetida (50 folds), y reducción del 21.5% en RMSE
respecto a OLS sobre datos de prueba.

---

## Fuente del Dataset

Menzies, T. (2017). *nasa93 [Data set]*. Zenodo.
https://doi.org/10.5281/zenodo.268419

Boehm, B. W. (1981). *Software engineering economics*. Prentice-Hall.
