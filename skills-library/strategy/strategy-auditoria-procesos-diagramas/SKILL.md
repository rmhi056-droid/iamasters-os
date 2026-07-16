---
name: strategy-auditoria-procesos-diagramas
description: Analiza una transcripción de auditoría de procesos con un cliente, diagrama cada proceso actual en Mermaid.js marcando fricciones, hace preguntas estratégicas de profundización y propone versiones optimizadas/automatizadas con nuevos diagramas, matriz de priorización y resumen ejecutivo. Usar cuando Roberto tenga la transcripción de una reunión de auditoría de procesos de [cliente] y quiera diagramar los procesos actuales, detectar fricciones y proponer automatización.
---

# Auditoría de Procesos — Transcripción a Diagramas

Convierte una transcripción de auditoría de procesos en diagramas Mermaid.js del estado actual, preguntas estratégicas de profundización y una propuesta optimizada/automatizada con sus propios diagramas. Cubre el **"después"** de la reunión — para preparar la batería de preguntas **antes** de la reunión, usa primero `strategy-auditoria-procesos-automatizacion`.

## Cuándo se invoca

- Roberto pega o adjunta la transcripción de una reunión de auditoría de procesos con un cliente y pide diagramarla
- Roberto pide "diagrama los procesos de [cliente]" o "identifica fricciones y automatización en esta transcripción"
- Tras completar la Fase 2 de esta misma skill, Roberto responde a las preguntas estratégicas y toca generar la propuesta optimizada (Fase 3)

## Process

### Paso 1 · Fase 1 — Análisis y diagramación de procesos actuales

1. Lee la transcripción completa e identifica **todos** los procesos mencionados, no solo los principales
2. Para cada proceso, extrae: nombre, objetivo, pasos actuales, roles/personas involucradas, herramientas utilizadas, puntos de fricción o ineficiencias mencionados, tiempos aproximados si se mencionan
3. Crea un diagrama Mermaid.js por cada proceso usando la **Paleta A** (diagnóstico) — ver `references/convenciones-mermaid.md` para la paleta completa, las reglas de implementación y la plantilla de estructura base
4. Marca explícitamente con `:::friccion` y el prefijo ⚠️ todo paso que sea: manual pudiendo automatizarse, dependiente de una sola persona sin backup, propenso a error humano mencionado por el cliente, o causante de retrasos/cuellos de botella
5. Evalúa el nivel de madurez digital del cliente (🔴 Básico / 🟡 Intermedio / 🟢 Avanzado)
6. Presenta cada proceso y cierra con el bloque de Diagnóstico Inicial — formato exacto en `references/fase1-diagramas-actuales.md`

**Límite**: máximo 15-18 nodos por diagrama. Si un proceso es más complejo, divídelo en subprocesos con su propio diagrama y leyenda.

### Paso 2 · Fase 2 — Consultoría y profundización

Tras presentar **todos** los diagramas de Fase 1 y el Diagnóstico Inicial, adopta el rol de consultor y haz las preguntas estratégicas organizadas en 4 bloques (infraestructura tecnológica, volumen y operaciones, equipo y recursos, objetivos y restricciones) — plantilla completa en `references/fase2-preguntas-estrategicas.md`.

**La primera pregunta siempre debe ser** qué herramienta de automatización usa o planea usar el cliente (N8N, Make, Zapier, Power Automate, desarrollo a medida, etc.) — determina el diseño técnico de toda la propuesta.

Espera la respuesta de Roberto antes de continuar a la Fase 3.

### Paso 3 · Fase 3 — Propuesta de procesos optimizados

Con las respuestas de la Fase 2:

1. Integra la información con lo detectado en la transcripción
2. Diseña versiones optimizadas de cada proceso usando la **Paleta B** (ver `references/convenciones-mermaid.md`), maximizando automatización con la herramienta indicada por el cliente, eliminando pasos manuales redundantes, reduciendo tiempos de ciclo y errores
3. Presenta cada proceso optimizado — formato exacto (mejoras, % de automatización, herramientas, diagrama, beneficios, consideraciones, riesgos) en `references/fase3-propuesta-optimizada.md`
4. Añade la Matriz de Priorización (impacto × esfuerzo → orden sugerido)
5. Cierra con el Resumen Ejecutivo de la Propuesta

### Paso 4 · Cierre

- Antes de entregar el documento final al cliente, invoca `tool-output-verifier` (score-only)
- Si detectaste un patrón nuevo (sector no cubierto, tipo de fricción no prevista), anota en `context/learnings.md` bajo `## strategy-auditoria-procesos-diagramas`

## Reglas no negociables

**Siempre:**
- Diagrama TODOS los procesos mencionados en la transcripción, no solo los principales
- Asigna clase de color a absolutamente todos los nodos — ninguno sin `:::clase` (fallback: `:::sistema` en Paleta A, `:::automatizado` en Paleta B)
- Incluye la leyenda como subgraph en todos los diagramas
- Usa Paleta A en diagramas actuales y Paleta B en optimizados, sin mezclarlas
- Nombra herramientas reales que existen en el mercado
- Sé realista sobre qué puede automatizarse y qué requiere intervención humana

**Nunca:**
- Dejes un nodo sin clase de color
- Mezcles Paleta A y B en el mismo diagrama
- Inventes información que no esté en la transcripción o en las respuestas de Roberto
- Propongas soluciones genéricas sin personalizar al cliente
- Ignores restricciones que el cliente haya mencionado
- Crees diagramas de más de 18 nodos (usa subprocesos)
- Asumas presupuesto sin haberlo preguntado

## Orden de la respuesta

1. Lista de procesos identificados (resumen ejecutivo inicial)
2. Fase 1: diagramas de todos los procesos actuales (Paleta A) + Diagnóstico Inicial
3. Fase 2: preguntas estratégicas por bloques
4. *(esperar respuesta de Roberto)*
5. Fase 3: propuestas optimizadas (Paleta B) + Matriz de Priorización
6. Resumen ejecutivo final

## Outputs

- Documento con diagramas Mermaid.js (actuales + optimizados), diagnóstico inicial, preguntas estratégicas y propuesta final, en `clients/<cliente>/projects/<fecha>-auditoria-procesos-diagramas/` o `projects/briefs/<fecha>-auditoria-diagramas-<empresa>/` si es prospecto

## Skills que llama

- **`strategy-auditoria-procesos-automatizacion`** — si aún no se ha preparado la batería de preguntas antes de la reunión con el cliente, usar esa skill primero
- **`tool-output-verifier`** — gate de calidad antes de entregar el documento final

## Edge cases

- **Transcripción incompleta o con audio cortado** → señala qué procesos quedaron con información incompleta en vez de inventar pasos
- **Cliente no ha dicho qué herramienta de automatización usa** → esa es la primera pregunta obligatoria de la Fase 2, no asumas N8N/Make por defecto
- **Proceso con más de 18 nodos** → divide en subprocesos, cada uno con su propio diagrama y leyenda

## Examples

Ver `references/examples.md` para un ejemplo completo del ciclo (Fase 1 → 2 → 3).
