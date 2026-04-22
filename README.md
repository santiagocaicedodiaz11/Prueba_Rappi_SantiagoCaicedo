# 📊 Rappi Store Availability — AI Dashboard

> Dashboard interactivo para analizar la disponibilidad de tiendas en Rappi en tiempo real, con visualizaciones avanzadas y un asistente de IA integrado.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat&logo=chartdotjs&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat)

---

## 🖼️ Vista previa

El dashboard presenta un diseño **fintech premium** con paleta azul eléctrico, tipografía moderna y efectos de profundidad. Incluye métricas clave, gráficas interactivas y un chat asistido por IA en el panel lateral.

---

## ✨ Características

- **Carga de CSV multi-archivo** — Arrastra y suelta uno o varios archivos CSV de SignalFx/Splunk; el dashboard los fusiona automáticamente y deduplica los puntos.
- **Serie de tiempo** — Gráfica de línea con gradiente, agregación configurable (por minuto, 5 min, 30 min, hora o sin agrupar).
- **Histograma de distribución** — Visualiza cómo se distribuyen los valores de tiendas visibles en el período analizado.
- **Gráfica comparativa** — Pico máximo vs. mediana, promedio y mínimo del período.
- **Tabla de estadísticas por día** — Promedio, máximo, mínimo, variación y tendencia para cada día cargado.
- **Filtros dinámicos** — Por métrica, período (última hora, 6h, 24h, 7 días o todo) y nivel de agregación.
- **Asistente de IA** — Chat lateral con contexto completo de los datos. Responde preguntas en español sobre caídas, tendencias, anomalías y resúmenes ejecutivos. Funciona con OpenRouter (LLaMA 3) o puede adaptarse a cualquier modelo compatible.
- **Diseño responsivo** — Interfaz de dos columnas con scroll independiente para dashboard y chat.

---

## 🗂️ Formato de datos esperado

El dashboard está diseñado para CSVs exportados desde **SignalFx / Splunk** con el siguiente formato:

| Plot name | metric (sf_metric) | Value Prefix | Value Suffix | `<timestamp 1>` | `<timestamp 2>` | ... |
|---|---|---|---|---|---|---|
| visible_stores | synthetic_monitoring_visible_stores | | | 12500 | 12480 | ... |

- Las primeras 4 columnas son metadatos de la métrica.
- Las columnas restantes son timestamps en formato `Sun Feb 01 2026 06:11:20 GMT-0500 (hora estándar de Colombia)`.
- Cada fila representa una serie de tiempo de una métrica distinta.

Puedes descargar un CSV de ejemplo desde [este enlace](https://drive.google.com/file/d/1RlX-BzLvSehEc_cwCuWmu_PhFRiNJvrE/view?usp=sharing).

---

## 🚀 Cómo usarlo

Este proyecto es un archivo HTML estático. No necesita instalación ni servidor.

**1. Clona el repositorio**
```bash
git clone https://github.com/tu-usuario/rappi-availability-dashboard.git
cd rappi-availability-dashboard
```

**2. Abre el archivo en tu navegador**
```bash
# Opción A: Abrir directamente
open rappi_dashboard.html

# Opción B: Con un servidor local (recomendado)
npx serve .
# o
python -m http.server 8080
```

**3. Carga tus archivos CSV**
Arrastra los archivos CSV al área de carga o selecciónalos desde el explorador de archivos.

**4. Configura tu API Key (opcional)**
Para activar el chat con IA, haz clic en el botón **API Key** en el header e ingresa tu clave de [OpenRouter](https://openrouter.ai/). Si no la configuras, el asistente responderá con análisis locales sobre los datos cargados.

---

## 🤖 Asistente de IA

El chat lateral envía automáticamente el contexto completo de los datos al modelo (estadísticas por hora, por día, promedios, máximos, mínimos y tendencias). Puedes hacer preguntas como:

- *"¿Cuándo fue el pico máximo de tiendas?"*
- *"¿A qué hora hay más disponibilidad?"*
- *"Dame un resumen ejecutivo de los datos"*
- *"¿Hay alguna caída notoria en el período?"*

El sistema tiene un fallback local inteligente que responde sin IA para las consultas más frecuentes (caídas, top incidentes, resumen).

**Modelo por defecto:** `meta-llama/llama-3-8b-instruct` vía OpenRouter. Puedes cambiar el modelo editando la variable `model` en el script.

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|---|---|
| HTML5 / CSS3 / JS vanilla | Estructura, estilos e interactividad |
| [Chart.js 4.4](https://www.chartjs.org/) | Visualizaciones de datos |
| [PapaParse 5.4](https://www.papaparse.com/) | Parsing de archivos CSV |
| [OpenRouter API](https://openrouter.ai/) | Modelo de lenguaje para el chat |
| Google Fonts (Outfit + DM Mono) | Tipografía |

---

## 📁 Estructura del proyecto

```
rappi-availability-dashboard/
├── rappi_dashboard.html   # Archivo principal (todo-en-uno)
└── README.md
```

El dashboard es un **single-file app**: HTML, CSS y JS están en un solo archivo para máxima portabilidad.

---

## ⚙️ Personalización

**Cambiar el modelo de IA**
Busca esta línea en el script y reemplaza el modelo:
```javascript
model: "meta-llama/llama-3-8b-instruct",
```

**Cambiar la métrica analizada**
Por defecto el dashboard busca la columna `metric (sf_metric)`. Si tu CSV tiene otro formato, ajusta la función `parseSignalFxCSV`.

---

## 📄 Licencia

MIT © 2025 — Libre para uso personal y comercial.

---

<p align="center">Hecho con ⚡ para el equipo de operaciones de Rappi</p>
