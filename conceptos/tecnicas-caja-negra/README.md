# Técnicas de generación de casos de prueba: caja negra

- **Área:** Pruebas de software (QA)
- **Estado:** repasado
- **Fecha de cierre:** 2025-10-31

## Qué es

Las técnicas de caja negra obtienen los casos de prueba a partir de la **especificación** (qué debe hacer el sistema), sin mirar el código interno. Permiten cubrir muchos escenarios con pocos casos bien elegidos.

## Contexto de los ejemplos

Los ejemplos se basan en un portal web de consulta de transacciones realizadas en datáfonos. El portal tiene:

- **Inicio:** gráficos con totales de cantidad y de valor de las transacciones, comercios con más ventas y franquicias con más ventas. Los montos desde mil millones se abrevian, por ejemplo `1.000M`.
- **Detalle de transacciones:** listado con filtros.
- **Reportes:** generación por tipo de transacción, número de documento del comercio y fecha.
- **Gestión de usuarios:** administración de permisos con dos roles, administrador y consultor.

Las reglas concretas de cada ejemplo (límites, rangos, estados) son supuestos para practicar la técnica y no describen reglas reales de ningún sistema.

## Técnicas

| Técnica | Cuándo usarla | Detalle y ejemplo |
|---------|---------------|-------------------|
| Partición de equivalencia | Entradas con rangos o categorías | [Ver](particion-equivalencia.md) |
| Análisis de valores límite | Complementa a la partición, en los bordes de cada rango | [Ver](valores-limite.md) |
| Tabla de decisión | Reglas de negocio con varias condiciones combinadas | [Ver](tabla-decision.md) |
| Transición de estado | Algo con ciclo de vida: pedido, sesión, ticket | [Ver](transicion-estado.md) |

## Cómo elegir

1. ¿El campo tiene rangos o grupos de valores? Partición de equivalencia y valores límite.
2. ¿El resultado depende de varias condiciones a la vez? Tabla de decisión.
3. ¿El comportamiento depende de lo que ya pasó antes? Transición de estado.

Es habitual combinarlas. Por ejemplo, partición y valores límite para validar cada campo de un formulario, y tabla de decisión para las reglas que los relacionan.

## Errores comunes

- Probar solo valores válidos y olvidar las clases inválidas (negativos, vacíos, texto donde va un número, un documento con letras).
- Elegir un valor cualquiera de la clase y no los bordes.
- Armar la tabla de decisión sin revisar combinaciones imposibles o contradictorias.
- Probar solo transiciones válidas y no verificar que las inválidas se rechacen.

## Explicado en pocas palabras

Caja negra es probar lo que el sistema promete, no cómo lo hace. Se eligen pocos casos, pero con criterio: uno por cada grupo de comportamiento y los bordes entre grupos.

## Dudas abiertas

- ¿Cómo combinar estas técnicas con las de caja blanca para medir cobertura?

## Referencias

- ISTQB, *Certified Tester Foundation Level Syllabus*, capítulo de técnicas de prueba.
