# 🚦 Movilidad Urbana y Productividad Económica en América Latina (2024)

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458.svg?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-0.12%2B-3776AB.svg)](https://seaborn.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Tabla de Contenidos
- [Descripción del Proyecto](#-descripción-del-proyecto)
- [Objetivos Principal y Específicos](#-objetivos-principal-y-específicos)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Fuentes de Datos](#-fuentes-de-datos)
- [Metodología y Flujo de Trabajo](#-metodología-y-flujo-de-trabajo)
- [Principales Hallazgos y Resultados](#-principales-hallazgos-y-resultados)
- [Recomendaciones e Impacto Financiero](#-recomendaciones-e-impacto-financiero)
- [Instalación y Configuración](#-instalación-y-configuración)
- [Uso y Ejecución](#-uso-y-ejecución)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Autor y Contacto](#-autor-y-contacto)

---

## 📖 Descripción del Proyecto

El proyecto **"Movilidad urbana y productividad económica"** evalúa la relación entre la congestión del tráfico vehicular y los indicadores de desarrollo económico (PIB per cápita, desempleo, población) en las principales metrópolis latinoamericanas durante el año 2024.

Mediante el análisis cruzado de métricas de movilidad en tiempo real e históricas combinadas con indicadores socioeconómicos, este estudio identifica patrones clave de infraestructura vial, detecta anomalías en tiempos de congestión y sirve como guía estratégica para entidades financieras y gubernamentales interesadas en financiar proyectos de infraestructura de transporte e inversión pública.

---

## 🎯 Objetivos Principal y Específicos

### Objetivo Principal
Determinar si existe una correlación directa entre los altos niveles de congestión vehicular (`jams_delay`) y la productividad económica (`city_gdp_capita`) en ciudades representativas de América Latina durante el período 2024.

### Objetivos Específicos
1. **Limpieza e Integración de Datos**: Normalizar y estandarizar datos multifuente heterogéneos (formatos de fecha, separadores de miles/decimales, nombres en `snake_case`).
2. **Consolidación Espacio-Temporal**: Extraer promedios anuales agregados por ciudad y filtrar los registros correspondientes al año 2024.
3. **Análisis Exploratorio de Datos (EDA)**: Evaluar la distribución del tráfico y PIB per cápita mediante histogramas, diagramas de caja (*boxplots*) y gráficos comparativos de barras.
4. **Generación de Dataset Final**: Exportar un conjunto de datos limpio e integrado (`ladb_mobility_economy_2024_clean.csv`) listo para modelado predictivo o toma de decisiones de inversión.

---

## 📂 Estructura del Repositorio

```text
.
├── datasets/
│   ├── tomtom_traffic.csv                   # Registro histórico de tráfico global (TomTom)
│   └── oecd_city_economy.csv                # Indicadores económicos por ciudad (OECD)
├── notebooks/
│   └── movilidad_urbana_productividad.ipynb  # Cuaderno Jupyter con el flujo completo de análisis
├── ladb_mobility_economy_2024_clean.csv     # Dataset final limpio e integrado (2024)
├── requirements.txt                         # Lista de dependencias de Python
└── README.md                                # Documentación profesional del proyecto
```

---

## 📊 Fuentes de Datos

El análisis se alimenta de dos fuentes primarias internacionales:

*   **TomTom Traffic Index (`tomtom_traffic.csv`)**:
    *   Mide retrasos acumulados en minutos (`jams_delay`), índice de tráfico en vivo (`traffic_index_live`), longitud de embotellamientos en km (`jams_length_kms`), conteo de embotellamientos (`jams_count`) y tiempos de viaje por cada 10 km.
    *   Contiene más de 1,000,000 de registros.
*   **OECD Cities Economy (`oecd_city_economy.csv`)**:
    *   Contiene indicadores macroeconómicos clave a nivel metropolitano: PIB per cápita municipal (`city_gdp_capita`), tasa de desempleo (`unemployment_pct`), contaminación por material particulado (`PM_2.5_μg/m³`) y población total (`population`).

---

## 🔄 Metodología y Flujo de Trabajo

El flujo de procesamiento de datos está estructurado en 7 pasos metódicos:

1.  **Paso 1: Carga y Exploración preliminar**: Importación de librerías (`pandas`, `numpy`, `seaborn`, `matplotlib`), revisión de tipos de datos e inspección de primeras filas.
2.  **Paso 2: Limpieza y Estandarización**:
    *   Conversión de columnas al formato `snake_case` (ej. `UpdateTimeUTC` -> `update_time_utc`).
    *   Conversión de campos de fecha a `datetime64[ns]` con tolerancia a errores (`errors='coerce'`).
    *   Limpieza de separadores de miles/puntos y porcentajes en campos numéricos (`city_gdp_capita`, `unemployment_pct`, `population_m`).
3.  **Paso 3: Extracción de Año y Filtrado 2024**: Extracción del atributo `.dt.year` y selección estricta del año 2024 utilizando `.copy()` para mantener la integridad de la memoria.
4.  **Paso 4: Agregación de Promedios**: Agrupamiento `.groupby(['city', 'country', 'year'])` sobre las métricas cuantitativas clave para evitar distorsiones por mediciones diarias o por horas.
5.  **Paso 5: Integración (Merge)**: Combinación mediante `pd.merge(..., how='inner')` sobre las llaves primarias `city` y `year` para consolidar movilidad e indicadores económicos.
6.  **Paso 6: Visualización de Relaciones**:
    *   **Boxplot con media**: Evaluación de valores extremos en retrasos de tráfico (`jams_delay`).
    *   **Histograma con KDE**: Análisis de la forma funcional y distribución del PIB per cápita.
    *   **Gráfico de Barras Comparativo**: Contraste directo entre niveles de congestión e ingreso per cápita.
7.  **Paso 7: Exportación**: Generación del archivo CSV estructurado `ladb_mobility_economy_2024_clean.csv`.

---

## 📈 Principales Hallazgos y Resultados

*   **Valores Atípicos y Severidad del Tráfico**:
    *   **Ciudad de México** encabeza la congestión regional con un retraso promedio acumulado de 2,833 minutos (`jams_delay`), registrándose como un valor extremadamente atípico (*outlier*) en comparación con el resto de metrópolis.
*   **Heterogeneidad Tráfico vs. PIB**:
    *   La relación entre PIB per cápita e índice de congestión no es lineal ni estrictamente proporcional:
        *   **Curitiba** ($12,381 USD PIB/capita) y **Brasilia** ($16,251 USD PIB/capita) registran niveles de tráfico bajos (183 min y 101 min respectivamente), demostrando una infraestructura vial o densidad equilibrada.
        *   **Montevideo** destaca con el mayor PIB per cápita en la muestra metropolitana de la OECD, conservando niveles de congestión bajos.
        *   **Bogotá** presenta un caso crítico: un PIB per cápita relativamente bajo ($11,442 USD) frente a un alto nivel de retrasos por embotellamientos (1,141.55 minutos).

---

## 💡 Recomendaciones e Impacto Financiero

*   **Ciudad Prioritaria para Inversión**: **Bogotá, Colombia** se consolida como la ciudad prioritaria para financiamiento en proyectos de infraestructura pública y transporte. Su brecha entre un PIB per cápita modesto y una congestión severa ofrece un alto rendimiento socioeconómico para créditos de desarrollo.
*   **Planes de Transporte Masivo**: Financiar la expansión de sistemas de transporte público limpio para reducir el parque automotor en circulación y mejorar los tiempos de traslado de la fuerza laboral.

---

## 🛠️ Instalación y Configuración

### 1. Clonar el Repositorio
```bash
git clone [https://github.com/tu-usuario/movilidad-urbana-productividad.git](https://github.com/tu-usuario/movilidad-urbana-productividad.git)
cd movilidad-urbana-productividad
```

### 2. Crear y Activar un Entorno Virtual
* **Linux/macOS:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
* **Windows:**
  ```cmd
  python -m venv venv
  venv\Scripts\activate
  ```

### 3. Instalar Dependencias
```bash
pip install pandas numpy seaborn matplotlib jupyter
```

---

## 🚀 Uso y Ejecución

Abre el cuaderno Jupyter interactivo para explorar el código paso a paso:

```bash
jupyter notebook notebooks/movilidad_urbana_productividad.ipynb
```

---

## 🧰 Tecnologías Utilizadas

* **Lenguaje**: Python 3.9+
* **Procesamiento de Datos**: Pandas, NumPy
* **Visualización de Datos**: Seaborn, Matplotlib
* **Entorno de Desarrollo**: Jupyter Notebook / Google Colab

---

## 👤 Autor y Contacto

Desarrollado con enfoque en Data Analytics & Data Science.

- **GitHub**: [@tu-usuario](https://github.com/tu-usuario)
- **LinkedIn**: [Tu Perfil](https://www.linkedin.com/in/tu-perfil)
