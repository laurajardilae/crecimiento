# Transición de estado

## Idea

Cuando el comportamiento depende del **estado actual** y de los **eventos** que ocurren, se modela con estados, eventos y transiciones. Se prueba que cada transición válida funcione y que las inválidas se rechacen.

## Pasos

1. Identificar los estados y los eventos.
2. Dibujar o tabular qué evento lleva de qué estado a cuál.
3. Derivar casos: cada transición válida, y cada combinación estado-evento no permitida.
4. Opcional: recorridos completos de principio a fin.

## Ejemplo 1: ciclo de vida de un usuario en la gestión de usuarios

Regla supuesta: un usuario nuevo queda pendiente de activación. Para eliminarlo primero debe estar inactivo. Eliminado es un estado final.

| Estado actual | Evento | Estado siguiente |
|---------------|--------|------------------|
| Pendiente de activación | Activar | Activo |
| Activo | Desactivar | Inactivo |
| Inactivo | Reactivar | Activo |
| Inactivo | Eliminar | Eliminado |

Casos válidos: las 4 transiciones de la tabla, más el recorrido pendiente, activo, inactivo, activo, inactivo, eliminado.

Casos inválidos (se espera rechazo y que el estado no cambie):

| Estado actual | Evento | Resultado esperado |
|---------------|--------|--------------------|
| Pendiente de activación | Desactivar | Rechazado |
| Pendiente de activación | Eliminar | Rechazado |
| Activo | Activar o reactivar | Rechazado |
| Activo | Eliminar | Rechazado (primero se desactiva) |
| Inactivo | Desactivar | Rechazado |
| Eliminado | Cualquier evento | Rechazado |

También conviene probar qué pasa con una sesión abierta cuando un usuario activo pasa a inactivo: debería perder el acceso.

## Ejemplo 2: estado de una solicitud de reporte

Regla supuesta: un reporte solicitado pasa a en proceso, luego a generado o fallido. Desde fallido se puede reintentar. Solo un reporte generado se puede descargar.

| Estado actual | Evento | Estado siguiente |
|---------------|--------|------------------|
| Solicitado | Iniciar | En proceso |
| En proceso | Terminar con éxito | Generado |
| En proceso | Terminar con error | Fallido |
| Fallido | Reintentar | En proceso |
| Generado | Descargar | Generado |

Casos inválidos relevantes: descargar un reporte que está solicitado, en proceso o fallido, y reintentar uno ya generado.

## Ventajas y límites

- Muy útil para flujos con reglas de orden.
- Probar todas las combinaciones inválidas es exhaustivo. Si son muchas, se priorizan las de mayor riesgo.
