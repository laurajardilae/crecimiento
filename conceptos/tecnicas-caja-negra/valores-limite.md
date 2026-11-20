# Análisis de valores límite

## Idea

Los errores se concentran en los bordes de las clases: un `<` que debió ser `<=`, un rango que empieza en 1 y no en 0. Por eso se prueban los valores **justo en el límite y a un paso de cada lado**.

## Pasos

1. Tomar las clases definidas en la [partición de equivalencia](particion-equivalencia.md).
2. Identificar el límite inferior y superior de cada clase.
3. Probar el valor en el límite, uno por debajo y uno por encima.

## Ejemplo 1: abreviatura de montos en el inicio

El límite está en mil millones. Es el caso más interesante, porque justo ahí cambia el formato.

| Valor | Resultado esperado | Qué verifica |
|-------|--------------------|--------------|
| -1 | Error o no se muestra | Borde inferior inválido |
| 0 | `0` | Borde inferior válido |
| 999.999.999 | `999.999.999` | Último valor sin abreviar |
| 1.000.000.000 | `1.000M` | Primer valor abreviado |
| 1.000.000.001 | `1.000M` | Redondeo justo después del límite |
| 1.499.999.999 | `1.499M` o `1.500M` | Cómo se redondea la abreviatura |

Preguntas que surgen y conviene aclarar con la especificación: si se redondea o se trunca, y qué pasa con 999.999.999,50 si los montos tienen decimales.

## Ejemplo 2: rango de fechas de un reporte

Regla supuesta: la fecha inicial no puede ser posterior a la final y el rango máximo es de 31 días.

| Rango | Resultado esperado | Qué verifica |
|-------|--------------------|--------------|
| Inicio = fin (1 día) | Se genera | Rango mínimo |
| 31 días | Se genera | Último rango permitido |
| 32 días | Mensaje de validación | Primer rango excedido |
| Inicio un día después del fin | Mensaje de validación | Orden de fechas |
| Fin con fecha de mañana | Mensaje de validación | Fecha futura |
| Fin con fecha de hoy | Se genera | Último día permitido |

## Notas

- Es una forma de elegir mejores representantes, no una técnica separada de la partición. Se usan juntas.
- Con rangos de decimales o fechas, el "paso" es la mínima unidad posible (un centavo, un día).
