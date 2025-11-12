# 🔍 WhatsApp ForensiCore | Solución de Análisis Forense Digital

[![License](https://img.shields.io/badge/License-Uso_Gratuito_No_Comercial-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v.1.0.2-orange.svg)]()
[![Platform](https://img.shields.io/badge/Platform-Win%20%7C%20Mac%20%7C%20Linux-lightgrey.svg)]()
[![Tech Stack](https://img.shields.io/badge/Tech-Python%20%7C%20CustomTkinter%20%7C%20Google_AI-green.svg)]()

<div align="center">
  <img src="https://ucapem.group/wp-content/uploads/2025/11/ForensiCore.png" alt="Logo de ForensiCore - Análisis Forense Digital" width="800"/>
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

## 🎯 Configuracion Inicial

**WhatsApp ForensiCore** puede ser ejecutado desde cualquier directorio o ruta, pero para un mejor desempeño se recomienda:

### 1. Ruta
Se recomienda descomprimir o copiar el aplicativo en la **unidad principal C:\ForensiCore**

### 2. Primera Ejecución
Al ejecutar y crear por primera vez un caso, al momento de salvar los datos, se recomienda **guardarlo en la misma ruta C:\ForensiCore**, porteriormente cerrar el programa y volver a ejecutarlo para que entre en funcionamiento los demas módulos.
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

### 🔑 Código de Licencia para la Comunidad Educativa y de Investigación

Para activar las funcionalidades del software en entornos educativos y garantizar su uso sin restricciones temporales, hemos habilitado un código de licencia genérico para la comunidad:

| **Tipo de Licencia** | **Código de Registro** | **Vigencia** |
| :--- | :--- | :--- |
| **Académico / Investigación** | `Z0FBQUFBQnBFZ0t3N014NzhDV3dQdUl6cUpEdFNiWk5Ya0dKZ3VkSmUxamlGQXVWUGg5Zm5rZ2w4RERRV0dCVEgzdFNvQ29mN0Vic2xyTjdmcVVyWE9nbUQxMnVXNlktZzEwYjMwMk5rZGxNZ0FQZUV2dDFsM3E5OWptVGYtTGplT2ZEVTZRSTN0RFJGODRHVlN5bllTYTRzY0NnMm1KeHU4SjJFZG1xX3JnbTJrNlViVnZLWllsaTdId0FIOS1HRl80YmZDNHA2bHdyQlFaUEdEazVhbmFEdmJfT2FOLUp1Y3JpcUtzNC1LWWdKaDEwVUlpTEhoWDltYkJRUDZnbVJyb1VVbzYxM3gxUXhlc3c0UU15STFRaHgzTGp0UlJmNzN6MlpZOXozX2RBY0ZoWUNGSFBmN3c9` | **Indefinido** (Sujeto a renovación) |

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

### 💰 Niveles de Contribución Sugeridos

Para asegurar que podemos cubrir los costos operativos y seguir invirtiendo en nuevas funcionalidades y estándares ISO, solicitamos amablemente que las contribuciones sean:

> **El soporte sugerido es de $30 USD en adelante.**
> Agradecemos inmensamente tu apoyo, el cual se traduce directamente en la mejora continua de la herramienta forense.

### ¡Apoya Nuestro Trabajo!

Haga clic en el botón de abajo para realizar su donación y obtener su código de registro profesional:

[![Donar con PayPal](https://img.shields.io/badge/PayPal-Donar-blue.svg?logo=paypal)](https://www.paypal.com/ncp/payment/NFEJUW3KN82WG)

<a href="https://www.paypal.com/ncp/payment/NFEJUW3KN82WG" target="_blank">
  <img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donar con PayPal" />
</a>

> **PASOS POST-DONACIÓN:**
> **Es fundamental** que, una vez realizada la donación, envíe un correo electrónico a **`support@ucapem.group`** con los siguientes datos para poder generar y enviar su código de registro:
> 1. **Nombre y Apellido**
> 2. **Número de Teléfono** (Incluyendo Código de País)
> 3. **Correo Electrónico**
> 4. **Comprobante de Donación**

**URL de Apoyo Directo (Donaciones):** `https://www.paypal.com/ncp/payment/NFEJUW3KN82WG`

---

## ☕ ¿Te sirvió este proyecto?

¡Genial! Puedes **apoyar al desarrollador** con un café virtual (da clic en el botón):

<a href="https://buymeacoffee.com/perito.lattuusuario" target="_blank">
  <img src="https://storage.ko-fi.com/cdn/kofi_stroke_cup.svg" width="180" alt="Support me on Ko-fi">
</a>

> *Cualquier apoyo ayuda a seguir mejorando el proyecto.*
