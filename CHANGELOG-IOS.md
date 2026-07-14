# Registro de Cambios (Changelog)

Todas las actualizaciones notables de WhatsApp ForensiCore se documentarán en este archivo. 
El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

## [4.1.0] - 2026-07-14
## 🚀 Nuevos Módulos

### 1. Visor Forense de Mensajería (Chat & Contacts Viewer)
* **Visualización Dinámica e Intuitiva:** Implementación de una interfaz gráfica moderna que imita el diseño de un cliente de mensajería (panel izquierdo para chats y contactos, panel derecho para la cronología de mensajes) facilitando la lectura fluida por parte del perito.
* **Procesamiento de Base de Datos Nativo:** Lectura e interpretación directa de contenedores SQLite de WhatsApp, incluyendo `ChatStorage.sqlite` y `ContactsV2.sqlite` en iOS, y `msgstore.db` en Android, en conjunto con sus archivos de registro transaccional (`.wal` y `.shm`).
* **Transcripción de Audio Integrada con IA (Whisper):** Integración de transcripción fonética offline (Speech-to-Text) utilizando el modelo neuronal **Faster-Whisper**. Permite transcribir audios del caso de forma 100% local, garantizando que la evidencia no abandone el entorno de análisis seguro.
* **Control de Memoria y Estabilidad:** Corrección de fugas de memoria críticas al cerrar el visor mediante la destrucción explícita de componentes gráficos, previniendo caídas aleatorias de la aplicación.

### 2. Visor de Contenido Compartido (Shared Content Viewer)
* **Categorización Inteligente de Evidencia:** Módulo dedicado para agrupar y filtrar elementos multimedia y metadatos no convencionales clasificados en:
  * 📡 Canales de WhatsApp
  * 📖 Historias / Status
  * 🎞️ Reels (Instagram / TikTok / YouTube)
  * 🌐 Contenido Externo (Click-to-WhatsApp - CTWA)
  * 🎭 Stickers y GIFs animados
  * 📄 Documentos Externos
  * 📍 Ubicaciones GPS (vCard / Maps)
  * 👤 Contactos (tarjetas de contacto vCard)
  * 🔗 Links / Vistas Previas de Enlaces
* **Generación de Reportes Judiciales:** Capacidad de exportar informes formales en formatos **PDF** y **HTML**. Los reportes incluyen miniaturas de las imágenes, rutas absolutas, hashes SHA-256 de los archivos y codificación de multimedia en Base64 para visualización directa y portable.

### 3. Módulo de Importación Forense de Terceros (iOS Backup Importer)
* **Compatibilidad Ampliada:** Soporte para la importación directa de copias de seguridad de iOS (iTunes) tanto en directorios planos como en formatos comprimidos (`.zip`, `.tar`, `.tar.gz`, `.tgz`), generados por herramientas comerciales.
* **Extracción Automatizada de Metadatos:** Lectura silenciosa del archivo de configuración `Info.plist` del backup para autocompletar de manera instantánea el formulario de "Nuevo Caso" con los datos del terminal (Modelo, Versión de iOS, Número de Serie, IMEI, Número de Teléfono y UDID).
* **Seguridad y Cadena de Custodia:** Aislamiento de la evidencia original, copiado seguro al directorio del caso con generación automática de firmas criptográficas (SHA-256) y registro en la consola de auditoría interna.

## 🔧 Actualizaciones y Correcciones Críticas

### 📱 Entorno iOS

* **Preservación del Archivo WAL:**
  * **Problema:** El uso del comando `PRAGMA wal_checkpoint` forzaba el vaciado del archivo de transacciones WAL a 0 KB, eliminando de forma irreversible trazas de mensajes efímeros y eliminados recientes que solo residían en dicha área volátil.
  * **Solución:** Se desactivó el checkpoint de seguridad. Ahora el motor de análisis lee el WAL de forma nativa en su estado crudo, asegurando que la evidencia permanezca intacta para procesos posteriores de recuperación profunda (Carving).
* **Robustez en la Extracción y Subprocesos:**
  * **Problema:** Las llamadas externas a herramientas causaban bloqueos indefinidos en Windows esperando entradas en la consola, además de levantar ventanas emergentes de comandos no deseadas.
  * **Solución:** Se integró indices en todos los subprocesos ejecutados, permitiendo una ejecución silenciosa, limpia e ininterrumpida.
