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
