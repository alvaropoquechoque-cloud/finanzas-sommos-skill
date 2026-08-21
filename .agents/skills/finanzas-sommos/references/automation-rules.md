# Reglas de automatización

## Categorización

Principio:
- buscar reglas activas cuya palabra clave esté contenida en la descripción;
- respetar tipo cuando la regla lo requiera;
- si no hay coincidencia inequívoca: `Por categorizar`.

Ejemplo:
- Descripción: `Google Cloud`
- Resultado esperado: `Platform cost`

## Tipo de cambio

### USD
`TC = 1`

### SOL
`TC = 0.28`

Convención: el TC representa USD por cada unidad de SOL, por lo que:
`Monto USD = Monto SOL × 0.28`

### BOB
Usar TCO oficial BCB correspondiente a la fecha.

Si no existe publicación para ese día:
- usar el último TCO oficial con fecha <= fecha de la transacción;
- no usar una cotización futura;
- no inventar un TC.

Conversión:
`Monto USD = Monto BOB / TCO`

### Otras monedas
Usar `TC manual (otras)` según la convención definida por la hoja. Si la convención no está clara, preguntar o inspeccionar ejemplos existentes antes de calcular.

## Estados y CxC/CxP

| Tipo | Estado | Resultado |
|---|---|---|
| Ingreso | Pendiente | CxC |
| Egreso | Pendiente | CxP |
| Ingreso | Pagado/Cobrado | Movimiento realizado; no CxC |
| Egreso | Pagado/Cobrado | Movimiento realizado; no CxP |

## Presupuesto

Ejecutado:
- Egreso
- Pagado/Cobrado
- mes correspondiente
- categoría correspondiente

Comprometido:
- Egreso
- Pendiente
- mes de vencimiento o criterio operativo vigente
- categoría correspondiente

Disponible:
`Presupuesto - Ejecutado - Comprometido`

## Bancos

Ingresos mes:
- Banco coincide
- Moneda coincide
- Fecha pertenece al mes
- Tipo = Ingreso
- Estado = Pagado/Cobrado

Egresos mes:
- Banco coincide
- Moneda coincide
- Fecha pertenece al mes
- Tipo = Egreso
- Estado = Pagado/Cobrado

Saldo calculado:
`Saldo inicial + Ingresos mes - Egresos mes`

Diferencia:
`Saldo final banco real - Saldo calculado`

Conciliación:
- sin saldo final real: `Pendiente cierre`
- diferencia dentro de tolerancia: `Conciliado`
- diferencia fuera de tolerancia: `Revisar`

## Dashboard

Cash:
- usar último mes con cierre bancario real completo;
- sumar solo saldos finales USD de ese mes;
- nunca sumar todos los meses históricos.

Ingresos/Burn:
- usar solo Pagado/Cobrado;
- cuando la métrica es "último mes con datos", detectar el último mes con movimientos realizados.
