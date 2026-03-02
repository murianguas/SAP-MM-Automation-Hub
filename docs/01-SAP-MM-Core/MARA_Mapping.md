# SAP Object: MARA (General Material Data)
## Descripción
Mapeo de campos base para la automatización de creación y consulta de materiales en SAP MM.

## Campos Críticos
| Campo SAP | Descripción | Tipo |
| :--- | :--- | :--- |
| MATNR | Número de Material | CHAR18 |
| MTART | Tipo de Material | CHAR4 |
| MEINS | Unidad de Medida Base | UNIT3 |

## Lógica n8n
Este objeto será el nodo de entrada para validaciones de stock en el flujo de automatización.