# 🚀 Rok.ai: AI VTuber Project (Low-Resource Architecture)

Este repositorio contiene la documentación, arquitectura y especificaciones de diseño de **Rok.ai**, un avatar virtual inteligente (AI VTuber) optimizado para ejecutarse de manera fluida en entornos de hardware limitado **sin tarjeta gráfica dedicada (GPU)**. 

⚠️ **WARNING / ADVERTENCIA:** 
* **Sobre la identidad:** `Rok.ai` es estrictamente un **alias confidencial** utilizado para la exposición pública de este portafolio. No representa el nombre real del software final.
* **Documentación Dinámica:** Este documento **no es fijo**. Se irá reformulando, expandiendo y modificando de manera flexible a lo largo de todo el proceso de desarrollo técnico según surjan nuevos enfoques, necesidades de optimización o cambios en la arquitectura.

> 🔒 **Nota de Desarrollo:** El código fuente, scripts de producción (Python backend) y componentes del núcleo de escritorio (Tauri core) pertenecen a un desarrollo propietario y se mantienen en un repositorio privado por razones de seguridad de credenciales (API Keys) y confidencialidad del proyecto.

---

## 📝 Descripción del Proyecto
Rok.ai es un sistema híbrido que demuestra cómo integrar Inteligencia Artificial avanzada, procesamiento de voz en tiempo real y renderizado gráfico eficiente utilizando únicamente recursos de **CPU y RAM**. 

El objetivo principal es lograr un avatar interactivo fluido que consuma el mínimo absoluto de recursos del sistema, permitiendo al usuario transmitir en vivo (streaming), trabajar o jugar en la misma computadora simultáneamente sin caídas de rendimiento.

---

## 🏗️ Arquitectura de Software (Híbrida & Descentralizada)

El sistema se divide en dos componentes independientes que se comunican localmente a través de protocolos ligeros (HTTP / WebSockets):

```text
┌────────────────────────────────────────┐
│   TAURI INTERFACE (Rust + TS)          │ 
│   - Consumo mínimo de RAM (<50MB)      │
│   - Animación por software (Sprites)    │
│   - Reproducción de audio fluida        │
└────────────────────────────────────────┘
                    ▲
                    │  (JSON / Audio Streams) via Localhost
                    ▼
┌────────────────────────────────────────┐
│   PYTHON CEREBRO (IA Backend)          │
│   - Orquestación de APIs en la nube    │
│   - Procesamiento optimizado en CPU    │
└────────────────────────────────────────┘
```
SDK
---

## 🛠️ Stack Tecnológico y Estrategia de Optimización

### 1. Frontend & Interfaz (Tauri + Rust + TypeScript)
*   **Tauri Framework:** Reemplaza soluciones pesadas como Electron, reduciendo drásticamente el uso de memoria RAM de ~500MB a menos de 50MB en ejecución.
*   **Rust Core:** Gestiona de forma segura los hilos de ejecución concurrentes, previniendo el congelamiento de la interfaz durante las peticiones y transmisiones de datos.
*   **Sprite-Based Animation (TS):** Sistema de animación por software basado en estados de imágenes fijas (PNGs) para simular parpadeo y habla (*Lip-sync*), eliminando el 100% de la carga sobre la GPU (WebGL/Live2D tradicional).

### 2. Backend & Inteligencia Artificial (Python 3.10)
*   **Cerebro (LLM):** Integración con la **Google Gemini API** (o Groq Cloud), delegando el procesamiento pesado del lenguaje a servidores externos (Consumo de CPU local para IA: 0%).
*   **Oído (STT):** Uso de `faster-whisper` (modelo *tiny*) optimizado en C++ para transcribir el micrófono del usuario en milisegundos usando solo hilos de la CPU.
*   **Voz (TTS):** Generación externa mediante la API de **ElevenLabs** o **Google TTS**, entregando al frontend un flujo de audio procesado y listo para reproducir.

---

## 📅 Roadmap de Desarrollo y Estado del Proyecto

*   [x] **Fase 0:** Diseño de arquitectura de bajo consumo y selección del Stack tecnológico.
*   [⏳] **Fase 1: El Núcleo en Python** -> Creación del script base, configuración del entorno e integración de APIs en la nube. *(En desarrollo)*
*   [ ] **Fase 2: El Puente (API Local)** -> Montar un servidor ligero (`FastAPI`) para comunicar Python con la interfaz de escritorio.
*   [ ] **Fase 3: La Ventana en Tauri** -> Construcción de la aplicación de escritorio en Rust que aloja el contenedor del avatar.
*   [ ] **Fase 4: Sincronización de Animación** -> Lógica en TypeScript para alternar los estados del Sprite según el análisis del audio entrante.
