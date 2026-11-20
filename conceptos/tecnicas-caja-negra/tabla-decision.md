# Tabla de decisión

## Idea

Cuando el resultado depende de **varias condiciones combinadas**, se listan todas las combinaciones relevantes en una tabla. Cada columna (regla) se convierte en un caso de prueba.

## Pasos

1. Listar las condiciones y las acciones o resultados posibles.
2. Calcular las combinaciones (con 2 condiciones de sí/no hay 4, con 3 hay 8).
3. Completar el resultado de cada combinación según la especificación.
4. Descartar las imposibles y unir las que den el mismo resultado sin importar una condición.
5. Escribir un caso de prueba por regla.

## Ejemplo 1: generación de un reporte

Regla supuesta: para generar un reporte hace falta un tipo de transacción, un documento de comercio válido y un rango de fechas válido. El sistema indica qué falló.

| Condición / Regla | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|-------------------|----|----|----|----|----|----|----|----|
| Tipo de transacción seleccionado | Sí | Sí | Sí | Sí | No | No | No | No |
| Documento del comercio válido | Sí | Sí | No | No | Sí | Sí | No | No |
| Rango de fechas válido | Sí | No | Sí | No | Sí | No | Sí | No |
| **Resultado** | Genera el reporte | Error en fechas | Error en documento | Errores en documento y fechas | Error en tipo | Errores en tipo y fechas | Errores en tipo y documento | Errores en los tres |

Cada columna es un caso de prueba. R1 es el camino feliz y las demás verifican que el mensaje de error corresponda exactamente a lo que falla.

## Ejemplo 2: permisos por rol

Regla supuesta: el consultor puede ver y consultar, pero solo el administrador gestiona usuarios.

| Acción | Administrador | Consultor |
|--------|---------------|-----------|
| Ver el inicio con gráficos | Permitido | Permitido |
| Consultar y filtrar el detalle de transacciones | Permitido | Permitido |
| Generar reportes | Permitido | Permitido |
| Ver el módulo de gestión de usuarios | Permitido | No permitido |
| Crear, editar o desactivar usuarios | Permitido | No permitido |
| Cambiar el rol de un usuario | Permitido | No permitido |

Cada celda es un caso. Además de verificar que el menú no muestre la opción al consultor, hay que probar el acceso directo por la dirección del módulo, que también debe rechazarse.

## Ventajas y límites

- Obliga a revisar combinaciones que se suelen olvidar.
- Con muchas condiciones la tabla crece rápido (2 elevado al número de condiciones). Ahí conviene simplificar uniendo reglas.
