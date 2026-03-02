# Configuración del Entorno de Automatización (Stack)

## 1. Engine: n8n (Self-Hosted)
Instalación local para procesamiento de datos SAP sin latencia de nube externa.
- **Runtime**: Node.js v20+
- **Gestor de paquetes**: npm
- **Comando de ejecución**: `npx n8n start`
- **Acceso local**: `http://localhost:5678`

## 2. Brain: Obsidian (PKM)
Gestión de conocimiento funcional de SAP MM y lógica de integración.
- **Sincronización**: Git (Local-to-Cloud).
- **Formatos**: Markdown (UTF-8).

## 3. Bridge: GitHub Desktop
Control de versiones para el "CV Vivo".
- **Repositorio**: `SAP-MM-Automation-Hub` (Public).
- **Flujo**: `Commit` (Cambios locales) -> `Push` (Publicación Cloud).