# Workflow: Limpieza de Gmail (JobLeads)

## 1. Lógica de Negocio

**Problema:** Saturación de la bandeja de entrada por alertas diarias de `mailer@jobleads.com`.

**Solución:** Automatizar la detección y traslado a la papelera (Trash) para lograr _Inbox Zero_.

---

## 2. Arquitectura del Flujo

El flujo se compone de tres etapas críticas ejecutadas en n8n:

1. **Extracción:** Captura de los últimos 50 mensajes vía API de Gmail.
    
2. **Filtrado:** Nodo _Filter_ configurado para aislar el remitente específico.
    
3. **Acción:** Operación `Trash` sobre el `threadId` para eliminar el hilo completo.
    

---

## 3. Configuración Técnica

### Nodo Filter

- **Campo:** `{{ $json.from }}`
    
- **Operador:** `Contains`
    
- **Valor:** `mailer@jobleads.com`
    

### Nodo Gmail (Acción)

- **Resource:** `Thread`
    
- **Operation:** `Trash`
    
- **ID:** `{{ $json.threadId }}`
    
![[Pasted image 20260302121223.png]]
---


---


## 4. Blueprint (Recuperación JSON)


```
{
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "e755fbbd-25e1-4bde-85c8-6a463e404508",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "operation": "getAll",
        "filters": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        208,
        0
      ],
      "id": "6d041382-c6fe-49ac-bc9c-a74349e30e05",
      "name": "Get many messages",
      "webhookId": "31430aad-ebc4-4914-a750-81a345d5fe2f",
      "credentials": {
        "gmailOAuth2": {
          "id": "R23jheU6U2R3uqoE",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 3
          },
          "conditions": [
            {
              "id": "9327873e-c312-4d3b-87b8-104a7514a7d6",
              "leftValue": "={{ $json.From }}",
              "rightValue": "mailer@jobleads.com",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.filter",
      "typeVersion": 2.3,
      "position": [
        416,
        0
      ],
      "id": "d2b28ae2-9641-41c6-8e48-966f058607d2",
      "name": "Filter"
    },
    {
      "parameters": {
        "content": "Lógica de Limpieza v1.0\n\n    Filtro por remitente específico: mailer@jobleads.com.\n\n    Acción: Pendiente de conectar nodo de borrado.\n    Objetivo: Mantener el Inbox limpio de alertas de empleo masivas."
      },
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        624,
        0
      ],
      "id": "655e84ce-923e-4b01-ba00-c00dd0ca66f0",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "resource": "thread",
        "operation": "trash",
        "threadId": "={{ $json.threadId }}"
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        624,
        0
      ],
      "id": "1e81e8ed-52dc-4e35-93d9-a64594a3852f",
      "name": "Trash a thread",
      "webhookId": "e773646d-e77d-498a-a8fa-1523c7a4dd53",
      "credentials": {
        "gmailOAuth2": {
          "id": "R23jheU6U2R3uqoE",
          "name": "Gmail account"
        }
      }
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Get many messages",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get many messages": {
      "main": [
        [
          {
            "node": "Filter",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Filter": {
      "main": [
        [
          {
            "node": "Trash a thread",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "pinData": {},
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "047be74f5432f53708d94b0250f7ff3a049b6c26cd46c970d342f91e30744bcc"
  }
}
```