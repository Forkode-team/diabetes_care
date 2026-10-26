# 📊 Diabetes Care Dashboard

> Panel de monitoreo de diabetes tipo 1 con análisis de reportes AGP de Linx CGM y calculadora de factor de corrección de insulina

[![Live Demo](https://img.shields.io/badge/demo-live-success?style=for-the-badge)](https://forkode-team.github.io/diabetes_care/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue?style=for-the-badge)](LICENSE)
[![Made with Love](https://img.shields.io/badge/Made%20with-❤️-red?style=for-the-badge)](https://github.com/Forkode-team/diabetes_care)

---

## 🌟 Características

- **📄 Análisis de PDF AGP**: Procesa reportes AGP de Linx CGM en español
- **🧮 Calculadora de Factor de Corrección**: Calcula ISF usando reglas médicas estándar (1500/1700/1800)
- **📈 Visualizaciones Interactivas**:
  - Tendencia de Tiempo en Rango (TIR) de 30 días
  - Perfil Ambulatorio de Glucosa (AGP)
  - Gráficos de patrones diarios
- **🔍 Detección de Patrones**: Identifica patrones de glucosa por hora del día y día de la semana
- **📱 Responsive**: Funciona en desktop, tablet y móvil
- **🔒 100% Privado**: Todo el procesamiento ocurre en tu navegador (no se envían datos a servidores)
- **⚡ Offline-Ready**: Funciona sin conexión después de la primera carga

---

## 🚀 Demo en Vivo

**Accede al dashboard aquí**: [https://forkode-team.github.io/diabetes_care/](https://forkode-team.github.io/diabetes_care/)

---

## 📋 Tabla de Contenidos

- [¿Qué es el Factor de Corrección?](#-qué-es-el-factor-de-corrección)
- [Cómo Usar](#-cómo-usar)
- [Tecnologías](#️-tecnologías)
- [Instalación Local](#-instalación-local)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Explicación Técnica](#-explicación-técnica)
- [Advertencias Médicas](#️-advertencias-médicas)
- [Contribuir](#-contribuir)
- [Licencia](#-licencia)

---

## 🧮 ¿Qué es el Factor de Corrección?

El **Factor de Corrección** (o **Factor de Sensibilidad a la Insulina**, ISF) es un valor que indica **cuántos mg/dL baja tu glucosa por cada unidad de insulina rápida**.

### Fórmulas Médicas Estándar

Este dashboard utiliza las reglas médicas reconocidas internacionalmente:

| Regla | Fórmula | Uso |
|-------|---------|-----|
| **1500** | `ISF = 1500 ÷ TDD` | Insulina regular (acción lenta) |
| **1700** | `ISF = 1700 ÷ TDD` | Insulina rápida con MDI (múltiples inyecciones) |
| **1800** | `ISF = 1800 ÷ TDD` | Insulina rápida con bomba de insulina |

**TDD** = Dosis Diaria Total de insulina (basal + bolos)

### Ejemplo Práctico

Si tu TDD es 56 unidades/día:

```
ISF (1800) = 1800 ÷ 56 = 32 mg/dL por unidad
```

Esto significa: **1 unidad de insulina rápida bajará tu glucosa aproximadamente 32 mg/dL**

### Ajustes Basados en Patrones

El dashboard también ajusta la recomendación según:

- **Alta variabilidad (CV% > 36%)**: Factor más conservador (-10%)
- **Hipoglucemias frecuentes (TBR > 4%)**: Factor más conservador (-15%)
- **Hiperglucemias frecuentes (TAR > 70% y TBR < 2%)**: Ligero aumento (+5%)

---

## 📖 Cómo Usar

### Paso 1: Obtener tu Reporte AGP

1. Abre la app de **Linx CGM**
2. Ve a **Reportes** → **AGP (Ambulatory Glucose Profile)**
3. Genera reporte de **30 días**
4. Descarga como **PDF**

### Paso 2: Cargar el PDF

1. Accede al dashboard: [https://forkode-team.github.io/diabetes_care/](https://forkode-team.github.io/diabetes_care/)
2. Arrastra tu PDF a la zona de carga o haz clic para seleccionarlo
3. Espera unos segundos mientras se procesa

### Paso 3: Calcular tu Factor de Corrección

1. **Ingresa tus dosis diarias**:
   - Insulina basal (ej: Lantus): `22` unidades
   - Desayuno: `14` unidades
   - Almuerzo: `10` unidades
   - Cena: `10` unidades

2. El **TDD se calcula automáticamente** (ej: 56 unidades/día)

3. **(Opcional)** Ingresa el factor que te dio tu endocrinólogo para comparar

4. Haz clic en **"Calcular Factor de Corrección"**

### Paso 4: Revisar Resultados

El dashboard te mostrará:

- ✅ **Tres cálculos** (reglas 1500/1700/1800)
- ✅ **Recomendación personalizada** ajustada por patrones de glucosa
- ✅ **Explicación** de los ajustes aplicados
- ✅ **Comparación** con el factor de tu endocrinólogo (si lo ingresaste)
- ✅ **Métricas clave**: GMI, MBG, CV%, TIR, TAR, TBR
- ✅ **Visualizaciones** de tendencias de 30 días
- ✅ **Patrones detectados** (horas del día, días de la semana)

---

## 🛠️ Tecnologías

Este proyecto es un **archivo HTML standalone** que utiliza:

| Tecnología | Versión | Propósito |
|-----------|---------|-----------|
| **[PDF.js](https://mozilla.github.io/pdf.js/)** | 3.11.174 | Extracción de texto de PDFs en navegador |
| **[Chart.js](https://www.chartjs.org/)** | 4.4.0 | Visualizaciones de datos (gráficos interactivos) |
| **[chartjs-plugin-annotation](https://www.chartjs.org/chartjs-plugin-annotation/)** | 3.0.1 | Líneas de referencia en gráficos |
| **[Tailwind CSS](https://tailwindcss.com/)** | CDN | Framework CSS responsive |
| **[Day.js](https://day.js.org/)** | 1.11.10 | Manejo de fechas en español |
| **Vanilla JavaScript (ES6+)** | - | Lógica de la aplicación |

### ¿Por qué estas tecnologías?

- **Sin servidor requerido**: Todo funciona client-side
- **Sin framework pesado**: Vanilla JS mantiene el bundle pequeño (~100KB)
- **CDN loading**: No requiere build process
- **Privacidad total**: Los datos del PDF nunca salen de tu navegador
- **Offline-capable**: Funciona sin internet después de la primera carga

---

## 💻 Instalación Local

### Opción 1: Abrir Directamente

El archivo `index.html` puede abrirse directamente en cualquier navegador moderno:

```bash
# Descargar el repositorio
git clone https://github.com/Forkode-team/diabetes_care.git
cd diabetes_care

# Abrir en navegador (Windows)
start index.html

# Abrir en navegador (macOS)
open index.html

# Abrir en navegador (Linux)
xdg-open index.html
```

### Opción 2: Servidor Local

Para mejor rendimiento con PDFs grandes:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server -p 8000

# Luego abre: http://localhost:8000
```

---

## 📁 Estructura del Proyecto

```
diabetes_care/
├── index.html              # Aplicación completa (standalone)
├── README.md              # Este archivo
└── LICENSE                # Licencia Apache 2.0
```

### Arquitectura Interna (index.html)

```
index.html
├── <head>
│   ├── CDN links (PDF.js, Chart.js, Tailwind)
│   └── Estilos personalizados
│
├── <body>
│   ├── Header
│   ├── Zona de carga de PDF
│   ├── Dashboard Container
│   │   ├── Métricas resumen (GMI, MBG, CV%, TIR)
│   │   ├── Calculadora de Factor de Corrección
│   │   ├── Visualización TIR (30 días)
│   │   ├── Curva AGP
│   │   ├── Detección de Patrones
│   │   └── Tabla desglose diario
│   └── Footer (disclaimers)
│
└── <script>
    ├── CONFIG (constantes)
    ├── GlucoseData (modelo de datos)
    ├── DailyMetrics (modelo de datos)
    ├── LinxPDFParser (extracción de PDF)
    ├── CorrectionFactorCalculator (cálculo ISF)
    ├── PatternDetector (análisis de patrones)
    ├── TIRVisualizer (gráfico TIR)
    ├── AGPVisualizer (curva AGP)
    └── DiabetesDashboard (controlador principal)
```

---

## 🔬 Explicación Técnica

### 1. Procesamiento de PDF

El parser utiliza **PDF.js** para extraer texto del reporte AGP:

```javascript
// Ordenamiento por coordenadas (top-to-bottom, left-to-right)
const sortedItems = textContent.items.sort((a, b) => {
    const yDiff = Math.abs(a.transform[5] - b.transform[5]);
    if (yDiff > 5) return b.transform[5] - a.transform[5]; // Y desc
    return a.transform[4] - b.transform[4]; // X asc
});
```

### 2. Extracción de Métricas

Usa **múltiples patrones regex** para robustez ante variaciones de formato:

```javascript
const gmiPatterns = [
    /GMI\s+\d+\s+mmol\/mol\s+(\d+\.?\d*)\s*%/i,
    /GMI.*?(\d+\.?\d*)\s*%/i,
    /(\d+\.?\d*)\s*%\s*<\s*7\.0/i
];
```

### 3. Cálculo del ISF

**IMPORTANTE**: Versiones anteriores usaban **MBG** (glucosa promedio) incorrectamente.

❌ **INCORRECTO** (versión antigua):
```javascript
ISF = 1800 / MBG  // Daba resultados erróneos (ej: 8 mg/dL)
```

✅ **CORRECTO** (versión actual):
```javascript
ISF = 1800 / TDD  // Usa dosis diaria total (ej: 32 mg/dL)
```

### 4. Ajustes Basados en Patrones

```javascript
let adjustmentFactor = 1.0;

if (cv > 36) adjustmentFactor *= 0.90;      // Alta variabilidad
if (tbr > 4) adjustmentFactor *= 0.85;      // Hipoglucemias frecuentes
if (tar > 70 && tbr < 2) adjustmentFactor *= 1.05;  // Hiperglucemias

recommendedISF = baseLine * adjustmentFactor;
```

### 5. Visualización TIR

Gráfico de barras apiladas con Chart.js:

```javascript
datasets: [
    { label: 'TBR (<70)', data: tbrData, backgroundColor: 'red' },
    { label: 'TIR (70-180)', data: tirData, backgroundColor: 'green' },
    { label: 'TAR (>180)', data: tarData, backgroundColor: 'yellow' }
]
```

---

## ⚠️ Advertencias Médicas

### IMPORTANTE - Lea Cuidadosamente

🩺 **Esta herramienta es solo para fines informativos y educativos**

- ❌ **NO sustituye** el consejo médico profesional
- ❌ **NO realice cambios** en su régimen de insulina sin consultar a su médico
- ❌ **NO ignore** las recomendaciones de su endocrinólogo

### Consideraciones Importantes

1. **Los cálculos son estimaciones**: Las reglas 1500/1700/1800 son guías generales que pueden no aplicar a todos los individuos

2. **Variabilidad individual**: Tu factor de corrección puede variar según:
   - Hora del día (resistencia a la insulina matutina)
   - Actividad física reciente
   - Estrés o enfermedad
   - Ciclo menstrual (en mujeres)
   - Medicamentos concurrentes

3. **Consulte siempre con su médico**: Si hay diferencia entre el cálculo y el factor de su endocrinólogo, confíe en su médico. Ellos conocen su historial completo.

4. **Seguridad ante todo**: En caso de duda, use un factor más conservador (número más alto = menos insulina)

### Privacidad de Datos

- ✅ **Todo el procesamiento es local**: Los PDFs se procesan en tu navegador
- ✅ **No se envían datos a servidores**: Nada sale de tu dispositivo
- ✅ **No hay tracking ni analytics**: Tu privacidad está protegida
- ⚠️ **No subas PDFs al repositorio**: Contienen información médica sensible

---

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Si quieres mejorar este proyecto:

### Reportar Bugs

1. Ve a [Issues](https://github.com/Forkode-team/diabetes_care/issues)
2. Haz clic en "New Issue"
3. Describe el problema con:
   - Navegador y versión
   - Pasos para reproducir
   - Comportamiento esperado vs actual
   - Screenshots si es posible

### Sugerir Mejoras

Las áreas donde más ayuda se necesita:

- 🌍 **Traducción a otros idiomas** (inglés, portugués, etc.)
- 📊 **Nuevas visualizaciones** (heatmaps, percentiles, etc.)
- 🔧 **Soporte para otros CGMs** (Dexcom, Freestyle Libre, etc.)
- 📱 **Mejoras de UX mobile**
- 🧪 **Tests automatizados**
- 📖 **Documentación médica** adicional

### Pull Requests

1. Fork el repositorio
2. Crea una rama: `git checkout -b feature/nueva-funcionalidad`
3. Commit tus cambios: `git commit -m 'Add: nueva funcionalidad'`
4. Push a la rama: `git push origin feature/nueva-funcionalidad`
5. Abre un Pull Request

### Guía de Estilo

- **JavaScript**: ES6+, sin frameworks
- **CSS**: Usa Tailwind utility classes cuando sea posible
- **Comentarios**: Documenta funciones complejas en español
- **Commits**: Usa [Conventional Commits](https://www.conventionalcommits.org/)
  - `feat:` nueva funcionalidad
  - `fix:` corrección de bug
  - `docs:` cambios en documentación
  - `style:` formato, punto y coma, etc.
  - `refactor:` refactorización de código

---

## 📚 Recursos Adicionales

### Referencias Médicas

- [ADA Standards of Care 2026](https://diabetesjournals.org/care/issue/47/Supplement_1)
- [Insulin Correction Factor Calculator (MDCalc)](https://www.mdcalc.com/calc/10187/insulin-sensitivity-factor-calculator)
- [Time in Range - Beyond A1C](https://www.beyond-a1c.com/time-in-range)

### Documentación Técnica

- [PDF.js Documentation](https://mozilla.github.io/pdf.js/)
- [Chart.js Documentation](https://www.chartjs.org/docs/latest/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

---

## 📜 Licencia

Este proyecto está bajo la licencia **Apache License 2.0**. Ver el archivo [LICENSE](LICENSE) para más detalles.

```
Copyright 2024 Forkode Team

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

---

## 🙏 Créditos

### Desarrollado con ❤️ por:

- **Forkode Team** - [@Forkode-team](https://github.com/Forkode-team)
- **LuisDi98** - [@LuisDi98](https://github.com/LuisDi98)

### Construido con asistencia de:

- **Claude (Anthropic)** - AI pair programming con Claude Sonnet 4.5

### Agradecimientos Especiales

- Comunidad de diabetes tipo 1
- Desarrolladores de PDF.js (Mozilla)
- Desarrolladores de Chart.js
- Linx CGM por proporcionar reportes AGP detallados

---

## 📞 Contacto

¿Tienes preguntas o sugerencias?

- 📧 Abre un [Issue](https://github.com/Forkode-team/diabetes_care/issues)
- 💬 Inicia una [Discussion](https://github.com/Forkode-team/diabetes_care/discussions)

---

## 🌟 Star History

Si este proyecto te ayudó, ¡considera darle una estrella! ⭐

[![Star History Chart](https://api.star-history.com/svg?repos=Forkode-team/diabetes_care&type=Date)](https://star-history.com/#Forkode-team/diabetes_care&Date)

---

<div align="center">

**Hecho con ❤️ para la comunidad de diabetes tipo 1**

[🔝 Volver arriba](#-diabetes-care-dashboard)

</div>
