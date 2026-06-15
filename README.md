# 📈 Predicción de Ventas — Rossmann Stores

Modelo de forecasting de ventas diarias para **1,115 tiendas** usando datos históricos, información por tienda y variables externas como estacionalidad, promociones, festivos y competencia.

---

## 🧠 Objetivo

Predecir las ventas futuras diarias de cada tienda, permitiendo a la empresa anticipar demanda, optimizar inventarios y planear promociones con mayor precisión.

---

## 📂 Dataset

| Archivo | Descripción |
|---|---|
| `train.csv` | ~1 millón de registros de ventas diarias por tienda (2013–2015) |
| `store.csv` | Información estática por tienda: tipo, surtido, competencia, promociones |

**Variables clave:** `Store`, `Sales`, `Customers`, `Promo`, `StateHoliday`, `SchoolHoliday`, `StoreType`, `Assortment`, `CompetitionDistance`

---

## ⚙️ Pipeline del Proyecto

### 1. Carga y Preparación de Datos
- Filtrado de tiendas cerradas (ventas y clientes en 0) para trabajar solo con días activos
- Imputación de valores nulos: `CompetitionDistance` con la media; columnas de Promo2 con 0
- Merge de `train.csv` y `store.csv` por `Store ID`
- Extracción de features temporales: `Year`, `Month`, `Day`, `Week`

### 2. Análisis Exploratorio (EDA)
- Correlación fuerte entre **Ventas y Clientes** (r = 0.82) y **Ventas y Promo** (r = 0.37)
- `Promo2` mostró correlación negativa (-0.13), sugiriendo baja efectividad
- Ventas más altas en: inicio/fin de mes, inicio de semana, y período navideño (diciembre)
- `StoreType 'b'` presentó el promedio de ventas más alto entre todos los tipos

### 3. Modelado con Facebook Prophet
- Modelo de series de tiempo robusto ante datos faltantes y cambios de tendencia
- Función `sales_predictions()` que:
  - Filtra datos por tienda
  - Prepara el formato Prophet (`ds`, `y`)
  - Integra festivos escolares y estatales como regressores externos
  - Genera forecast con intervalos de confianza (`yhat`, `yhat_lower`, `yhat_upper`)
  - Exporta predicciones a `forecast.csv`

---

## 📊 Principales Hallazgos

- Las **promociones activas (Promo=1)** incrementan significativamente tanto ventas como número de clientes
- Existe una marcada **estacionalidad semanal y mensual** en las ventas
- Los **festivos** tienen impacto medible y fue incorporado explícitamente al modelo
- El modelo genera forecasts por tienda individual, escalable a las 1,115 tiendas

---

## 🛠️ Tecnologías

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Prophet](https://img.shields.io/badge/Facebook%20Prophet-forecasting-orange)
![Pandas](https://img.shields.io/badge/Pandas-data--wrangling-lightgrey?logo=pandas)
![Matplotlib](https://img.shields.io/badge/Matplotlib-visualization-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)

---

## 🚀 Cómo ejecutar

```bash
# 1. Clonar el repositorio
git clone https://github.com/RafaRivera75/Departamento_de_Ventas.git
cd Departamento_de_Ventas

# 2. Instalar dependencias
pip install pandas numpy matplotlib prophet

# 3. Abrir el notebook
jupyter notebook "Departamento_de_Ventas .ipynb"
```

> ⚠️ El dataset original proviene de la competencia [Rossmann Store Sales en Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales). Descárgalo y coloca los archivos en la raíz del proyecto antes de ejecutar.

---

## 📁 Estructura del Proyecto

```
Departamento_de_Ventas/
│
├── Departamento_de_Ventas .ipynb   # Notebook principal
├── sales_train_all.csv             # Dataset consolidado (generado)
├── forecast.csv                    # Predicciones exportadas (generado)
└── README.md
```

---

## 👤 Autor

**Rafael Rivera** — [github.com/RafaRivera75](https://github.com/RafaRivera75)
