---
name: finanzas-sommos
description: Usa esta skill para operar, auditar, reparar o extender el workflow financiero de Sommos en Google Sheets: Config, reglas de categorización, Transacciones, TC BCB, Estado de pagos, CxC, CxP, Presupuesto, Bancos, Runway Mensual y Dashboard. También úsala para importar o diseñar importación de extractos bancarios. No usar para contabilidad fiscal, impuestos o decisiones contables que requieran criterio profesional externo.
---

# Finanzas Sommos

## Objetivo

Mantener el archivo financiero como un sistema simple, trazable y altamente automático, usando **Transacciones como fuente operativa principal** y evitando duplicidad de carga.

La prioridad es responder correctamente:
- cuánto cash real existe;
- qué cuentas están por cobrar y pagar;
- cuánto se ha ejecutado y comprometido del presupuesto;
- cuál es el burn y runway;
- si los bancos están conciliados;
- qué registros requieren intervención manual.

## Regla principal

Antes de modificar el archivo, **leer la estructura actual** de las pestañas y columnas. El usuario modifica el Sheet con frecuencia; nunca asumir que las columnas mantienen posiciones históricas.

Después de cada edición:
1. verificar fórmulas y valores efectivos;
2. buscar errores como `#REF!`, `#VALUE!`, `#N/A` y `#ERROR!` en las áreas afectadas;
3. confirmar que Dashboard, Runway, CxC, CxP y Bancos siguen recibiendo los datos correctos;
4. preservar formato, validaciones y datos manuales no relacionados.

## Flujo operativo

Usar este orden conceptual:

`Config → Reglas categorización → Transacciones → TC BCB → Estado de pagos → CxC/CxP → Presupuesto → Bancos → Runway Mensual → Dashboard`

### 1. Config
- Mantener catálogos base: países, monedas, tipos, categorías, conciliación, presupuesto y estados.
- No agregar opciones nuevas sin necesidad.

### 2. Reglas categorización
- Usar palabras clave de descripción/proveedor para asignar categoría automática.
- Ejemplo conocido: `Google Cloud → Platform cost`.
- Si no existe una regla inequívoca, devolver `Por categorizar`; nunca inventar una categoría.

### 3. Transacciones
Es la **fuente única de carga operativa**.

La estructura vigente esperada se documenta en `references/sheet-schema.md`, pero siempre debe validarse en vivo antes de escribir.

Comportamientos:
- Categoría: automática según reglas.
- TC a USD:
  - USD = `1`.
  - SOL = `0.28` fijo mientras esa sea la política definida por el usuario.
  - BOB = TCO oficial del BCB correspondiente a la fecha; si no hay publicación ese día, usar el último TCO oficial disponible anterior a la fecha.
  - Otras monedas = `TC manual (otras)`.
- Monto USD:
  - USD: monto original.
  - BOB: monto original / TC.
  - Monedas cuyo TC representa USD por unidad local, por ejemplo SOL=0.28: monto original × TC.

No inventar tipos de cambio.

### 4. Estado de pago y derivación automática
Los estados operativos definidos son:
- `Pagado/Cobrado`
- `Pendiente`

Derivación:
- `Ingreso + Pendiente → CxC`
- `Egreso + Pendiente → CxP`

Cuando un registro se cambia a `Pagado/Cobrado` en Transacciones, debe dejar de aparecer automáticamente en CxC/CxP.

`Estado de pagos` es una vista de control y **no debe convertirse en una segunda fuente de carga**.

### 5. Presupuesto
- `Ejecutado`: considerar operaciones efectivamente `Pagado/Cobrado`.
- `Comprometido`: considerar egresos `Pendiente` cuando exista categoría suficiente para asignarlos.
- Nunca inventar asignación presupuestaria si el registro no tiene categoría.

### 6. Bancos y conciliación
El sistema debe trabajar por cuenta y por mes.

Reglas:
- Saldo inicial del mes = saldo final real del mes anterior.
- Ingresos del mes = transacciones `Ingreso + Pagado/Cobrado` de esa cuenta, moneda y mes.
- Egresos del mes = transacciones `Egreso + Pagado/Cobrado` de esa cuenta, moneda y mes.
- Saldo final calculado = saldo inicial + ingresos - egresos.
- Saldo final banco = dato real manual copiado del banco al cierre.
- Diferencia = saldo final banco - saldo final calculado.
- Conciliado cuando la diferencia está dentro de la tolerancia definida; de lo contrario, marcar `Revisar`.

Nunca sobrescribir silenciosamente un saldo final bancario real ingresado manualmente.

Dashboard debe usar el **último cierre bancario completo real**, no sumar meses históricos ni sustituirlo por un saldo calculado provisional.

### 7. Runway y Dashboard
- Runway debe usar cash real de apertura/cierre y flujos esperados sin duplicar transacciones.
- Burn e ingresos realizados deben basarse en `Pagado/Cobrado`.
- Si se usa "último mes con datos", detectar el último mes real con movimientos realizados.
- No presentar un runway aparentemente enorme sin advertir si faltan gastos recurrentes u operativos.

## Importación de extractos bancarios

Cuando el usuario quiera cargar extractos:
- Preferir CSV/XLSX sobre PDF cuando el banco lo permita.
- Para PDF, extraer primero a una tabla de staging; no escribir directamente a Transacciones sin validación.
- Diseñar o usar una pestaña `Importación extractos` con al menos:
  `Fecha | Banco | Descripción original | Tipo | Moneda | Monto | Categoría detectada | Duplicado | Importar`.
- Identificar duplicados con una clave estable, por ejemplo `Banco + Fecha + Monto + Descripción` y, si existe, un ID bancario nativo.
- No importar filas marcadas como duplicadas sin revisión explícita.
- Después de importar a Transacciones, dejar que las automatizaciones existentes hagan categorización, TC, CxC/CxP, Bancos y Dashboard.

Leer `references/importacion-extractos.md` para el flujo completo.

## Guardrails financieros

- No inventar saldos, categorías, monedas, tipos de cambio ni estados.
- No borrar históricos para "arreglar" una fórmula.
- No sumar saldos mensuales históricos como si fueran cash actual.
- No contar `Pendiente` como ingreso cobrado o gasto pagado.
- No duplicar una misma operación en Transacciones y CxC/CxP como cargas manuales independientes.
- Distinguir saldo real bancario de saldo calculado.
- Si una fórmula depende de una columna eliminada, reparar contra el encabezado actual, no contra índices memorizados.

## Archivos de referencia

Antes de una tarea relevante, abrir solo las referencias necesarias:
- `references/sheet-schema.md`: pestañas, columnas y roles.
- `references/automation-rules.md`: reglas de automatización y fórmulas conceptuales.
- `references/importacion-extractos.md`: importación de CSV/PDF y deduplicación.
- `references/qa-checklist.md`: checklist antes de cerrar cambios.
