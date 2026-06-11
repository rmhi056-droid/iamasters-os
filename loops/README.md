# Loops del operador

Esta carpeta guarda los loops recurrentes que diseñas con la skill
`automation-loop-engine`.

Un **loop** es un sistema de trabajo repetible: tiene una cola de entrada, estaciones de
ejecución, verificación automática, compuertas humanas, estado persistente y aprendizaje.

La idea es dejar de repetir una tarea a mano y convertirla en una línea de producción que
puede procesar muchos items con el mismo criterio.

## Estructura de cada loop

Cada loop vive en su propia carpeta:

```text
loops/<nombre-kebab>/
├── loop-spec.md
├── REGLAS.md
└── loop-state.md
```

`loop-spec.md` es la fuente de verdad. Define el objetivo, disparador, cola, estaciones,
operarios, verificación, compuertas humanas, condiciones de parada, métricas y aprendizaje.

`REGLAS.md` guarda el aprendizaje validado. Cada corrección repetida del usuario se convierte
en una regla numerada que se aplica a items futuros.

`loop-state.md` guarda el estado operativo: items pendientes, procesados, escalados, métricas
del último lote y notas volátiles. Puede cambiar mucho y no debe considerarse documentación fija.

## Índice central

`loops/_index.md` es el registro central de loops. Lo crea la skill en el primer uso real.

Debe listar cada loop con:

- nombre
- objetivo
- disparador
- nivel A actual
- fecha de creación
- última revisión

También puede incluir candidatos detectados por el radar que todavía no se han diseñado.

## Plantillas

`loops/_templates/` queda reservado para plantillas de loops comunes.

Antes de diseñar un loop desde cero, la skill debe mirar si existe una plantilla parecida.

En esta fase la carpeta puede estar vacía: `.gitkeep` solo mantiene la estructura en Git.

## Privacidad

El contenido real de `loops/` es **privado del operador**.

Puede contener procesos internos, criterios comerciales, reglas aprendidas, clientes,
colas de trabajo o métricas sensibles.

Por eso está ignorado por Git. Solo se versionan este `README.md` y la carpeta `_templates/`.