* **Reporte de Eventos de Llamadas:**
  * **Corrección 1 (Participantes y Remitente):** Se corrigió la asignación de remitentes en chats grupales e individuales cuando las identidades originales eran nulas o formateadas con JIDs crudos, mapeándolas automáticamente al "Propietario del Dispositivo" o "Miembro del Grupo".
  * **Corrección 2 (Duración de Llamadas):** Conversión y formateo automático de las duraciones de llamadas (horas, minutos y segundos) a partir de cadenas de texto y metadatos crudos extraídos de la base de datos de llamadas.
* **Descarga e Integración de Historias / Estados:**
  * **Descarga CDN:** Se añadió soporte para descargar y desencriptar archivos multimedia asociados a historias (`HISTORIA (ESTADO)`) directamente de los servidores CDN de Meta.
  * **Visualización Unificada:** Se actualizó el visor de iOS para buscar todas las sesiones secundarias asociadas al JID del contacto (como `@status` o `.status`), permitiendo cargar y previsualizar sus historias de forma local y exportarlas correctamente a PDF/HTML.
* **Mapeo Inteligente de Mensajes Sin Fecha:**
  * Se implementó una lógica de coincidencia relajada para enlazar mensajes huérfanos sin fecha (timestamp 0) al chat del contacto correspondiente si su contenido binario crudo recuperado por carving contiene el número telefónico o JID del contacto.
* **Rendimiento O(1) en Contenido Compartido:**
  * Se resolvió un cuello de botella crítico de rendimiento al implementar un índice plano de archivos en memoria al inicio de la extracción, evitando lecturas y búsquedas repetitivas de archivos en el disco duro.

### 🤖 Entorno Android

* **Algoritmo de Descifrado de Backups:**
  * **Corrección Maestra de Longitud de Cabeceras:** Se corrigió el descifrado del Master Key Blob de los respaldos ADB. En lugar de asumir tamaños estáticos para el vector de inicialización (IV) y la clave AES, el descifrado ahora parsea dinámicamente los prefijos de longitud del blob para admitir de forma universal diferentes versiones de compilación de Android.
* **Inyección de Hallazgos en Carving:**
  * **Corrección en messages.bin:** Se restringió la inyección indiscriminada de registros binarios recuperados. Los elementos normales y activos de multimedia ya no se marcan como hallazgos forenses duplicados en la lista maestra a menos que estén explícitamente marcados como eliminados o efímeros en la base de datos.
* **Montaje Automatizado de Unidades Virtuales:**
  * **Colisiones de Firma en Windows:** Corrección en el script de PowerShell para el montaje de VHDs. Se añadió lógica robusta para forzar el estado "En Línea", remover protecciones contra escritura y asignar de manera dinámica la primera letra de unidad libre disponible en el sistema.
  * **Nombres de Archivo Seguros:** Forzado automático para que el archivo del VHD adopte el nombre exacto asignado al caso forense en su creación.
* **Filtro de Cronología:**
  * Se implementó un filtro estricto para incluir eventos en la línea de tiempo del reporte final únicamente si poseen un timestamp válido (`>0`), evitando la inclusión de registros corruptos o vacíos.
* **Soporte de Historias en Visor y Contenido Compartido:**
  * **Integración en Chats:** Se actualizó el visor de Android para extraer dinámicamente las historias correspondientes a los contactos alojadas en la sesión global `status@broadcast` de `msgstore.db`.
  * **Optimización y Indexado de Nube:** Se integró el indexado de la carpeta `Cloud_Media_Descargada` en el visor para la resolución rápida de adjuntos en la nube y se aplicó la optimización de caché de búsqueda en memoria para el módulo de Contenido Compartido, eliminando bloqueos de pantalla.
* **Smart Headers / Cabeceras Inteligentes (Ambas Plataformas):**
  * Se corrigió la visualización de datos "Desconocidos" en los encabezados de los reportes. Cuando el número de teléfono o nombre de perfil no se pueden extraer por completo debido a cifrados de extremo a extremo (E2EE) o selecciones parciales, el sistema autodefine etiquetas descriptivas contextuales como *"Todos los Chats (Multiobjetivo)"* o *"Objetivo: [Nombre del Chat]"*.

---

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
