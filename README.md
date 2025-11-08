# 🔍 WhatsApp ForensiCore | Solución de Análisis Forense Digital

[![License](https://img.shields.io/badge/License-Uso_Gratuito-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v.1.0.2-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Win%20%7C%20Mac%20%7C%20Linux-lightgrey.svg)]()
[![Tech Stack](https://img.shields.io/badge/Tech-Python%20%7C%20CustomTkinter%20%7C%20Google_AI-green.svg)]()

## 🛡️ Descripción y Valor Estratégico

**WhatsApp ForensiCore** es una herramienta esencial de **Análisis Forense Digital** diseñada para la extracción, consolidación y presentación de evidencia proveniente de bases de datos de WhatsApp (Android/iOS).

El proyecto se enfoca en la **integridad probatoria** (ISO 27037) y la **trazabilidad del proceso** (ISO 27043), proporcionando a peritos judiciales y analistas una cadena de custodia clara, desde el descifrado hasta la generación del reporte final. Su arquitectura modular permite un análisis profundo, incluyendo la **recuperación de eventos de alto valor probatorio (AVE)** como mensajes eliminados y ediciones de contenido.

---

## ✨ Módulos de la Aplicación y Alcance Funcional

La interfaz se estructura en cuatro módulos funcionales, cada uno diseñado para cumplir una fase crítica del proceso forense.

### 1. Módulo de Adquisición y Conversión (Frame de Licenciamiento y Configuración)
Este módulo se enfoca en la **preparación y la seguridad del caso**:
* **Licenciamiento Criptográfico:** Implementa la librería `cryptography` con cifrado Fernet para proteger el acceso a la aplicación y vincular el uso a un registro.
* **Gestión de Caso:** Permite al perito establecer la información básica del caso (Nombre del Perito, Nombre del Caso) que luego se integrará automáticamente en el Reporte Forense.
* **Manejo de Base de Datos:** Permite la carga de archivos `msgstore.db` (bases de datos) y la gestión del proceso de descifrado.

### 2. Módulo de Análisis y Recuperación (Parser Module)
El núcleo del análisis forense. Este módulo procesa la base de datos para construir una línea de tiempo completa y detallada:
* **Extracción de Eventos AVE:** Identifica y recupera registros de mensajes que han sido **eliminados, editados o marcados como anulados**, esenciales para la investigación.
* **Consolidación de Datos:** Combina información de múltiples tablas (mensajes, llamadas, participantes) para presentar una vista unificada y cronológica de la actividad del usuario.
* **Trazabilidad:** Procesa los metadatos de los archivos de base de datos para asegurar el cumplimiento de la **Cadena de Custodia**.

### 3. Módulo de Reportes Forenses (Report Module)
Este módulo es responsable de la documentación y presentación final de la evidencia, siguiendo un estándar de calidad judicial:
* **Generación PDF:** Utiliza la librería **ReportLab** para generar reportes estructurados en formato PDF, listos para ser presentados en un tribunal.
* **Exportación de Datos Crudos:** Permite exportar la línea de tiempo completa a formatos planos como **CSV**, facilitando la integración con otras herramientas forenses (ej., Nuix, EnCase).
* **Auditoría de Acciones:** Incluye un **Log de Auditoría** que registra todas las acciones tomadas por el perito dentro de la herramienta, asegurando la trazabilidad total (ISO 27043).

### 4. Módulo de Interpretación con IA (Gemini AI Frame)
Integración de la **Inteligencia Artificial** para soporte en la toma de decisiones e interpretación de grandes volúmenes de datos:
* **Análisis Rápido:** Permite al perito enviar fragmentos de conversaciones o líneas de tiempo consolidadas a la API de **Google Gemini** para obtener resúmenes ejecutivos, análisis de sentimientos o la identificación de patrones de actividad sospechosa.
* **Generación de Conclusiones:** Asiste en la redacción de conclusiones forenses basadas en el análisis de texto.
* **Reporte AI Suplementario:** Genera un PDF aparte con las preguntas, respuestas e interpretaciones obtenidas de la IA, manteniendo la evidencia principal inalterada.

---

## 💻 Requisitos Técnicos y Compilación

Este proyecto está construido en Python con una interfaz gráfica basada en **CustomTkinter**.

### 1. Entorno y Dependencias

Para compilar o ejecutar desde el código fuente, instale las siguientes dependencias:

```bash
# Nuitka (Compilación), CustomTkinter (GUI), Google AI, ReportLab, Criptografía
python3 -m pip install nuitka customtkinter pillow google-genai cryptography reportlab
