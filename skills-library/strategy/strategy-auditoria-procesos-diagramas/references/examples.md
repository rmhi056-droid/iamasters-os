# Ejemplo — ciclo completo

Roberto pega la transcripción de la reunión de auditoría con "Distribuidora Ejemplo SL" (sector alimentación).

1. **Fase 1**: identificas 4 procesos (gestión de pedidos, control de stock, facturación, atención postventa). Para cada uno generas el diagrama Mermaid Paleta A con su leyenda, marcando con `:::friccion` ⚠️ los pasos manuales dependientes de una sola persona (p.ej. "el pedido se valida por WhatsApp con el jefe de almacén"). Cierras con el Diagnóstico Inicial: 4 procesos, madurez 🟡 Intermedio, top 3 fricciones (validación manual de pedidos, doble tecleo en facturación, ausencia de alertas de stock).

2. **Fase 2**: preguntas por bloques. Primera pregunta obligatoria: "¿Qué herramienta de automatización usan o planean usar?" Roberto (o el cliente en la transcripción) responde N8N, ERP Gespymes sin API abierta documentada, 50 pedidos/día, presupuesto medio, prioridad en gestión de pedidos.

3. **Fase 3** (tras la respuesta): rediseñas el proceso de gestión de pedidos con Paleta B — automatización vía N8N con webhook desde el formulario de pedidos, validación automática de stock, notificación a almacén solo si hay excepción. Nivel de automatización pasa de 20% a 75%. Repites para los otros 3 procesos, añades la Matriz de Priorización (gestión de pedidos = 🔴 Urgente por alto impacto/bajo esfuerzo) y cierras con el Resumen Ejecutivo.
