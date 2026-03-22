# 🔍 WhatsApp ForensiCore | Solución de Análisis Forense Digital

[![License](https://img.shields.io/badge/License-Uso_Gratuito_No_Comercial-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v.3.0.0-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Win%20%7C%20Mac%20%7C%20Linux-lightgrey.svg)]()
[![Tech Stack](https://img.shields.io/badge/Tech-Python%20%7C%20CustomTkinter%20%7C%20Google_AI-green.svg)]()

<div align="center">
  <a href="https://www.youtube.com/watch?v=n2w6BTI5MhQ&t=2742s&pp=ygUGdWNhcGVt" target="_blank">
    <img src="https://ucapem.group/wp-content/uploads/2026/03/ForensiCorev3.0.0.png" alt="Ver Demo de ForensiCore" width="1020"/>
  </a>
  <p><strong>🎥 Video - Lanzamiento WhatsApp ForensiCore v3.0.0</strong></p>
</div>

---

## 🛡️ Descripción y Valor Estratégico

**WhatsApp ForensiCore** es una herramienta esencial de **Análisis Forense Digital** diseñada para la extracción, consolidación y presentación de evidencia proveniente de Archivos Incrementales de WhatsApp (Android).

El proyecto se enfoca en la **integridad probatoria** (**ISO 27037**) y la **trazabilidad del proceso** (**ISO 27043**), proporcionando a peritos judiciales y analistas una cadena de custodia clara, desde el descifrado hasta la generación del reporte final. Su arquitectura modular permite un análisis profundo, incluyendo la **recuperación de eventos de alto valor probatorio (AVE)** como mensajes eliminados y ediciones de contenido.

Este es un **proyecto de código cerrado (Proprietary)**, ofrecido de forma **gratuita** para la comunidad educativa y de investigación, pero que requiere un código de registro para su uso profesional y comercial.

---

## ✨ Módulos de la Aplicación y Alcance Funcional

La interfaz se estructura en cuatro módulos funcionales, cada uno diseñado para cumplir una fase crítica del proceso forense.

### 1. Módulo de Adquisición y Conversión
Este módulo se enfoca en la **preparación y la seguridad del caso**:
* **Gestión de Caso:** Permite al perito establecer la información básica del caso (Nombre del Perito, Nombre del Caso) que luego se integrará automáticamente en el Reporte Forense.
* **Manejo de Base de Datos y Archivos Incrementales:** Permite la carga de archivos `msgstore.db` y `msgstore-increment-xx.db` (bases de datos y archivos incrementales desencriptadas) y la gestión del proceso de extracción de indicios.

### 2. Módulo de Análisis y Recuperación
El núcleo del análisis forense. Este módulo procesa la base de datos para construir una línea de tiempo completa y detallada:
* **Extracción de Eventos AVE:** Identifica y recupera registros de mensajes que han sido **eliminados, editados o marcados como anulados**, esenciales para la investigación.
* **Consolidación de Datos:** Combina información de múltiples tablas (mensajes, llamadas, participantes) para presentar una vista unificada y cronológica de la actividad del usuario.
* **Trazabilidad:** Procesa los metadatos de los archivos de base de datos para asegurar el cumplimiento de la **Cadena de Custodia**.

### 3. Módulo de Reportes Forenses
Este módulo es responsable de la documentación y presentación final de la evidencia, siguiendo un estándar de calidad judicial:
* **Generación PDF:** Utiliza la librería **ReportLab** para generar reportes estructurados en formato PDF, listos para ser presentados en un tribunal.
* **Exportación de Datos Crudos:** Permite exportar la línea de tiempo completa a formatos planos como **CSV**, facilitando la integración con otras herramientas forenses (ej., Nuix, EnCase).
* **Auditoría de Acciones:** Incluye un **Log de Auditoría** que registra todas las acciones tomadas por el perito dentro de la herramienta, asegurando la trazabilidad total (**ISO 27043**).

### 4. Módulo de Interpretación con IA
Integración de la **Inteligencia Artificial** para soporte en la toma de decisiones e interpretación de grandes volúmenes de datos:
* **Análisis Rápido:** Permite al perito enviar archivos JSON o líneas de tiempo consolidadas a la API de **Google Gemini** para obtener resúmenes ejecutivos, análisis de continuidad o la identificación de indicios recuperados.
* **Generación de Conclusiones:** Asiste en la redacción de conclusiones forenses basadas en el análisis de texto.
* **Reporte AI Suplementario:** Genera un PDF aparte con las interpretaciones obtenidas de la IA, manteniendo la evidencia principal inalterada.

---

# 🚀 Novedades y Actualizaciones - WhatsApp ForensiCore (v.2.0.0)

Hemos elevado **WhatsApp ForensiCore** al siguiente nivel, transformándolo de un simple extractor de bases de datos a una **Suite Forense Integral** con capacidades de análisis heurístico, indexación avanzada y generación de dictámenes asistidos por IA. Todo alineado estrictamente a las normativas **ISO/IEC 27037, 27042 y 27043**.

## 🌟 Características Destacadas de la Nueva Versión

### 1. 🔓 Módulo de Adquisición Avanzada: Extracción Física/Lógica (APK Downgrade)
Se ha perfeccionado el motor de extracción automatizada para dispositivos Android, permitiendo acceder al contenedor cifrado de WhatsApp (`/data/data/com.whatsapp`) sin requerir privilegios de superusuario (Root).
* **Bypass de Sandbox (Android 12+):** Implementación de la técnica de *APK Downgrade*, que degrada temporalmente la aplicación a una versión heredada con políticas de seguridad permisivas (Target SDK antiguo) para forzar la habilitación del `adb backup`.
* **Extracción de Llaves Criptográficas:** Captura exitosa del archivo `key` y de la base de datos viva (`msgstore.db`), junto con sus archivos de registro transaccional (`-wal` y `-shm`), vitales para la recuperación de datos volátiles.
* **Orquestación ADB Segura:** Automatización del *Android Debug Bridge* que garantiza la retención de los datos del usuario durante la sustitución de paquetes, preservando la integridad de la evidencia original.

### 2. 🧠 Nuevo Módulo de Inteligencia Artificial Forense (Gemini 2.5 Flash)
Se ha integrado un motor de asistencia pericial que no solo lee los datos, sino que aplica lógica investigativa criminalística para interpretar la evidencia volátil.
* **Detección de Artefactos Anti-Forenses:** Identificación y correlación automática de registros "Tombstone" (Mensajes eliminados) y reconstrucción de mensajes "Ver una vez" (Efímeros) desde la memoria transaccional (WAL).
* **Ingeniería de Prompts Forenses:** La IA redacta hallazgos evaluando la intencionalidad de ocultamiento y la dinámica de comunicación entre los involucrados.
* **Exportación Dinámica:** Generación de **Informes en PDF y HTML** con renderizado avanzado, notas de descargo legal (disclaimers), protección de firmas y diseño responsivo.

### 3. 🔎 Integración Nativa con el Motor IPED (Digital Evidence Processor and Indexer)
Ahora ForensiCore funciona como un orquestador directo para **IPED (Digital Evidence Processor and Indexer)**, permitiendo indexar la evidencia, aplicar OCR y buscar expresiones regulares sin salir de la herramienta.
* **Filtro de Evidencia Inteligente (Smart Exclusion):** El sistema aísla automáticamente los directorios de evidencia pura (Bases de datos, Extracciones ADB, Fijaciones) y excluye los reportes internos para evitar duplicidad de hallazgos y optimizar el consumo de CPU/RAM.
* **Lectura Dinámica de Perfiles:** Detección en tiempo real de los perfiles de indexación de IPED (`default`, `forensic`, `blind`, `fast`, etc.).
* **Consola Transmisión en Vivo:** Monitoreo del flujo de procesamiento de Java directamente en la interfaz gráfica oscura de ForensiCore.

### 4. 🛡️ Trazabilidad y Cadena de Custodia Estricta
Se ha reestructurado por completo el sistema de *Logging* para garantizar la pureza de la evidencia:
* **Aislamiento de Reportes:** Creación de un único directorio centralizado llamado `Reportes` para almacenar exclusivamente las salidas finales (PDF, CSV, JSON, HTML).
* **Logs Raíz:** El archivo `audit_log.txt` (que registra cada clic, módulo ejecutado y error del perito) se guarda directamente en la raíz del caso, asegurando que la auditoría de la herramienta no contamine los subdirectorios de extracción.

---

# 🚀 Novedades y Actualizaciones - WhatsApp ForensiCore (v.3.0.0)

Esta actualización mayor transforma a **WhatsApp ForensiCore** en una suite integral de grado pericial, incorporando inteligencia artificial local (Gemini AI), métodos de adquisición agresivos y entornos de análisis aislados, alineados estrictamente a las normativas **ISO/IEC 27037, 27042 y 27043**.

## 🌟 Características Destacadas de la Nueva Versión

#### 📱 1. Adquisición Avanzada y Entorno Seguro
* **APK Downgrade Automatizado:** Bypass del Sandbox en Android 11+ (sin Root) orquestando la degradación y restauración segura de la aplicación.
* **Extracción E2EE:** Captura nativa de copias de seguridad con cifrado de extremo a extremo.
* **Montaje VHD:** Aislamiento de la evidencia en discos virtuales cifrados (`Datos.vhd`) para prevenir la contaminación de hashes por el sistema operativo anfitrión.
* **Radar Anti-Mod y Telemetría:** Detección mediante ADB de entornos de "Perfiles de Trabajo" y aplicaciones clonadas (WhatsApp Plus, GBWhatsApp).

#### 🧠 2. Inteligencia Artificial y Procesamiento Multimedia (Offline)
* **Transcriptor Whisper AI:** Procesamiento NLP local (CPU int8) para convertir notas de voz (OGG/M4A) a texto de forma autónoma, sin comprometer la confidencialidad.
* **Visión Computacional:** Módulo OpenCV para la extracción automática de cuadros clave (frames) en videos recuperados.

#### ☁️ 3. Resurrección de Evidencia y Conexión CDN
* **Descifrado de Efímeros ("Ver una vez"):** Reconstrucción criptográfica y conexión a los servidores de Meta (`mmg.whatsapp.net`) mediante derivación de llaves HKDF.
* **Key Hunting (Fuerza Bruta MAC):** Algoritmos avanzados sobre archivos `.wal` y `.shm` para rescatar llaves multimedia huérfanas de mensajes eliminados.
* **Lectura de Magic Bytes:** Identificación de cabeceras hexadecimales crudas para restaurar la extensión real de archivos corruptos.

#### 📄 4. Exportación y Trazabilidad
* **Reporte HTML Interactivo:** Nuevo motor de generación de dictámenes web offline con galerías de evidencia efímera y reproductores multimedia.
* **Mejoras en PDF Pericial:** Tabla de *triage volumétrico* (conteo de Tombstones/Free-Pages) y apéndice dinámico para mensajes que superan los 1800 caracteres.

---

## 🎯 Configuracion Inicial

**WhatsApp ForensiCore** puede ser ejecutado desde cualquier directorio o ruta, pero para un mejor desempeño se recomienda:

### 1. Ruta
Instalar el aplicativo en la **ruta ppor defecto C:\Archivos de programa\ForensiCore**

### 2. Primera Ejecución
**Se debe ejecutar con privilegios de administrador** y crear por primera vez un caso, al momento de salvar los datos, se recomienda **guardarlo en la misma ruta por defecto C:\Adquisicion-ForensiCore**, porteriormente cerrar el programa y volver a ejecutarlo para que entre en funcionamiento los demas módulos.
Posterior al primer caso, en los siguientes, despues de dar clic en el botón **Guardar Caso** se debe seleccionar el directorio donde se encuentre el directorio com.whatsapp con las respectivas bases de datos desencriptadas.

---

## 💻 Requisitos Técnicos Mínimos

Para la ejecución estable de **WhatsApp ForensiCore** desde el código fuente o como binario compilado (si se utiliza la versión pre-empaquetada), se requieren los siguientes componentes:

### Requisitos de Software (Windows, macOS, Linux)

| Componente | Requisito Mínimo | Notas |
| :--- | :--- | :--- |
| **Sistema Operativo** | Windows (64-bit), macOS (64-bit), Distribuciones Linux modernas. | Soporte nativo para Python y librerías C/C++. |
| **Python Opcional** | Python 3.9 o superior (versión estable). | Requerido para ejecutar futuras actualizaciones. |
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
      <small>Donativo $30</small>
    </td>
    <td align="center">
      <b>ForensiCore V2.0.0</b><br>
      <small>Donativo $50</small>
    </td>
    <td align="center">
      <b>ForensiCore V3.0.0</b><br>
      <small>Donativo $80</small>
    </td>
    <td align="center">
      <b>ForensiCore V3.0.0</b><br>
      <small>Donativo $100</small>
    </td>
    <td align="center">
      <b>ForensiCore V3.0.0</b><br>
      <small>Donativo $120</small>
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
