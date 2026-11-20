# Partición de equivalencia

## Idea

Se divide el conjunto de entradas posibles en grupos (clases) donde se espera que el sistema se comporte igual. Si un valor de la clase funciona, se asume que los demás también. Por eso basta probar **un representante por clase**, tanto de las clases válidas como de las inválidas.

## Pasos

1. Leer la especificación e identificar las entradas.
2. Dividir cada entrada en clases válidas e inválidas.
3. Elegir un valor representativo por clase.
4. Definir el resultado esperado de cada uno.

## Ejemplo 1: formato de los montos en los gráficos del inicio

Regla supuesta: los montos menores a 1.000.000.000 se muestran completos con separador de miles. Desde 1.000.000.000 se abrevian en millones con la letra M (por ejemplo, 1.000M).

| Clase | Tipo | Representante | Resultado esperado |
|-------|------|---------------|--------------------|
| Cero | Válida | 0 | `0` |
| Menor a mil millones | Válida | 45.350.000 | `45.350.000` |
| Mil millones o más | Válida | 2.500.000.000 | `2.500M` |
| Negativo | Inválida | -1.000 | No se muestra o se trata como error |
| No numérico | Inválida | "abc" | No se muestra o se trata como error |
| Vacío o nulo | Inválida | (sin valor) | Se muestra `0` o un guion, según se defina |

## Ejemplo 2: filtro por número de documento del comercio

Regla supuesta: el documento tiene solo dígitos y de 6 a 12 caracteres.

| Clase | Tipo | Representante | Resultado esperado |
|-------|------|---------------|--------------------|
| De 6 a 12 dígitos | Válida | 900123456 | Se aplica el filtro |
| Menos de 6 dígitos | Inválida | 123 | Mensaje de validación |
| Más de 12 dígitos | Inválida | 12345678901234 | Mensaje de validación |
| Con letras o símbolos | Inválida | 9001A3-56 | Mensaje de validación |
| Vacío | Válida | (sin valor) | Se muestran todos los comercios |

## Ventajas y límites

- Reduce mucho la cantidad de casos sin perder variedad de escenarios.
- No detecta fallos en los bordes. Para eso se complementa con [valores límite](valores-limite.md).
