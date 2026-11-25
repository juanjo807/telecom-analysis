# 📱 Análisis Estadístico y Segmentación de Clientes — ConnectaTel

Proyecto del Sprint 7 del bootcamp de Análisis de Datos de **TripleTen**.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/juanjo807/telecom-analysis/blob/main/notebooks/S7_Version-Estudiante-Project-ConnectaTel.ipynb)

## 🎯 Objetivo del proyecto

Evaluar el comportamiento de uso de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en Latinoamérica, con información registrada hasta el año 2024. El análisis busca:

- detectar problemas de calidad de datos y limpiarlos,
- construir un perfil estadístico de uso por cliente,
- identificar valores atípicos (*outliers*),
- crear segmentos de clientes accionables para diseñar estrategias de retención y mejorar la oferta de planes.

---

## 📂 Datasets utilizados

> ⚠️ **Los datos no se incluyen en este repositorio.** Los tres archivos CSV pertenecen al curso de TripleTen y se entregan dentro de su plataforma.

| Archivo | Tamaño | Contenido |
|---|---|---|
| `plans.csv` | 2 filas × 8 columnas | Catálogo de planes actuales (`Basico` y `Premium`): precio mensual en USD, mensajes, GB y minutos incluidos, y costo por consumo extra. |
| `users_latam.csv` | 4,000 filas × 8 columnas | Datos de los clientes: `user_id`, nombre, edad, ciudad, fecha de registro, plan contratado y fecha de cancelación (`churn_date`). |
| `usage.csv` | 40,000 filas × 6 columnas | Detalle del uso real: llamadas (`call`, con duración en minutos) y mensajes (`text`, con longitud). |

---

## 🔄 Etapas del análisis

1. **Carga y exploración inicial:** dimensiones, columnas y tipos de datos de los tres datasets.
2. **Calidad de datos:** conteo de nulos, valores inválidos (*sentinels*) como `-999` en `age` y `'?'` en `city`, y fechas fuera de rango (registros futuros en 2026).
3. **Limpieza:** `age` imputada con la mediana, valores inválidos convertidos a `NaN`/`NaT`, y verificación de que los nulos en `duration` y `length` son estructurales (dependen de `type`).
4. **Estadísticas de uso por usuario:** agregación por `user_id` (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`), unión con `users` y resumen descriptivo.
5. **Distribuciones y outliers:** histogramas por plan, *boxplots* y límites superiores con el método IQR.
6. **Segmentación:** nivel de uso (`Bajo uso`, `Uso medio`, `Alto uso`) y grupo de edad (`Joven`, `Adulto`, `Adulto Mayor`).
7. **Insight ejecutivo:** hallazgos y recomendaciones para el negocio.

---

## 🔍 Hallazgos principales

- **Calidad de datos:** 40 fechas de registro futuras (1.00 %), edades `-999` y ciudades con `'?'` que se estandarizaron como nulas.
- **Planes:** 64.88 % de los clientes tiene el plan `Basico` y 35.12 % el `Premium`.
- **El plan no explica el consumo:** la edad, los mensajes, las llamadas y los minutos se distribuyen de forma muy similar en ambos planes.
- **Segmentos de uso:** `Uso medio` concentra 73.58 % de la base; `Bajo uso` 19.48 % y `Alto uso` 6.95 %.
- **Segmentos de edad:** `Adulto` 50.45 %, `Adulto Mayor` 30.55 % y `Joven` 19.00 %.
- **Outliers:** se mantienen porque corresponden a usuarios con consumo real alto (hasta 155.69 minutos), no a errores de captura.

Las recomendaciones comerciales (migración de clientes intensivos al plan `Premium`, plan intermedio y paquetes para el segmento joven) están detalladas al final del notebook.

---

## 🚀 Cómo ejecutar el notebook

Antes de empezar, consigue los tres CSV y guárdalos en una carpeta `datasets/`. El notebook original los lee desde `/datasets/` (la ruta del entorno de TripleTen), así que **si lo ejecutas en otro lugar debes cambiar las tres rutas de `pd.read_csv()`** por la ubicación de tus archivos.

### Opción 1: Google Colab

1. Haz clic en el botón **Open in Colab** de arriba, o abre [Google Colab](https://colab.research.google.com/) y usa **Archivo → Abrir cuaderno → GitHub** con la URL de este repositorio.
2. Sube los tres CSV al panel de archivos de Colab (quedan en `/content/`) y cambia las rutas en la celda de carga, por ejemplo `pd.read_csv('/content/plans.csv')`.
3. Ejecuta todo con **Entorno de ejecución → Ejecutar todas**.

### Opción 2: Entorno local (Jupyter)

1. Clona el repositorio:
   ```bash
   git clone https://github.com/juanjo807/telecom-analysis.git
   cd telecom-analysis
   ```
2. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```
3. Coloca los CSV en `datasets/` y ajusta las rutas del notebook a `datasets/plans.csv`, etc.
4. Abre el notebook con Jupyter y ejecuta todas las celdas en orden:
   ```bash
   jupyter notebook
   ```

---

## 📋 Guía de reproducción

- **Python:** 3.8 o superior.
- **Librerías:** `pandas`, `numpy`, `seaborn`, `matplotlib` y `jupyter` (ver `requirements.txt`).
- **Orden:** ejecuta las celdas de arriba hacia abajo; cada paso depende de las variables creadas en el anterior (`users`, `usage`, `user_profile`).

---

## 🗂️ Estructura del repositorio

```
telecom-analysis/
├── notebooks/
│   └── S7_Version-Estudiante-Project-ConnectaTel.ipynb
├── README.md
└── requirements.txt
```

---

## 👤 Autor

[@juanjo807](https://github.com/juanjo807) — estudiante de Análisis de Datos en TripleTen.
