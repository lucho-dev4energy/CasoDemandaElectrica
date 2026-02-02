# ⚡ Pronóstico de Demanda Eléctrica - PJM Interconnection
> **Proyecto Final: IA Aplicada al Sector Eléctrico**

Este repositorio contiene el desarrollo de un sistema de predicción de carga eléctrica horaria utilizando técnicas avanzadas de Machine Learning. El objetivo es optimizar la operación de sistemas de potencia mediante pronósticos de alta precisión.

---

## 📌 1. Contexto del Proyecto
La predicción precisa de la demanda eléctrica es crítica para los operadores de sistema (**ISO/RTO**). En un mercado moderno, con alta integración de renovables, minimizar el error de pronóstico permite:
* Reducir márgenes de reserva rodante.
* Optimizar el despacho económico.
* Evitar penalizaciones por desvíos en el mercado mayorista.

Se trabaja con datos reales de la región **PJM (2002-2018)**, una de las organizaciones de transmisión regional más grandes de EE. UU.

---

## 🎯 2. Objetivos

* **Objetivo General:** Desarrollar modelos de ML capaces de pronosticar el consumo horario (MW) minimizando el error porcentual medio (MAPE).
* **Objetivos Específicos:**
    * Realizar un **Análisis Exploratorio de Datos (EDA)** para identificar estacionalidad.
    * Implementar **Ingeniería de Características** (Variables temporales y Lags).
    * Comparar modelos de complejidad incremental: Regresión Lineal, Random Forest y Gradient Boosting.

---

## 📊 3. Descripción de los Datos
* **Fuente:** Histórico de consumo horario de PJM Interconnection (Región Este).
* **Variable Objetivo:** `PJME_MW` (Demanda en Megavatios).
* **Preprocesamiento:**
    * Limpieza de outliers (filtros para valores < 15,000 MW).
    * Manejo de fechas y estandarización de índices temporales.

### Ingeniería de Características (Feature Engineering)
Se crearon variables explicativas para capturar los ciclos de consumo:
1.  **Calendario:** `hour`, `dayofweek`, `quarter`, `month`, `year`.
2.  **Retardos (Lags):**
    * `lag_1`: Consumo de la hora anterior (Inercia inmediata).
    * `lag_24`: Consumo de la misma hora del día anterior (Periodicidad diaria).

---

## 🤖 4. Metodología y Modelado
Se aplicó una división cronológica estricta para evitar el *Data Leakage*:
* **Train:** Datos previos al 01-01-2017.
* **Test:** Datos desde 2017 hasta 2018.

### 🏆 Resultados Comparativos

| Modelo | MAE (MW) | RMSE (MW) | MAPE (%) | $R^2$ |
| :--- | :---: | :---: | :---: | :---: |
| **Gradient Boosting** | **326.06** | **438.08** | **1.03%** | **0.9949** |
| Random Forest | 597.59 | 794.76 | 1.92% | 0.9832 |
| Regresión Lineal | 976.56 | 1,250.44 | 3.15% | 0.9583 |



---

## 💡 5. Conclusiones
* **Superioridad del Boosting:** El modelo **Gradient Boosting** redujo el error en un 66% respecto a la Regresión Lineal, demostrando que la demanda eléctrica es un fenómeno intrínsecamente no lineal.
* **Poder de la Inercia:** El análisis de *Feature Importance* reveló que el **lag_1** y el **lag_24** son los predictores más críticos, confirmando la fuerte memoria de corto plazo del sistema eléctrico.
* **Impacto Operativo:** Lograr un MAPE del **1.03%** representa un nivel de precisión de clase mundial para pronósticos de corto plazo.

---

## 🚀 6. Recomendaciones Futuras
1.  **Variables Exógenas:** Integrar datos de **temperatura y humedad** para capturar la sensibilidad térmica (uso de aire acondicionado/calefacción).
2.  **Deep Learning:** Evaluar redes neuronales recurrentes tipo **LSTM** para capturar dependencias temporales de largo plazo.
3.  **MLOps:** Implementar pipelines de monitoreo de *Data Drift* para asegurar la vigencia del modelo en el tiempo.

---

## 🛠️ Stack Tecnológico
* **Lenguaje:** Python 3.12+
* **Librerías:** `Pandas`, `NumPy`, `Scikit-Learn`, `Matplotlib`, `Seaborn`.
* **Entorno:** Google Colab / Jupyter.

---
**Autor:** [lucho-dev4energy](https://github.com/lucho-dev4energy)
