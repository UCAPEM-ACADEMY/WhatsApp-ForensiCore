# 🔍 WhatsApp ForensiCore | Solución de Análisis Forense Digital

[![License](https://img.shields.io/badge/License-Uso_Gratuito-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v.1.0.2-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Win%20%7C%20Mac%20%7C%20Linux-lightgrey.svg)]()
[![Tech Stack](https://img.shields.io/badge/Tech-Python%20%7C%20CustomTkinter%20%7C%20Google_AI-green.svg)]()

## 🛡️ Descripción y Valor Estratégico

**WhatsApp ForensiCore** es una herramienta esencial de **Análisis Forense Digital** diseñada para la extracción, consolidación y presentación de evidencia proveniente de Archivos Incrementales de WhatsApp (Android).

El proyecto se enfoca en la **integridad probatoria** (ISO 27037) y la **trazabilidad del proceso** (ISO 27043), proporcionando a peritos judiciales y analistas una cadena de custodia clara, desde el descifrado hasta la generación del reporte final. Su arquitectura modular permite un análisis profundo, incluyendo la **recuperación de eventos de alto valor probatorio (AVE)** como mensajes eliminados y ediciones de contenido.

---

## ✨ Módulos de la Aplicación y Alcance Funcional

La interfaz se estructura en cuatro módulos funcionales, cada uno diseñado para cumplir una fase crítica del proceso forense.

### 1. Módulo de Adquisición y Conversión
Este módulo se enfoca en la **preparación y la seguridad del caso**:
* **Gestión de Caso:** Permite al perito establecer la información básica del caso (Nombre del Perito, Nombre del Caso) que luego se integrará automáticamente en el Reporte Forense.
* **Manejo de Base de Datos:** Permite la carga de archivos `msgstore.db` (bases de datos) y la gestión del proceso de descifrado.

### 2. Módulo de Análisis y Recuperación
El núcleo del análisis forense. Este módulo procesa la base de datos para construir una línea de tiempo completa y detallada:
* **Extracción de Eventos AVE:** Identifica y recupera registros de mensajes que han sido **eliminados, editados o marcados como anulados**, esenciales para la investigación.
* **Consolidación de Datos:** Combina información de múltiples tablas (mensajes, llamadas, participantes) para presentar una vista unificada y cronológica de la actividad del usuario.
* **Trazabilidad:** Procesa los metadatos de los archivos de base de datos para asegurar el cumplimiento de la **Cadena de Custodia**.

### 3. Módulo de Reportes Forenses
Este módulo es responsable de la documentación y presentación final de la evidencia, siguiendo un estándar de calidad judicial:
* **Generación PDF:** Utiliza la librería **ReportLab** para generar reportes estructurados en formato PDF, listos para ser presentados en un tribunal.
* **Exportación de Datos Crudos:** Permite exportar la línea de tiempo completa a formatos planos como **CSV**, facilitando la integración con otras herramientas forenses (ej., Nuix, EnCase).
* **Auditoría de Acciones:** Incluye un **Log de Auditoría** que registra todas las acciones tomadas por el perito dentro de la herramienta, asegurando la trazabilidad total (ISO 27043).

### 4. Módulo de Interpretación con IA
Integración de la **Inteligencia Artificial** para soporte en la toma de decisiones e interpretación de grandes volúmenes de datos:
* **Análisis Rápido:** Permite al perito enviar fragmentos de conversaciones o líneas de tiempo consolidadas a la API de **Google Gemini** para obtener resúmenes ejecutivos, análisis de sentimientos o la identificación de patrones de actividad sospechosa.
* **Generación de Conclusiones:** Asiste en la redacción de conclusiones forenses basadas en el análisis de texto.
* **Reporte AI Suplementario:** Genera un PDF aparte con las preguntas, respuestas e interpretaciones obtenidas de la IA, manteniendo la evidencia principal inalterada.

---

## 💻 Requisitos Técnicos Mínimos

Para la ejecución estable de **WhatsApp ForensiCore** desde el código fuente o como binario compilado (si se utiliza la versión pre-empaquetada), se requieren los siguientes componentes:

### Requisitos de Software (Windows, macOS, Linux)

| Componente | Requisito Mínimo | Notas |
| :--- | :--- | :--- |
| **Sistema Operativo** | Windows (64-bit), macOS (64-bit), Distribuciones Linux modernas. | Soporte nativo para Python y librerías C/C++. |
| **Python** | Python 3.10 o superior (versión estable). | Requerido para ejecutar el código fuente. |
| **Acceso a Internet** | Requerido | Esencial para las consultas al **Módulo de Interpretación con AI (Gemini)**. |

---

## 📜 Licencia y Uso

Este software es de **Uso Gratuito (FREE FOR USE)** para fines educativos.

**IMPORTANTE (USO PROFESIONAL):** Si el uso de esta herramienta será de carácter **profesional, pericial o comercial**, el usuario deberá realizar una **donación de apoyo** al proyecto. Una vez confirmada la donación, se le enviará el **código de registro** correspondiente, el cual activa el soporte técnico y el uso formal de la aplicación.

**Derechos de Autor (Copyright):** Todos los derechos sobre el código fuente, la propiedad intelectual y la arquitectura de la aplicación están reservados. No se permite la redistribución, modificación o venta de este código sin un acuerdo de licencia formal. El uso está sujeto al Acuerdo de Licencia de Usuario Final (EULA) incluido en la aplicación.

**Contacto:** Para soporte avanzado, licencias de usuario registrado o información sobre donaciones, por favor contacte a `support@ucapem.group`.

