---
name: strategy-diagnostico-transformacion-digital
description: Guía una sesión de diagnóstico de madurez digital de 2h con un cliente (cuestionario de 24 preguntas en 6 dimensiones), calcula el índice de madurez digital y genera el informe final en Word listo para entregar. Usar cuando Roberto diga "vamos a hacer el diagnóstico de madurez digital de [cliente]", "diagnóstico de transformación digital", "sesión de diagnóstico con [cliente]", "calcula el índice de madurez" o "genera el informe de diagnóstico digital".
---

# Diagnóstico de Transformación Digital

Herramienta de diagnóstico de madurez digital para clientes. Cada sesión (conversación) corresponde a un cliente distinto — no mezclar contextos entre sesiones. Objetivo: guiar la sesión de diagnóstico de 2h, calcular el índice de madurez digital y generar el informe completo listo para entregar.

## Cuándo se invoca

- Roberto dice el nombre del cliente y sector para arrancar una sesión de diagnóstico
- Roberto pide calcular el índice de madurez digital de un cliente
- Roberto dice "generar informe" tras completar (o interrumpir) el cuestionario
- Roberto pide retomar un diagnóstico pausado

## Process

### Paso 1 · Arranque

Cuando Roberto dé el nombre del cliente y sector:

1. Confirma en una frase que entiendes el cliente y su sector
2. Pregunta si quiere el cuestionario **guiado** (pregunta a pregunta) o **libre** (él dicta respuestas y tú anotas)
3. Espera su elección antes de continuar — no arranques el cuestionario sin confirmación

### Paso 2 · Durante la sesión

- **Modo guiado**: lanza las 24 preguntas de una en una (ver `references/preguntas-dimensiones.md`), espera la puntuación (1-5), anota y pasa a la siguiente
- **Modo libre**: Roberto dicta respuestas, registra en silencio hasta que diga "terminar"
- En cualquier momento Roberto puede decir "pausa" para salir del flujo sin perder lo anotado
- Si una puntuación no está clara, pregunta **una sola vez** para aclarar
- **Las puntuaciones las da Roberto o el cliente en la sesión — nunca las infieras ni las propongas sin datos**

### Paso 3 · Cálculo del índice

Al completar las 24 preguntas (ver fórmulas y tabla de clasificación en `references/preguntas-dimensiones.md`):

1. Calcula la media de cada una de las 6 dimensiones
2. Calcula el índice global (media de las 6 dimensiones)
3. Clasifica según la tabla: Incipiente / Básico / Medio / Avanzado
4. Muestra la tabla resumen (dimensión → puntuación → clasificación) antes de generar el informe

### Paso 4 · Generación del informe

Se dispara cuando Roberto dice "generar informe" o al terminar el cuestionario:

1. Pregunta: nombre legal de la empresa, sector, número de empleados, nombre del interlocutor
2. Genera el informe completo en Word (.docx) siguiendo la estructura de `references/estructura-informe.md` (7 secciones)
3. Si el cliente tiene características especiales (familiar, industrial, servicios...), adapta el análisis y las iniciativas propuestas a ese contexto
4. El informe debe poder entregarse directamente al cliente sin edición previa — ejecutivo, legible en 10 minutos por un director general
5. Firma siempre como: **Roberto Hernández · Consultor de Gestión Empresarial · CMC® · CCA® · Auditor ISO 9001**

### Paso 5 · Cierre

- Antes de entregar el .docx, invoca `tool-output-verifier` (score-only) como gate de calidad de entregable a cliente
- Si la sesión reveló un patrón nuevo (pregunta que no encajaba, cliente atípico), anota en `context/learnings.md` bajo `## strategy-diagnostico-transformacion-digital`

## Outputs

- Informe `.docx` completo, listo para entregar, en `clients/<cliente>/projects/<fecha>-diagnostico-madurez-digital/` si es cliente existente, o en `projects/briefs/<fecha>-diagnostico-<empresa>/` si es prospecto sin carpeta de cliente propia
- Tabla resumen del índice de madurez (en el chat, antes del informe)

## Skills que llama

- **`docx`** (plugin anthropic-skills) — para generar el informe final en formato Word
- **`tool-output-verifier`** — gate de calidad antes de entregar el informe al cliente

## Edge cases

- **Cliente atípico** (familiar, industrial, servicios...) → adapta iniciativas y lenguaje, no uses el mismo análisis genérico
- **Puntuación ambigua** → pregunta una sola vez; si sigue sin estar clara, anota como pendiente y sigue (no bloquees la sesión)
- **Roberto dice "pausa"** → sal del flujo inmediatamente, conserva todas las puntuaciones anotadas hasta ese punto
- **Dudas de Roberto durante la sesión** → respóndelas sin salir del flujo del cuestionario

## Examples

Ver `references/examples.md` para 2 ejemplos completos (modo guiado y modo libre).
