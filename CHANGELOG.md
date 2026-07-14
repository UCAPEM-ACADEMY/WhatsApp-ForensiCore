# Registro de Cambios (Changelog)

Todas las actualizaciones notables de WhatsApp ForensiCore se documentarán en este archivo. 
El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

## [3.2.0] - 2026-07-14
## 🚀 Nuevos Módulos

### 1. Visor Forense de Mensajería (Chat & Contacts Viewer)
* **Visualización Dinámica e Intuitiva:** Implementación de una interfaz gráfica moderna que imita el diseño de un cliente de mensajería (panel izquierdo para chats y contactos, panel derecho para la cronología de mensajes) facilitando la lectura fluida por parte del perito.
* **Procesamiento de Base de Datos Nativo:** Lectura e interpretación directa de contenedores de  WhatsApp, incluyendo `msgstore.db`, en conjunto con sus archivos de registro transaccional (`.wal` y `.shm`).
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

## 🔧 Actualizaciones y Correcciones Críticas

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

## [3.1.2] - 2026-04-04
### Solucionado (Fixed)
- **Filtro de Evidencia Estricto:** Se corrigió una vulnerabilidad lógica que inyectaba incondicionalmente mensajes vivos en los reportes finales. Ahora, el sistema evalúa estrictamente la bandera, garantizando que el PDF y el JSON solo contengan evidencia eliminada, editada, efímera o geolocalizaciones.
- **Purga Binaria en RAM (Deduplicación por Índices):** Se implementó un motor avanzado para el Carving de Páginas Libres y WAL. El script ahora extrae todos los key_id vivos de la base de datos y los utiliza como "lista negra" para aniquilar los falsos positivos a nivel hexadecimal antes de la lectura en crudo.
- **Corrección de Multimedia Activa:** Las fotografías y videos vivos ya no se catalogan erróneamente como evidencia recuperada, limpiando drásticamente el ruido en el reporte final.
- **Selector Explícito de Versión:** Se eliminó la selección automática de paquetes que causaba colapsos en dispositivos con Dual Messenger. Se implementó un menú desplegable (Combobox) para que el perito elija explícitamente entre WhatsApp Normal (com.whatsapp) y WhatsApp Business (com.whatsapp.w4b).
- **Limpieza Preventiva ADB:** Se añadieron comandos de limpieza en el directorio /data/local/tmp/ del dispositivo móvil antes de cada extracción para evitar la contaminación cruzada de bases de datos de extracciones previas fallidas.
- **Detector de Errores Silenciosos:** Se integró un sistema de alertas (messagebox) que avisa al perito si los módulos secundarios no se encuentran en la ruta esperada, evitando cierres inesperados de la aplicación.

---

## [3.1.1] - 2026-03-25
### Añadido (Added)
- **Módulo de Deep Carving:** Motor avanzado de búsqueda en espacio no asignado (Free-Pages) y memoria transaccional (WAL) para rescate binario de textos e imágenes RAW.
- **Recuperación Efímera Optimizada:** Extracción de rastros y metadatos de mensajes "Ver una vez" a partir de llaves criptográficas huérfanas.
- **Filtro Forense Anti-Ruido Máximo:** Nuevo motor heurístico que detecta y destruye código residual SQLite, índices FTS, JSON, vCards y enlaces de enrutamiento de Meta.

### Cambiado (Changed)
- **Optimización de carga en Reportes PDF:** Truncamiento inteligente de fragmentos de texto excesivamente largos con advertencias visuales y derivación al archivo CSV.
- **Manejo visual de excepciones multimedia:** Inyección de íconos forenses de advertencia en HTML y PDF cuando la imagen RAW rescatada está corrupta o no se localiza físicamente.
- **Distribución en Parche (Patch Update):** Nueva modalidad de actualización ligera vía instalador específico que actualiza scripts clave sin eliminar la versión base (3.0.0) ni afectar la licencia del usuario.

### Solucionado (Fixed)
- Colapso crítico (AttributeError: 'NoneType') que interrumpía la generación del Visor HTML Interactivo al procesar bases de datos con campos estructurales nulos o severamente corruptos.
_ Filtración de falsos positivos y "basura" de sistema (Triggers SQL, hashes largos y variables de interfaz) hacia la tabla de textos huérfanos en la consolidación de evidencia.

---

## [3.0.0] - 2026-03-21
### Añadido (Added)
- **APK Downgrade Automatizado:** Bypass del Sandbox en Android 12+ para extracción ADB.
- **Extracción E2EE:** Captura nativa de copias de seguridad cifradas de extremo a extremo.
- **Aislamiento VHD:** La evidencia se guarda en discos virtuales cifrados (`Datos.vhd`) para prevenir contaminación.
- **IA Forense Offline:** Transcripción de audios con `faster-whisper` y extracción de fotogramas clave con `cv2`.

### Cambiado (Changed)
- **Orquestación de reportes mejorada:** PDF dinámico para mensajes extensos y nuevo Visor HTML interactivo.

### Solucionado (Fixed)
- Detección mejorada de perfiles de trabajo y aplicaciones clonadas mediante comandos ADB.
- Otras correcciónes menores.

---

## [2.0.0] - [Fecha de tu versión 2]
### Añadido (Added)
- Interfaz gráfica moderna utilizando CustomTkinter.
- Soporte para exportación básica en formato PDF y JSON.

### Solucionado (Fixed)
- Corrección en el parseo de bases de datos corruptas de WhatsApp (`msgstore.db`).

---

## [1.0.2] - [Fecha de tu versión 1]
### Añadido (Added)
- Lanzamiento inicial de la herramienta de extracción de bases de datos de WhatsApp.
