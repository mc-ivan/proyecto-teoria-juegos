# Competencia Estratégica en Streaming con Estimación de Pagos y Equilibrios de Nash en un Diseño 2×3×2

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/mc-ivan/proyecto-teoria-juegos/blob/main/notebook/Proyecto_Teoria_Juegos.ipynb)

**Resumen.**  
Este proyecto combina **teoría de juegos** y **econometría** para estudiar la competencia entre **Netflix (2 estrategias)**, **Disney (3)** y **Max (2)** en un juego estático **2×3×2**. A partir de un **panel trimestral 2020–2024**, se estiman por **OLS** los efectos de **originales (O)**, **precio (P)** y **bundle (B)** —propios y rivales— sobre **altas netas** y **ARPU**. Con dichas predicciones se **simulan pagos (beneficios)** por perfil estratégico, se identifican **mejores respuestas**, **equilibrios de Nash** y el **frente de Pareto**, y se generan gráficos y CSV reproducibles.

## Datos Generales:
**Maestria en Ingeniería Matematica V1**

**Módulo:** MODELADO MEDIANTE TEORÍA DE JUEGOS Y ECONOMÍA EXPERIMENTAL

# GRUPO 3
### Integrantes:
- Gimena Javier
- Giovanni Ortiz
- Ivan Mamani 

**Fecha de Presentación:** 7/09/2025

---



## 1. Estructura del Repositorio

```
proyecto-teoria-juegos/
├─ dataset/
│  └─ ott_panel_quarterly_synthetic_2020_2024.csv    # panel integrado (2020Q1–2024Q4)
├─ notebook/
│  └─ Proyecto_Teoria_Juegos.ipynb                   # notebook principal (Colab-friendly)
├─ sources/                                          # se crea al ejecutar el notebook
   ├─ 01_subscriptores_por_plataforma.png
   ├─ 02_altas_trimestrales_por_plataforma.png
   ├─ 03_ingresos_trimestrales_por_plataforma.png
   ├─ 04_arpu_mensual_por_plataforma.png
   ├─ 05_inversion_trimestral_por_plataforma.png
   ├─ payoffs_2x3x2.csv
   ├─ nash_puros.csv
   ├─ pareto_front.csv                                 
   └─ Paper Competencia Estratégica en Streaming - Grupo 3.pdf  # Informe del paper
```

## 2. Dataset

Fuentes de referencia utilizadas para construir el panel:

- **Netflix:** *Netflix OTT revenue and subscribers* (Kaggle).  
- **Disney:** *Walt Disney OTT platforms revenue and subscribers* (Kaggle).  
- **Max:** *Quarterly Results* (Investor Relations de Warner Bros. Discovery).

El notebook integra estas fuentes en un **panel trimestral 2020–2024** con variables:
`subs_start_millions`, `net_adds_millions`, `subs_end_millions`, `arpu`,
banderas estratégicas (`flag_O`, `flag_P`, `flag_B`) y conteos rivales
(`riv_flag_O`, `riv_flag_P`, `riv_flag_B`).

> El panel integrado utilizado en el proyecto está en `dataset/ott_panel_quarterly_synthetic_2020_2024.csv`.

## 3. Metodología

1. **Preprocesamiento:** normalización `YYYYQn`, tipado numérico, recálculo de flags rivales por trimestre y salvaguardas (recortes suaves en `arpu` y `net_adds` si hiciera falta).
2. **Especificación OLS:**
   - `net_adds_millions ~ O + P + B + riv_O + riv_P + riv_B + C(platform)`  
   - `arpu ~ O + P + B + riv_O + riv_P + riv_B + C(platform)`  
   (efectos fijos por plataforma; errores robustos)
3. **Simulación de pagos (por perfil (N,D,M))**  
4. **Análisis del juego:** tabla **2×3×2** de pagos (millones), **mejores respuestas**, **Nash** (puros/débiles) y **Pareto**; rebanadas 2×3 fijando la estrategia de Max.


## 4. Resultados Principales

- **Matriz de pagos 2×3×2:** `outputs_project/payoffs_2x3x2.csv`  
- **Equilibrios de Nash (puros):** `outputs_project/nash_puros.csv`  
- **Perfiles Pareto-eficientes:** `outputs_project/pareto_front.csv`  
- **Visualizaciones:** series de suscriptores, altas netas, ingresos, ARPU e inversión (archivos `01`–`05`).

> El notebook imprime además las **rebanadas** (Max=O y Max=P) con los triples de pagos `(Pi{Netflix}, Pi{Disney}, Pi{Max})` por celda.


## 5. Reproducibilidad

### Opción A — Google Colab
1. Abre `notebook/Proyecto_Teoria_Juegos.ipynb` en Colab.  
2. Ejecuta todas las celdas (el notebook lee el CSV del repo).  
3. Revisa `sources/` para figuras y CSV exportados.

### Opción B — Local
```bash
# 1) Crear entorno
python -m venv .venv
source .venv/bin/activate  # (Windows: .venv\Scripts\activate)

# 2) Instalar dependencias
pip install -U numpy pandas statsmodels matplotlib

# 3) Ejecutar el notebook (opcional con jupyter)
pip install jupyter
jupyter notebook notebook/Proyecto_Teoria_Juegos.ipynb
```

## Contribuciones

Contribuciones y sugerencias son bienvenidas mediante Issues y Pull Requests.

## Ejecutar en Google Colab

Para explorar el notebook y reproducir los resultados, puedes abrir el proyecto directamente en Google Colab usando el siguiente botón:

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/mc-ivan/proyecto-teoria-juegos/blob/main/notebook/Proyecto_Teoria_Juegos.ipynb)

## Paper

Para ver el informe completo y detallado de este trabajo, accede al siguiente archivo PDF.

[📄 Paper (PDF)](<sources/Paper Competencia Estratégica en Streaming - Grupo 3.pdf>)

## Licencia

Este trabajo y los contenidos asociados (código fuente, gráficos, interpretaciones y documentación) han sido desarrollados con fines académicos y/o investigativos en el marco del proyecto de análisis de modelos de clasificación.

Salvo que se indique lo contrario, este trabajo se distribuye bajo la Licencia Creative Commons Atribución-NoComercial-CompartirIgual 4.0 Internacional (CC BY-NC-SA 4.0).

Para más detalles sobre la licencia, consultar:

[![Licencia: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)


