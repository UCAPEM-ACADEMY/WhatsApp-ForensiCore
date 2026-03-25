# Registro de Cambios (Changelog)

Todas las actualizaciones notables de WhatsApp ForensiCore se documentarán en este archivo. 
El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

## [3.0.0] - 2026-03-21
### Añadido (Added)
- **APK Downgrade Automatizado:** Bypass del Sandbox en Android 12+ para extracción ADB.
- **Extracción E2EE:** Captura nativa de copias de seguridad cifradas de extremo a extremo.
- **Aislamiento VHD:** La evidencia se guarda en discos virtuales cifrados (`Datos.vhd`) para prevenir contaminación.
- **IA Forense Offline:** Transcripción de audios con `faster-whisper` y extracción de fotogramas clave con `cv2`.

### Cambiado (Changed)
- Orquestación de reportes mejorada: PDF dinámico para mensajes extensos y nuevo Visor HTML interactivo.

### Solucionado (Fixed)
- Detección mejorada de perfiles de trabajo y aplicaciones clonadas mediante comandos ADB.

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
