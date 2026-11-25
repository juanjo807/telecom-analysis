# telecom-analysis
# 📱 Análisis Estadístico y Segmentación de Clientes — ConnectaTel

## 🎯 Objetivo del Proyecto
Evaluar el comportamiento de uso de los clientes de **ConnectaTel** (operaciones en México y Colombia) con información registrada hasta el año 2024, a partir de sus registros de llamadas, mensajes de texto y planes contratados. El objetivo es detectar problemas de calidad de datos, analizar distribuciones, identificar valores atípicos (*outliers*) y construir segmentos accionables para diseñar estrategias de retención y optimizar la oferta comercial de planes.

---

## 📂 Datasets Utilizados
El análisis integra tres fuentes de datos principales:
- **`plans.csv` (2 filas × 8 columnas):** Catálogo de planes actuales (`Basico` y `Premium`), tarifas mensuales en USD, beneficios incluidos (mensajes, GB y minutos) y costos por consumo extra.
- **`users_latam.csv` (4,000 filas × 8 columnas):** Información demográfica y contractual de los clientes (`user_id`, nombre, edad, ciudad, fecha de registro, plan contratado y fecha de cancelación/`churn_date`).
- **`usage.csv` (40,000 filas × 6 columnas):** Detalle del uso real de servicios durante 2024 (`type`: llamadas `call` con su duración en minutos y mensajes `text` con su longitud en caracteres).

---

## 🔄 Etapas del Análisis Realizadas
1. **Carga y exploración inicial:** Revisión de dimensiones, columnas y tipos de datos de los tres datasets (`plans`, `users`, `usage`).
2. **Identificación de problemas de calidad de datos:** Conteo de nulos, detección de valores inválidos/sentinels (`-999` en `age`, `'?'` en `city`) y revisión de fechas fuera de rango (registros futuros en `2026`).
3. **Limpieza básica de datos:** Imputación de `age` con la mediana (`48.0`), estandarización de valores inválidos a `NaN`/`NaT` y verificación de nulos estructurales (*Missing At Random* - MAR) en `duration` y `length`.
4. **Summary statistics de uso por usuario:** Agregación de métricas por `user_id` (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`), cruce con `users` (`user_profile`) y cálculo de estadísticas descriptivas y proporciones por plan (`64.88%` Básico vs. `35.12%` Premium).
5. **Visualización de distribuciones y detección de outliers:** Creación de histogramas comparativos por plan, diagramas de caja (*boxplots*) y cálculo de límites superiores mediante el método **IQR**.
6. **Segmentación de clientes:** Clasificación por nivel de uso (`Bajo uso`, `Uso medio`, `Alto uso`) y rango etario (`Joven`, `Adulto`, `Adulto Mayor`) con visualización de proporciones mediante gráficos de barras.
7. **Insight ejecutivo para stakeholders:** Síntesis de hallazgos clave y recomendaciones comerciales (*upselling*, diseño de plan intermedio y estrategias de retención).

---

## 🚀 Cómo Ejecutar el Notebook

### Opción 1: Ejecutar en Google Colab (Recomendada)
1. Haz clic en el botón **Open in Colab** o abre [Google Colab](https://colab.research.google.com/).
2. Ve a **Archivo → Subir cuaderno** (o abre la pestaña **GitHub** e ingresa la URL de este repositorio).
3. Asegúrate de cargar los archivos CSV (`plans.csv`, `users_latam.csv`, `usage.csv`) en la ruta `/datasets/` (o actualiza la ruta dentro de `pd.read_csv()`).
4. Ejecuta todas las celdas secuencialmente desde **Entorno de ejecución → Ejecutar todas**.

### Opción 2: Ejecutar en Entorno Local (Jupyter Notebook / JupyterLab)
1. Clona este repositorio en tu computadora y entra a la carpeta del proyecto.
2. Verifica que los tres archivos CSV estén disponibles en la carpeta `/datasets/`.
3. Abre el archivo `.ipynb` con Jupyter Notebook o JupyterLab y ejecuta todas las celdas de principio a fin.

---

## 📋 Guía de Reproducción
Para reproducir exactamente los resultados y gráficos de este estudio:
- **Versión de lenguaje:** Python 3.8 o superior.
- **Librerías requeridas:**
  ```bash
  pip install pandas numpy seaborn matplotlib jupyter
