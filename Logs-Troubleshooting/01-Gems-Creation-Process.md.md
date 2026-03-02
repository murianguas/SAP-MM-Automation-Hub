# Configuración del Motor de Contexto: NotebookLM 

Este documento detalla la creación de la base de conocimientos que alimenta la lógica de nuestros Agentes IA, utilizando referencias de las empresas top del sector tecnológico.

## 1. Objetivo del Motor de Contexto
El objetivo es "anclar" (grounding) el conocimiento del Gem a fuentes de autoridad, evitando respuestas genéricas y asegurando que las automatizaciones de SAP y n8n sigan los estándares de la industria (Clean Core y Enterprise Automation).

## 2. Carga de Referencias Externas (Fuentes Top)
Se han seleccionado y cargado en NotebookLM los siguientes activos estratégicos:

### A. Ingeniería de Instrucciones (Prompt Engineering)
- **Google & Anthropic Best Practices**: Guías técnicas sobre estructuración de "System Prompts" y técnicas de *Chain-of-Thought* (Cadena de Pensamiento).
- **OpenAI Cookbook**: Patrones de diseño para la manipulación de JSON y manejo de errores en APIs.

### B. Estándares de Automatización Empresarial
- **Salesforce Agentforce Framework**: Referencias sobre cómo los agentes autónomos gestionan flujos de trabajo de principio a fin sin intervención humana.
- **n8n Documentation (Expert Level)**: Documentación técnica sobre nodos HTTP, expresiones en JavaScript y manejo de colas de datos.

### C. Estándares SAP MM (Clean Core)
- **SAP Press & Whitepapers**: Documentación sobre el modelo de datos de SAP S/4HANA para asegurar que el mapeo de tablas (MARA, EKKO) cumpla con las mejores prácticas de integración.

## 3. Proceso de Síntesis y Extracción
Para generar las instrucciones finales del Gem, se ejecutó el siguiente flujo en NotebookLM:

1. **Carga Estructurada**: Se subieron fuentes clave de Google, Anthropic y Salesforce para definir el "Cómo" debe pensar la IA.
2. **Generación de Directivas de Comportamiento**: Se utilizó la capacidad de razonamiento de NotebookLM para destilar una guía de estilo que prioriza el "Clean Core" y la eficiencia en n8n.
3. **Refinado de Instrucciones**: Se extrajeron los comandos y protocolos de respuesta que garantizan que el Gem actúe como un Arquitecto de Soluciones y no como un asistente básico.

## 4. Alimentación con Activos Oficiales de SAP (Academy Content)
Para asegurar el rigor funcional en el módulo MM, se ha integrado al Gem el conocimiento de los manuales oficiales de certificación de SAP S/4HANA. Esto permite que el agente comprenda la lógica de negocio real de un entorno SAP:

- **S4H400 (S/4HANA Business Processes in MM)**: Fundamentos de los procesos de aprovisionamiento y gestión de inventarios.
- **TS450 1 & 2 (Sourcing and Procurement)**: Configuración avanzada de compras, determinación de fuentes y condiciones de precio.
- **TS452 1 & 2 (Invoice Verification & Inventory Management)**: Lógica interna de la verificación de facturas y todos los movimientos de mercancías (Goods Movements).

## 5. Carga y Despliegue en el Gem (Final Setup)
El último paso de la infraestructura consistió en trasladar toda la inteligencia sintetizada al entorno de ejecución:

1. **Inyección del System Prompt**: Se pegaron las directivas de comportamiento refinadas en la configuración del Gem de Gemini.
2. **Vinculación de Recursos**: El Gem fue instruido para que, ante cualquier duda sobre un proceso de inventario (MI01) o de compras (ME21N), priorice la lógica descrita en los manuales **TS450/452**.
3. **Validación de Salida**: Se realizaron pruebas de estrés para confirmar que el Gem genera mapeos de tablas (EKKO, MSEG, MARA) alineados al 100% con el estándar de SAP S/4HANA.

## 6. Conclusión de Infraestructura
Con este proceso, el entorno de trabajo queda blindado. Tenemos:
- **Repositorio** limpio y sincronizado (GitHub).
- **Motor de Automatización** listo (n8n).
- **Consultor IA** alimentado con estándares de empresas Top y manuales oficiales de SAP.

