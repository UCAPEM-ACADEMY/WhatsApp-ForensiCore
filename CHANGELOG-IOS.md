# Registro de Cambios (Changelog)

Todas las actualizaciones notables de WhatsApp ForensiCore se documentarán en este archivo. 
El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

## [4.0.0] - 2026-04-05
## ⚙️ Capacidades Técnicas Principales

### 1. Adquisición y Extracción de Evidencia
* **Android:** Módulo de fijación de pantalla interactiva, extracción mediante técnicas de *Downgrade* forense (preservando datos de la aplicación sin acceso root) y adquisición de respaldos encriptados.
* **iOS:** Adquisición lógica de respaldos (iTunes Backup), descifrado forense de contenedores locales, exploración de *Keychain* y extracción de estructuras *CoreData* aisladas.

### 2. Análisis Estructural y *Deep Carving*
* **Decodificación:** Parsing automático de bases de datos `msgstore.db` (Android) y `ChatStorage.sqlite` (iOS).
* **Carving Avanzado:** Rastreo y extracción de datos en *Free Pages* y memoria transaccional (WAL - Write-Ahead Logging). Recuperación de mensajes eliminados, audios y contenido multimedia efímero (Mensajes de "Ver una vez").
* **Trazabilidad:** Cálculo automático de firmas Hash (SHA-256) para garantizar la integridad bit a bit de cada contenedor analizado.

### 3. Interpretación Forense Asistida por Inteligencia Artificial
* **Análisis Heurístico:** Integración con motores de IA de última generación (Gemini 1.5 Pro) para procesar de forma automatizada las líneas de tiempo extraídas.
* **Perfilación Anti-Forense:** Capacidad de la IA para identificar dinámicas de comunicación criminal, uso de artefactos efímeros y comportamientos deliberados de ocultamiento de rastros.
* **Copiloto Forense:** Asistente conversacional integrado (Chatbot IA) entrenado en metodologías forenses digitales para asistir al perito durante su investigación en tiempo real.

### 4. Reportabilidad Legal
* **Dictámenes Automatizados:** Generación interactiva de visores HTML y dictámenes técnicos en PDF listos para su presentación en tribunales, incluyendo la separación de hallazgos vivos vs. rescatados mediante *carving*.
* **Integración IPED:** Exportación de *datasets* estructurados listos para ser consumidos por el software IPED (Indexador y Procesador de Evidencia Digital).

---
