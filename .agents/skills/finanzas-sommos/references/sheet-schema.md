# Esquema funcional del archivo Finanzas Sommos

> Importante: este documento describe la estructura de referencia. Antes de escribir, validar los encabezados actuales del Google Sheet.

## Config
Catálogos base para listas desplegables y estados.

## Reglas categorización
Reglas basadas en palabra clave, tipo y estado activo para asignar una categoría a la descripción de una transacción.

## Transacciones
Estructura de referencia actual:

| Columna | Campo | Tipo | Rol |
|---|---|---|---|
| A | Fecha | Fecha | Fecha de movimiento |
| B | Tipo | Dropdown | Ingreso / Egreso |
| C | País | Dropdown | País asociado |
| D | Categoría | Fórmula | Categoría automática |
| E | Descripción | Texto | Concepto/proveedor |
| F | Moneda | Dropdown | USD / BOB / SOL / otras |
| G | Monto original | Número | Importe en moneda original |
| H | TC a USD | Fórmula | TC automático según moneda |
| I | Monto USD | Fórmula | Conversión a USD |
| J | Banco | Dropdown | Cuenta/banco |
| K | Conciliación | Dropdown | Estado de conciliación |
| L | Presupuestado | Dropdown | Presupuestado / no presupuestado |
| M | Estado pago | Dropdown | Pagado/Cobrado / Pendiente |
| N | Fecha vencimiento | Fecha | Fecha límite |
| O | Responsable | Texto | Responsable interno |
| P | TC manual (otras) | Número | TC manual para moneda no automatizada |

## TC BCB
Serie diaria para BOB:
- Fecha
- TCO publicado BCB
- TCO vigente
- Estado (Publicado / Arrastre último TCO / Sin dato)
- Fuente o autorización de importación

## Estado de pagos
Vista derivada de Transacciones para control operativo. No debe ser fuente primaria.

## CxC
Vista automática de Transacciones filtrando `Ingreso + Pendiente`.

## CxP
Vista automática de Transacciones filtrando `Egreso + Pendiente`.

## Presupuesto
Campos conceptuales:
- Mes
- Categoría
- Presupuesto USD
- Ejecutado USD
- Comprometido USD
- Disponible USD
- Variación USD
- % ejecución
- Comentario

## Bancos
Histórico mensual por cuenta. Debe diferenciar:
- saldo inicial;
- TC inicial;
- saldo inicial USD;
- saldo final banco real/manual;
- TC de cierre;
- saldo final USD;
- ingresos del mes;
- egresos del mes;
- saldo final calculado;
- diferencia;
- conciliación automática.

## Runway Mensual
Vista mensual de cash inicial, cobros esperados, egresos comprometidos, flujo neto, cash final, burn y runway.

## Dashboard
Indicadores de dirección:
- cash disponible;
- CxC pendiente;
- CxP pendiente;
- ingresos último mes con datos;
- burn último mes con datos;
- runway;
- CxC vencida;
- presupuesto disponible.
