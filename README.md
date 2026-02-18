# sprint7-final-project
# 📱 ConnectaTel — Análisis de Segmentación de Clientes

## 🎯 Objetivo del Proyecto

Realizar un análisis exploratorio y de segmentación sobre la base de clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con el fin de identificar patrones de uso, detectar valores extremos, y clasificar a los usuarios en segmentos accionables que permitan mejorar la oferta de planes y estrategias de retención.

---

## 📂 Dataset Utilizado

| Archivo | Descripción |
|---|---|
| `plans.csv` | Base de datos principal con información de los planes actuales (precio, minutos incluidos, GB incluidos, costo por extra) |
|`users.csv` | Base de datos principal con información demográfica y de uso de 4,000 clientes de ConnectaTel |
|`usage.csv` | Base de datos principal con información del detalle de uso real de los servicios (llamadas y mensajes) |

### Variables principales

| Variable | Tipo | Descripción |
|---|---|---|
| `plan_name` | Texto | Básico o Premium |
| `age` | Numérica | Edad del usuario (18–79 años) |
| `cant_mensajes` | Numérica | Cantidad de mensajes enviados |
| `cant_llamadas` | Numérica | Cantidad de llamadas realizadas |
| `age` | Numérica | Edad del usuario (18–79 años) |
| `cant_mensajes` | Numérica | Cantidad de mensajes enviados |
| `cant_llamadas` | Numérica | Cantidad de llamadas realizadas |
| `type` | Texto | Call or text |
| `cant_minutos_llamada` | Numérica | Total de minutos en llamadas |
| `grupo_uso` | Categórica (creada) | Clasificación por nivel de uso |
| `grupo_edad` | Categórica (creada) | Clasificación por rango de edad |

---

## 🔬 Etapas del Análisis

### 1. 🧹 Calidad de Datos
- Revisión de valores nulos y registros duplicados así como número de filas y columnas en cada dataset.
- Detección de inconsistencias entre columnas (por ejemplo, `age` tenía 4,000 registros vs. 3,999 en variables de uso)
- Exploramos columnas categóricas en el dataset users.
- Estandarización de columnas. (en fechas)
- Decisión de limpieza documentada por variable, desde 'age' por inconsistencias, 'city' para limpiar las faltantes, ´reg_date´por años pasados y futuros en el dataset 2024.

### 2. 📊 Análisis Exploratorio (EDA)
- Resumen de estadísticas a tráves de conteos y renombre de columnas, con el fin de obtener promedios, minimos, máximos y desviacion estándar. 
- Generación de boxplots para las variables `age`, `cant_mensajes`, `cant_llamadas` y `cant_minutos_llamada`
- Cálculo de estadísticas descriptivas con `.describe()`
- Identificación visual de distribuciones y asimetría

### 3. 🚨 Detección y Tratamiento de Outliers
- Aplicación del método **IQR** para calcular límites superiores en las variables de uso
- Comparación entre límite IQR y valor máximo real por variable
- Decisión: **mantener todos los outliers** al representar comportamientos reales de usuarios (heavy users)

| Variable | Límite Superior IQR | Máximo Real | Decisión |
|---|---|---|---|
| `cant_mensajes` | 11.5 | 17 | ✅ Mantener |
| `cant_llamadas` | 10.5 | 15 | ✅ Mantener |
| `cant_minutos_llamada` | 61.86 | 155.69 | ✅ Mantener |

### 4. 🏷️ Segmentación de Usuarios

**Por nivel de uso** — columna `grupo_uso`:
- `Bajo uso`: llamadas < 5 **y** mensajes < 5
- `Uso medio`: llamadas < 10 **y** mensajes < 10
- `Alto uso`: resto de casos

**Por edad** — columna `grupo_edad`:
- `Joven`: age < 30
- `Adulto`: age < 60
- `Adulto Mayor`: age ≥ 60

### 5. 📈 Visualización de Segmentos
- Countplots con `seaborn` para `grupo_uso` y `grupo_edad`
- Gráficos con orden lógico (bajo → alto / joven → adulto mayor) y paletas diferenciadas por dimensión

### 6. 💡 Conclusiones y Recomendaciones de Negocio
- Identificación del segmento más valioso: **Adulto + Alto uso**
- Oportunidad de upselling en el segmento **Adulto + Uso medio** (mayor volumen)
- Propuesta de productos: Plan Heavy Caller, Plan Joven, Programa de fidelización Adulto Mayor

---

## 🛠️ Tecnologías Utilizadas

- **Python** — lenguaje principal
- **Pandas** — manipulación y análisis de datos
- **Matplotlib / Seaborn** — visualización
- **Jupyter Notebook** — entorno de desarrollo

---

## 👥 Audiencia

Este análisis está dirigido al equipo de **producto y marketing** de ConnectaTel para apoyar decisiones sobre diseño de planes, segmentación de campañas y estrategias de retención de clientes.
