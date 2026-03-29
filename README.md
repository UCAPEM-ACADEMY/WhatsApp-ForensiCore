# 🔍 WhatsApp ForensiCore | Solución de Análisis Forense Digital

[![License](https://img.shields.io/badge/License-Uso_Gratuito_No_Comercial-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v.3.1.1-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Win%20%7C%20Mac%20%7C%20Linux-lightgrey.svg)]()
[![Tech Stack](https://img.shields.io/badge/Tech-Python%20%7C%20CustomTkinter%20%7C%20Google_AI-green.svg)]()

<div align="center">
  <a href="https://www.youtube.com/watch?v=n2w6BTI5MhQ&t=2742s&pp=ygUGdWNhcGVt" target="_blank">
    <img src="https://ucapem.group/wp-content/uploads/2026/03/ForensiCore_v3.1.1.png" alt="Ver Demo de ForensiCore" width="1020"/>
  </a>
  <p><strong>🎥 Video - Lanzamiento WhatsApp ForensiCore v3.0.0</strong></p>
</div>

---

## 🔄 Historial de Actualizaciones

Mantenemos un registro estricto de todas las mejoras, correcciones y nuevas herramientas integradas en cada versión de la suite.

👉 **[Ver el Registro de Cambios completo (CHANGELOG)](CHANGELOG.md)**

---

## 🛡️ Descripción y Valor Estratégico

**WhatsApp ForensiCore** es una herramienta esencial de **Análisis Forense Digital** diseñada para la extracción, consolidación y presentación de evidencia proveniente de Archivos Incrementales de WhatsApp (Android).

El proyecto se enfoca en la **integridad probatoria** (**ISO 27037**) y la **trazabilidad del proceso** (**ISO 27043**), proporcionando a peritos judiciales y analistas una cadena de custodia clara, desde el descifrado hasta la generación del reporte final. Su arquitectura modular permite un análisis profundo, incluyendo la **recuperación de eventos de alto valor probatorio (AVE)** como mensajes eliminados y ediciones de contenido.

Este es un **proyecto de código cerrado (Proprietary)**, ofrecido de forma **gratuita** para la comunidad educativa y de investigación, pero que requiere un código de registro para su uso profesional y comercial.

---

## ✨ Arquitectura y Alcance Funcional de WhatsApp ForensiCore

WhatsApp ForensiCore ha evolucionado de un extractor de bases de datos a una Suite Forense Integral con capacidades de análisis heurístico, indexación avanzada, visión computacional y generación de dictámenes asistidos por IA. Todo el flujo de trabajo está alineado estrictamente a las normativas internacionales para el manejo de evidencia digital (ISO/IEC 27037, 27042 y 27043).

La interfaz y el motor interno se estructuran en cuatro módulos principales, diseñados para cubrir cada fase crítica del ciclo de vida de la respuesta a incidentes y el análisis forense móvil:

### 📱 1. Módulo de Adquisición Avanzada y Entorno Seguro
Este módulo se enfoca en la extracción física/lógica, la preparación de la evidencia y el aislamiento seguro del caso:
* **Gestión Pericial:** Registro de metadatos del caso (Nombre del Perito, Número de Caso, Credenciales) que blindan la cadena de custodia desde el primer clic.
* **Bypass de Sandbox (APK Downgrade Automatizado):** Orquestación segura vía ADB para Android 11+ (sin necesidad de Root). Degrada temporalmente la aplicación a una versión heredada para forzar la habilitación del adb backup, extrayendo el contenedor cifrado (/data/data/com.whatsapp) y la llave criptográfica (key), preservando intactos los datos del usuario.
* **Extracción E2EE:** Captura nativa de copias de seguridad con cifrado de extremo a extremo.
* **Aislamiento en Montaje VHD:** Aislamiento de la evidencia cruda en discos virtuales cifrados (Datos.vhd) para prevenir la contaminación de hashes por el sistema operativo anfitrión.
* **Radar Anti-Mod y Telemetría:** Detección automática de entornos de "Perfiles de Trabajo" y aplicaciones clonadas o no oficiales (WhatsApp Plus, GBWhatsApp).

### 🔎 2. Módulo de Análisis, Deep Carving y Recuperación
El núcleo heurístico del análisis forense. Este módulo procesa las bases de datos y la memoria residual para resucitar evidencia:
* **Manejo Dinámico de DBs:** Lectura de bases de datos vivas (msgstore.db), archivos incrementales, y sus respectivos archivos de registro transaccional (-wal y -shm).
* **Deep Carving y Triage Volumétrico:** **(Solo Usuarios Registrados)** Motor avanzado de búsqueda en espacio no asignado (Free-Pages) y memoria transaccional para el rescate binario crudo de textos e imágenes RAW eliminadas.
* **Resurrección Efímera ("Ver una vez"):** Reconstrucción criptográfica y conexión a los servidores de Meta (mmg.whatsapp.net) mediante derivación de llaves HKDF.
* **Key Hunting (Fuerza Bruta MAC):** Algoritmos avanzados para rescatar llaves multimedia huérfanas de mensajes destruidos, restaurando la extensión real de archivos corruptos mediante la lectura de Magic Bytes.
* **Filtro Forense Anti-Ruido Máximo:** Motor heurístico que detecta y destruye código residual SQLite, índices FTS, JSON, vCards y enlaces de enrutamiento interno de Meta, evitando falsos positivos en la tabla de textos huérfanos.
* **Consolidación Cronológica (Eventos AVE):** Combina y unifica mensajes, llamadas, geolocalizaciones y participantes en una sola línea de tiempo inmutable.

### 📄 3. Módulo de Trazabilidad, Exportación y Reportes
Responsable de la documentación y presentación final de la evidencia bajo estándares de calidad judicial:
* **Visor HTML Interactivo:** Nuevo motor offline que genera dictámenes web responsivos, incluyendo galerías visuales de evidencia efímera, reproductores multimedia integrados y alertas visuales para imágenes RAW corruptas.
* **Generación de Dictámenes PDF:** Creación de reportes periciales formales. Incluye tablas de triage volumétrico (conteo de Tombstones/Free-Pages) y truncamiento inteligente de mensajes extensos con derivación a CSV.
* **Exportación de Datos Crudos:** **(Solo Usuarios Registrados)** Salida de la línea de tiempo completa a formatos planos (CSV, JSON) para su ingesta en plataformas de eDiscovery de terceros (ej. Nuix, EnCase).
* **Auditoría Estricta (ISO 27043):** Archivo audit_log.txt inmutable en la raíz del caso que registra cada clic, módulo ejecutado y error del perito, garantizando la trazabilidad total sin contaminar los subdirectorios de extracción.
* **Integración Nativa con IPED:** ForensiCore actúa como orquestador directo para IPED (Digital Evidence Processor and Indexer). Aísla automáticamente los directorios de evidencia pura (Smart Exclusion) para aplicar OCR y búsqueda de expresiones regulares optimizando CPU/RAM.

### 🧠 4. Módulo de Inteligencia Artificial Forense (Offline/Online)
Integración de IA para soporte en la toma de decisiones, procesamiento multimedia y análisis de grandes volúmenes de datos:
* **Procesamiento NLP Local (Whisper AI):** Motor de transcripción local (CPU int8) que convierte notas de voz y llamadas (OGG/M4A/MP3) a texto de forma 100% autónoma y offline, sin comprometer la confidencialidad de la evidencia enviándola a la nube.
* **Visión Computacional (OpenCV):** Extracción automática de cuadros clave (frames) en videos recuperados para su indexación en el dictamen visual.
* **Asistencia Pericial (Gemini 2.5 Flash):** Conexión vía API para análisis criminalístico de líneas de tiempo consolidadas. Aplica lógica investigativa para redactar resúmenes ejecutivos, evaluar la intencionalidad de ocultamiento, e identificar dinámicas de comunicación entre involucrados.
* **Reporte AI Suplementario:** Generación de un anexo PDF independiente con las interpretaciones y conclusiones obtenidas por la IA, manteniendo la presentación de la evidencia cruda y principal estrictamente separada e inalterada.

---

## 🎯 Configuracion Inicial

**WhatsApp ForensiCore** puede ser ejecutado desde cualquier directorio o ruta, pero para un mejor desempeño se recomienda:

### 1. Ruta
Instalar el aplicativo en la **ruta por defecto C:\Archivos de programa\ForensiCore**

### 2. Primera Ejecución
**Se debe ejecutar con privilegios de administrador** y crear por primera vez un caso, al momento de salvar los datos, se recomienda **guardarlo en la misma ruta por defecto C:\Adquisicion-ForensiCore**, porteriormente cerrar el programa y volver a ejecutarlo para que entre en funcionamiento los demas módulos.
Posterior al primer caso, en los siguientes, despues de dar clic en el botón **Guardar Caso** se debe seleccionar el directorio donde se encuentre el directorio com.whatsapp con las respectivas bases de datos desencriptadas.

---

## 💻 Requisitos Técnicos Mínimos

Para la ejecución estable de **WhatsApp ForensiCore** desde el código fuente o como binario compilado (si se utiliza la versión pre-empaquetada), se requieren los siguientes componentes:

### Requisitos de Software (Windows)

| Componente | Requisito Mínimo | Notas |
| :--- | :--- | :--- |
| **Sistema Operativo** | Windows (64-bit) | Soporte nativo para Python y librerías C/C++. |
| **Python Opcional** | Python 3.12 (versión estable). | Requerido para ejecutar futuras actualizaciones. |
| **Acceso a Internet** | Requerido | Esencial para las consultas al **Módulo de Interpretación con AI (Gemini)**. |

---

## 📜 Licencia y Política de Uso (Código Cerrado)

Este software es de **Código Cerrado (Proprietary)** y su uso está regulado por la siguiente política:

### 🎓 Uso Educativo y de Investigación (Gratuito)
**WhatsApp ForensiCore** se ofrece de forma **gratuita** para su uso por parte de **estudiantes, docentes e investigadores** en el ámbito académico y no comercial. Se solicita un reconocimiento al proyecto en cualquier publicación o trabajo derivado.

### 🔑 Código de Registro para la Comunidad Educativa y de Investigación (v1.0.2 - v2.0.0) - Código de Instalación V3.0.0

Para activar las funcionalidades del software en entornos educativos y garantizar su uso sin restricciones temporales, hemos habilitado un código de registro genérico para la comunidad:

### 🎓 Licencia Académica / Investigación

| **Tipo de Registro** | **Código de Registro** | **Vigencia** |
| :--- | :--- | :--- |
| **Académico / Investigación<br>V1.0.2 - v2.0.0** | <details><summary>👉 Clic para revelar código</summary><code>Z0FBQUFBQnBFZ0t3N014NzhDV3dQdUl6cUpEdFNiWk5Ya0dKZ3VkSmUxamlGQXVWUGg5Zm5rZ2w4RERRV0dCVEgzdFNvQ29mN0Vic2xyTjdmcVVyWE9nbUQxMnVXNlktZzEwYjMwMk5rZGxNZ0FQZUV2dDFsM3E5OWptVGYtTGplT2ZEVTZRSTN0RFJGODRHVlN5bllTYTRzY0NnMm1KeHU4SjJFZG1xX3JnbTJrNlViVnZLWllsaTdId0FIOS1HRl80YmZDNHA2bHdyQlFaUEdEazVhbmFEdmJfT2FOLUp1Y3JpcUtzNC1LWWdKaDEwVUlpTEhoWDltYkJRUDZnbVJyb1VVbzYxM3gxUXhlc3c0UU15STFRaHgzTGp0UlJmNzN6MlpZOXozX2RBY0ZoWUNGSFBmN3c9</code></details> | **Indefinido** (Sujeto a renovación) |

| **Versión** | **Código de Instalación** | **Vigencia** |
| :--- | :--- | :--- |
| **ForensiCore v3.0.0** | `34ZOBsTEzP21046` | **Indefinido** |

### 💼 Uso Profesional, Pericial o Comercial (Registro Requerido)

Si la herramienta se utiliza con **fines profesionales, periciales, comerciales** o cualquier actividad generadora de ingresos, el usuario deberá realizar una **donación de apoyo al proyecto**. Una vez confirmada la donación, se le enviará el código de registro correspondiente. Este código de registro:
* Activa la versión completa de uso formal.
* Incluye acceso a soporte técnico avanzado.
* Garantiza el cumplimiento del Acuerdo de Licencia de Usuario Final (EULA).

**Derechos de Autor (Copyright):** Todos los derechos sobre el código fuente, la propiedad intelectual y la arquitectura de la aplicación están reservados. No se permite la ingeniería inversa, la redistribución, modificación o venta de este código.

**Contacto:** Para soporte avanzado, licencias de usuario registrado o información de cumplimiento, por favor contacte a `support@ucapem.group`.

---

## 💖 Apoyo y Contribución al Proyecto

El desarrollo y mantenimiento de **WhatsApp ForensiCore** representa una inversión significativa. Su apoyo es fundamental para garantizar la **excelencia, estabilidad y continuidad** del proyecto.

### 💰 Niveles de Contribución y Soporte

Para garantizar la sostenibilidad del proyecto, la inversión en nuevas funcionalidades y el cumplimiento de estándares ISO 27037/27042, hemos establecido diferentes niveles de soporte según la versión de la herramienta:

> **[!IMPORTANTE]**
> **Antes de realizar su contribución:** Le solicitamos amablemente **revisar las Notas de Versión**. Esto le permitirá verificar las capacidades técnicas y compatibilidad de cada entrega para asegurarse de que el aporte corresponda a la versión de su interés.

### ¡Apoya Nuestro Trabajo!

Haga clic en el botón de abajo para realizar su donación y obtener su código de registro profesional:

<table>
  <tr>
    <td align="center">
      <b>ForensiCore V1.0.2</b><br>
      <small>Android</small><br>
      <small>Donativo $30</small><br>
      <small>Sin Soporte</small>
    </td>
    <td align="center">
      <b>ForensiCore V2.0.0</b><br>
      <small>Android</small><br>
      <small>Donativo $50</small><br>
      <small>Sin Soporte</small>
    </td>
    <td align="center">
      <b>ForensiCore V3.1.1</b><br>
      <small>Android</small><br>
      <small>Donativo $100</small><br>
      <small>Actualizaciones Periódicas</small>
    </td>
    <td align="center">
      <b>ForensiCore V3.1.1</b><br>
      <small>Android</small><br>
      <small>Donativo $130</small><br>
      <small>Actualizaciones Periódicas</small>
    </td>
    <td align="center">
      <b>ForensiCore V4.0.0</b><br>
      <small>Android - iOS</small><br>
      <small>Donativo $150</small><br>
      <small>Actualizaciones Periódicas</small>
    </td>
    <td align="center">
      <b>ForensiCore V4.0.0</b><br>
      <small>Android - iOS</small><br>
      <small>Donativo $180</small><br>
      <small>Actualizaciones Periódicas</small>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://www.paypal.com/ncp/payment/NFEJUW3KN82WG" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
    </td>
    <td align="center">
      <a href="https://www.paypal.com/ncp/payment/UVGZAACSN25H4" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
    </td>
    <td align="center">
      <a href="https://www.paypal.com/ncp/payment/WXG5QS7R3JNTL" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
    </td>
    <td align="center">
      <a href="https://www.paypal.com/ncp/payment/S6MUPKWXCDZQE" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
    </td>
    <td align="center">
      <a href="https://www.paypal.com/ncp/payment/D48BEBLN5Z8PG" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
      <td align="center">
      <a href="https://www.paypal.com/ncp/payment/D48BEBLN5Z8PG" target="_blank">
        <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar">
      </a>
    </td>
  </tr>
</table>

> **PASOS POST-DONACIÓN:**
> **Es fundamental** que, una vez realizada la donación, envíe un correo electrónico a **`support@ucapem.group`** con los siguientes datos para poder generar y enviar su código de registro:
> 1. **Nombre y Apellido**
> 2. **Número de Teléfono** (Incluyendo Código de País)
> 3. **Correo Electrónico**
> 4. **Comprobante de Donación**
---

## ☕ ¿Te sirvió este proyecto?

¡Genial! Puedes **apoyar al desarrollador** con un café virtual (da clic en el botón):

<a href="https://buymeacoffee.com/perito.lat" target="_blank">
  <img src="https://storage.ko-fi.com/cdn/kofi_stroke_cup.svg" width="100" alt="Support me on Ko-fi">
</a>

> *Cualquier apoyo ayuda a seguir mejorando el proyecto.*
