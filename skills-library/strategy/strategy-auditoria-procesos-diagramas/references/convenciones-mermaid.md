# Sistema de colores y convenciones visuales

Todos los diagramas Mermaid deben seguir este sistema de forma estricta y consistente. **Ningún nodo puede quedar sin color asignado.**

## Paleta A — Diagramas de proceso actual (diagnóstico, Fase 1)

Transmite el estado real, incluyendo fricciones y problemas.

| Tipo de nodo | Color | Hex | Clase Mermaid |
|---|---|---|---|
| Inicio / Fin | Verde oscuro | `#1a7a4a` | `classDef inicio` |
| Acción manual (persona) | Azul medio | `#2d6a9f` | `classDef manual` |
| Acción de sistema (ya automatizada) | Gris azulado | `#6c7a8d` | `classDef sistema` |
| Decisión | Ámbar | `#e6a817` | `classDef decision` |
| Punto de fricción / ineficiencia | Rojo coral | `#c0392b` | `classDef friccion` |
| Espera / Delay externo | Naranja | `#e67e22` | `classDef espera` |
| Dato / Documento / Input | Lila | `#8e44ad` | `classDef dato` |

## Paleta B — Diagramas de proceso optimizado (propuesta, Fase 3)

Transmite modernidad, fluidez y automatización.

| Tipo de nodo | Color | Hex | Clase Mermaid |
|---|---|---|---|
| Inicio / Fin | Verde brillante | `#27ae60` | `classDef inicio` |
| Acción automatizada (N8N/Make/etc.) | Cian | `#0097a7` | `classDef automatizado` |
| Acción manual residual (requiere persona) | Azul | `#1565c0` | `classDef manual` |
| Decisión lógica / condición | Ámbar claro | `#f9a825` | `classDef decision` |
| Integración externa / API / Webhook | Verde lima | `#7cb342` | `classDef integracion` |
| Validación / Control de calidad automático | Turquesa | `#00796b` | `classDef validacion` |
| Error / Excepción / Fallback | Rojo | `#b71c1c` | `classDef error` |

## Implementación en Mermaid

Cada diagrama DEBE incluir:
1. Las definiciones de clases (`classDef`) al final del bloque
2. La asignación de clase a cada nodo con la sintaxis `:::nombreClase`
3. Un subgraph de leyenda al inicio del diagrama

**Regla crítica**: ningún nodo puede quedar sin clase asignada. Si un nodo no encaja claramente en ninguna categoría, usa `:::sistema` (Paleta A) o `:::automatizado` (Paleta B) como fallback. Revisa siempre antes de cerrar el bloque que todo nodo tiene su `:::clase`.

## Plantilla base — Fase 1 (Paleta A)

```
graph TD

%% ── LEYENDA ──────────────────────────────
subgraph LEYENDA
  direction LR
  L1([Inicio/Fin]):::inicio
  L2[Acción Manual]:::manual
  L3[Acción Sistema]:::sistema
  L4{Decisión}:::decision
  L5[⚠️ Fricción]:::friccion
  L6[⏳ Espera]:::espera
  L7[/Dato/]:::dato
end

%% ── FLUJO PRINCIPAL ──────────────────────
A([Inicio]):::inicio --> B[Paso 1]:::manual
B --> C{¿Condición?}:::decision
C -->|Sí| D[Paso 2]:::sistema
C -->|No| E[⚠️ Error manual]:::friccion
D --> F[⏳ Espera aprobación]:::espera
F --> G([Fin]):::inicio

%% ── ESTILOS ───────────────────────────────
classDef inicio fill:#1a7a4a,stroke:#145c38,color:#fff,font-weight:bold
classDef manual fill:#2d6a9f,stroke:#1f4e7a,color:#fff
classDef sistema fill:#6c7a8d,stroke:#4a5568,color:#fff
classDef decision fill:#e6a817,stroke:#c48a00,color:#000,font-weight:bold
classDef friccion fill:#c0392b,stroke:#922b21,color:#fff,font-weight:bold
classDef espera fill:#e67e22,stroke:#b05a0a,color:#fff
classDef dato fill:#8e44ad,stroke:#6c3483,color:#fff
```

## Plantilla base — Fase 3 (Paleta B)

```
graph TD

%% ── LEYENDA ──────────────────────────────
subgraph LEYENDA
  direction LR
  L1([Inicio/Fin]):::inicio
  L2[🤖 Automatizado]:::automatizado
  L3[👤 Manual residual]:::manual
  L4{Decisión lógica}:::decision
  L5[🔗 Integración]:::integracion
  L6[✅ Validación]:::validacion
  L7[❌ Error/Fallback]:::error
end

%% ── FLUJO PRINCIPAL ──────────────────────
A([Inicio]):::inicio --> B[🤖 Paso automatizado]:::automatizado
B --> C{¿Condición?}:::decision
C -->|Sí| D[🔗 Llamada API]:::integracion
C -->|No| E[❌ Fallback]:::error
D --> F[✅ Validación automática]:::validacion
F --> G([Fin]):::inicio

%% ── ESTILOS ───────────────────────────────
classDef inicio fill:#27ae60,stroke:#1e8449,color:#fff,font-weight:bold
classDef automatizado fill:#0097a7,stroke:#00717a,color:#fff
classDef manual fill:#1565c0,stroke:#0d47a1,color:#fff
classDef decision fill:#f9a825,stroke:#c17900,color:#000,font-weight:bold
classDef integracion fill:#7cb342,stroke:#558b2f,color:#fff
classDef validacion fill:#00796b,stroke:#004d40,color:#fff
classDef error fill:#b71c1c,stroke:#7f0000,color:#fff,font-weight:bold
```

## Especificaciones técnicas generales

- Sintaxis `graph TD` (Top-Down) o `graph LR` (Left-Right) según convenga al proceso
- Formas: `[]` procesos/acciones · `{}` decisiones · `([])` inicio/fin · `[/.../]` inputs/outputs (datos) · `[(...)]` bases de datos
- Flechas con etiquetas descriptivas cuando aporte: `-->|texto|`
- Diagramas claros y legibles — si un proceso es muy complejo, divídelo en subprocesos
- Máximo 15-18 nodos por diagrama; más allá de eso, crea subprocesos separados con su propia leyenda
