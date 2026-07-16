---
name: strategy-auditoria-procesos-automatizacion
description: Genera una batería de 80-120 preguntas personalizadas para preparar una auditoría o consultoría de automatización con IA en una empresa cliente, tras recopilar contexto conversacionalmente en 5 bloques. Usar cuando Roberto diga "prepárame la auditoría de procesos de [cliente]", "necesito la batería de preguntas para la reunión con [cliente]", "vamos a preparar la consultoría de automatización de [cliente]" o quiera preparar una primera reunión de diagnóstico de automatización.
---

# Auditoría de Procesos — Preparación

Genera baterías de preguntas estratégicas para preparar auditorías/consultorías de automatización con IA, a partir del contexto de una empresa concreta. Proceso conversacional en 3 fases: recopilar contexto, confirmar, generar el documento.

## Cuándo se invoca

- Roberto va a tener una reunión de auditoría/consultoría de automatización con un cliente y necesita preparar las preguntas
- Roberto pide "la batería de preguntas para [cliente]"
- Roberto quiere preparar una primera reunión exploratoria de automatización

## Process

### Paso 1 · Recopilar contexto

Haz las preguntas de forma **conversacional y progresiva**, en los 5 bloques de `references/bloques-recopilacion.md` (3-4 preguntas por bloque) — **nunca las 17 de golpe**. Tras cada respuesta de Roberto, puedes hacer preguntas de seguimiento específicas según lo que comparta.

### Paso 2 · Análisis y confirmación

Una vez recopilado el contexto:

1. Resume en un párrafo breve el contexto completo entendido
2. Identifica los 3-4 focos principales donde probablemente existan oportunidades de automatización
3. Pregunta a Roberto si quiere añadir o corregir algo antes de generar la batería

**No generes el documento sin pasar por esta confirmación.**

### Paso 3 · Generar la batería de preguntas

Genera el documento completo en markdown siguiendo la estructura de 12 secciones de `references/estructura-documento.md`, aplicando las directrices de calidad de `references/directrices-preguntas.md`.

Requisitos no negociables:
- Mínimo 80-120 preguntas en total, distribuidas estratégicamente
- 2500-4000 palabras
- Personalizado al sector, tamaño, madurez digital, área de foco, presupuesto y urgencia del cliente — nunca preguntas genéricas aplicables a cualquier empresa
- Incluye siempre la sección de señales de alerta y oportunidad, y el framework de priorización
- No enumeres áreas/departamentos que no sean relevantes para el contexto específico

### Paso 4 · Cierre

- Si el documento es para entregar o usar en reunión con cliente, invoca `tool-output-verifier` (score-only) antes de darlo por cerrado
- Si el patrón de preguntas reveló algo nuevo (sector no cubierto, señal de alerta no prevista), anota en `context/learnings.md` bajo `## strategy-auditoria-procesos-automatizacion`

## Outputs

- Documento markdown (`BATERÍA DE PREGUNTAS PARA AUDITORÍA DE AUTOMATIZACIÓN`) en `clients/<cliente>/projects/<fecha>-auditoria-automatizacion/` si es cliente existente, o `projects/briefs/<fecha>-auditoria-<empresa>/` si es prospecto

## Skills que llama

- **`tool-output-verifier`** — gate de calidad si el documento se usa cara a cara con el cliente

## Edge cases

- **Roberto no sabe algún dato del bloque de recopilación** (p.ej. presupuesto) → anótalo como "por confirmar en reunión" y sigue, no bloquees el proceso
- **Cliente con múltiples áreas de interés** → cubre mínimo 3, máximo 6 áreas; prioriza las que Roberto marcó como foco
- **Reunión ya en curso / sin tiempo para las 5 fases completas** → puedes comprimir el Paso 1 a los bloques imprescindibles (empresa + objetivos/pain points) si Roberto lo pide explícitamente, pero avisa que la batería será menos personalizada

## Examples

Ver `references/examples.md` para 2 ejemplos completos.
