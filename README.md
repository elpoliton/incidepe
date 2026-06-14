# IncidePe + Certificado Joven 🏛️

> **Hackathon TransformaGob 2026 · Desafío 17 CEPLAN — "Voz joven sin barreras"**

Sistema modular y omnicanal que intercepta a jóvenes de 18–25 años en los tiempos muertos de traslado dentro de las estaciones de la Línea 1 del Metro de Lima, convirtiendo sus testimonios en insumos formales de política pública — trazables, anonimizados y con respaldo legal.

---

## 📋 Tabla de contenidos

- [El problema](#el-problema)
- [La solución](#la-solución)
- [Módulos del sistema](#módulos-del-sistema)
- [Demo en vivo](#demo-en-vivo)
- [Instalación local](#instalación-local)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Marco legal](#marco-legal)
- [Fórmula IAJ y Octógonos](#fórmula-iaj-y-octógonos)
- [Equipo](#equipo)
- [Licencia](#licencia)

---

## El problema

Los jóvenes de 18 a 25 años en Lima Sur y Lima Este (zonas periféricas) no participan en procesos de políticas públicas porque:

- Los canales formales son **complejos, lentos y adultocentristas**
- Sus voces raramente llegan a quienes diseñan políticas
- No existe devolución de resultados — participar no tiene impacto visible
- El tiempo disponible es escaso y fragmentado (traslados, colas)

---

## La solución

**IncidePe** intercepta a los jóvenes exactamente donde tienen tiempo disponible: **en las colas y andenes de la Línea 1 del Metro de Lima** (Estaciones Bayóvar y Villa El Salvador), convirtiendo ese tiempo muerto en participación ciudadana real mediante un flujo de WhatsApp de 2 minutos.

```
[QR en la estación] → [WhatsApp chatbot] → [Pipeline IA] → [Tracker] → [Política pública]
```

---

## Módulos del sistema

### 1. 📱 Módulo de Ingesta — Chatbot WhatsApp
- Activación por Deep Link desde código QR físico en la estación
- Lenguaje cercano, sin burocracia — como habla un amigo
- Acepta texto o nota de voz (hasta 1 minuto)
- Detecta la estación automáticamente por el identificador del QR

### 2. 🔍 Backend — Pipeline de Procesamiento Semántico
- **Tarea A:** Anonimización PII en tiempo real (regex + NER)
- **Tarea B:** Clasificación semántica por ejes CEPLAN (NLP)
- **Tarea C:** Vinculación normativa y registro en macrozona

### 3. 📍 Tracker de Trazabilidad Ciudadana (PWA)
Cinco estados en tiempo real, estilo "tracker de delivery":

| Estado | Descripción |
|--------|-------------|
| 1 · Recibido y anonimizado | PII protegida bajo Ley N.º 29733 |
| 2 · Procesamiento semántico | Clasificado por eje temático CEPLAN |
| 3 · Vinculación normativa | Expediente colectivo bajo Ley N.º 26300 |
| 4 · En evaluación técnica | Mesa técnica intersectorial CEPLAN |
| 5 · Incidencia efectiva | Incorporado a Política Nacional de Juventud |

### 4. 🏆 Ranking Nacional — Sistema de Octógonos
Dashboard institucional con el **Índice de Apertura Juvenil (IAJ)** visible en GOB.PE.

---

## Demo en vivo

🌐 **[incidepe.github.io/incidepe](https://incidepe.github.io/incidepe)**

La demo incluye:
- Simulación completa de la conversación WhatsApp (arquetipo: Vanessa, 22 años, VES)
- Tracker interactivo con los 5 estados
- Calculadora en vivo del IAJ con activación de octógonos
- Código backend completo en Python

---

## Instalación local

### Demo (solo frontend)
```bash
# Clona el repositorio
git clone https://github.com/tu-usuario/incidepe.git
cd incidepe

# Abre en el navegador — sin dependencias
open index.html
```

### Backend Python completo
```bash
# Instala dependencias
pip install -r requirements.txt

# Ejecuta el pipeline de ejemplo
python -m incidepe.pipeline

# Levanta la API (FastAPI)
uvicorn incidepe.api:app --reload
```

`requirements.txt`:
```
fastapi>=0.111.0
uvicorn>=0.29.0
spacy>=3.7.0
python-multipart>=0.0.9
```

---

## Estructura del proyecto

```
incidepe/
├── index.html              # Demo interactivo completo (standalone)
├── README.md               # Este archivo
├── LICENSE                 # MIT License
├── requirements.txt        # Dependencias Python
│
├── incidepe/               # Paquete Python (backend)
│   ├── __init__.py
│   ├── anonymizer.py       # Anonimización PII — Ley N.º 29733
│   ├── classifier.py       # Motor semántico CEPLAN
│   ├── iaj_calculator.py   # Fórmula IAJ + sistema de octógonos
│   ├── pipeline.py         # Orquestador principal
│   └── api.py              # API REST (FastAPI)
│
├── pwa/                    # Tracker de trazabilidad (React PWA)
│   ├── src/
│   │   ├── App.jsx
│   │   ├── Tracker.jsx
│   │   └── ShareCard.jsx
│   └── package.json
│
└── docs/                   # Documentación y arquitectura
    ├── arquitectura.md
    └── flujo-conversacional.md
```

---

## Marco legal

| Norma | Aplicación en el sistema |
|-------|--------------------------|
| **Ley N.º 29733** (Protección de Datos) | Anonimización automática de PII antes del almacenamiento |
| **Ley N.º 26300** (Participación Ciudadana) | Clasificación legal de aportes como Consulta Ciudadana Virtual Masiva |
| **DL 1412 Art. 29** (Software Público) | Código bajo Licencia MIT, auditable y reutilizable por entidades del Estado |
| **Guía CEPLAN — Políticas Nacionales** | Mapeo de testimonios a la Fase 1: Diagnóstico del Problema Público |

---

## Fórmula IAJ y Octógonos

```
IAJ = (TAP × 0.40) + (ITD × 0.20) + (DPP × 0.20) + (GSC × 0.20)
```

| Indicador | Peso | Descripción |
|-----------|------|-------------|
| TAP | 40% | Tasa de Absorción de Propuestas — aportes que llegaron al Estado 5 |
| ITD | 20% | Índice de Trazabilidad y Devolución — usuarios notificados |
| DPP | 20% | Densidad de Participación Periférica — aportes de macrozonas periféricas |
| GSC | 20% | Grado de Satisfacción Ciudadana — promedio encuesta 1–5 |

### Reglas de activación (orden de prioridad)

| Condición | Octógono | Efecto en GOB.PE |
|-----------|----------|------------------|
| IAJ ≥ 85% | 🟢 **Verde** | Certificado Joven — destacado como modelo |
| IAJ < 50% y TAP < 15% | 🔴 **Rojo A** | Sanción: "Exceso de adultocentrismo" |
| ITD < 30% | 🔴 **Rojo B** | Sanción: "Bajo en trazabilidad" |
| 50% ≤ IAJ < 85% | 🟡 **Ámbar** | En proceso de mejora — observado |

---

## Equipo

Desarrollado para el **Hackathon TransformaGob 2026** — CEPLAN + PCM + Ministerio de Juventud.

---

## Licencia

**MIT License** — Copyright © 2026 Equipo IncidePe

Se autoriza el uso, copia, modificación y distribución del software para cualquier propósito, incluyendo uso por entidades del Estado Peruano, bajo los términos de la Licencia MIT y en cumplimiento del Decreto Legislativo N.º 1412, Artículo 29.

---

> *"Del tiempo muerto al cambio real."* 🇵🇪
