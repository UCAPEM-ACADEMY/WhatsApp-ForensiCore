# Registro de Cambios (Changelog)

Todas las actualizaciones notables de WhatsApp ForensiCore se documentarán en este archivo. 
El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

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
