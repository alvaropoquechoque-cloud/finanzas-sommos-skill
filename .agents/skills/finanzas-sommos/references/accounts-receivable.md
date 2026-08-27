# Accounts receivable — snapshot de referencia

Fecha del snapshot: **2026-08-27**.

Este archivo sirve como contexto. **No sustituye la lectura en vivo de `Transacciones` o `CxC`.**

Antes de crear cualquiera de estas obligaciones, comprobar si ya existe. Varias de ellas fueron cargadas al Sheet durante agosto de 2026.

## 1. Grants

Categoría:

`Other financing cash flow`

### INNOVATECH

Monto pactado total: USD 90,000.

Monto recibido informado: USD 30,000.

Pendiente conocido:

- USD 25,000 — fecha esperada/vencimiento: 2026-08-31.
- USD 35,000 — fecha esperada/vencimiento: 2026-09-30.

No registrar USD 60,000 como una sola CxC si los dos desembolsos ya existen individualmente.

### Startup Perú

Programa finalizado.

Desembolso final pendiente:

- USD 934 — 2026-08-31.

No existen otros desembolsos futuros conocidos después de este pago.

### INCOFIN

Programa finalizado el 2026-01-31.

Desembolso pendiente:

- USD 3,945 — vencido desde 2026-01-31.

El país no fue confirmado por el usuario. No inventarlo.

### FIID Guatemala

Monto pactado total: USD 100,000.

Monto recibido informado: USD 29,970.

Pendiente:

- USD 40,000 — 2026-10-31.
- USD 30,030 — 2027-02-28.

País: GUATEMALA.

## 2. Clientes — facturas históricas pendientes conocidas

### Banco de Crédito del Perú

- Factura julio 2026: USD 3,672.
- La fecha exacta de vencimiento histórica no fue confirmada.

Categoría: `Full new integration incomes`.

País: PERU.

### BCP Perú + Habitat

- Factura febrero 2026: USD 3,000.
- Vencimiento no confirmado.

Categoría: `Proof of concept incomes`.

País: PERU.

### RENDINERO

- Factura junio 2026: USD 1,000.
- Factura julio 2026: USD 1,000.
- Vencimientos históricos no confirmados.

Categoría: `Proof of concept incomes`.

País no confirmado. No inventarlo.

### Primaa

- Factura junio 2026: USD 1,750.
- Vencimiento histórico no confirmado.

Categoría: `Proof of concept incomes`.

País no confirmado. No inventarlo.

## 3. Clientes — recurrencias conocidas

Estas recurrencias deben existir como filas separadas por mes.

### Banco Sol

- Agosto 2026: BOB 17,500 — fecha esperada 2026-08-31.
- Septiembre 2026: BOB 17,500 — fecha esperada 2026-09-30.

País: BOLIVIA.

Categoría: `Full new integration incomes`.

No recrear julio: los ingresos de julio ya fueron conciliados con el extracto de BancoSol.

### Banco de Crédito del Perú

Pago mensual conocido: USD 3,672 hasta diciembre 2026.

- Agosto: USD 3,672 — 2026-08-31.
- Septiembre: USD 3,672 — 2026-09-30.
- Octubre: USD 3,672 — 2026-10-31.
- Noviembre: USD 3,672 — 2026-11-30.
- Diciembre: USD 3,672 — 2026-12-31.

País: PERU.

Categoría: `Full new integration incomes`.

### RENDINERO

Pago mensual conocido: USD 1,000 hasta noviembre 2026.

- Agosto: USD 1,000 — 2026-08-31.
- Septiembre: USD 1,000 — 2026-09-30.
- Octubre: USD 1,000 — 2026-10-31.
- Noviembre: USD 1,000 — 2026-11-30.

Categoría: `Proof of concept incomes`.

País no confirmado.

### Leads Quiero BCP

- Agosto 2026: USD 4,000 — 2026-08-31.

País: PERU.

Categoría: `Proof of concept incomes`.

## 4. Anti-duplicación

Antes de crear una CxC, buscar al menos por:

- descripción/cliente;
- moneda;
- monto original;
- fecha de emisión/registro;
- fecha de vencimiento;
- estado pendiente.

Si una obligación equivalente ya existe, no crear una segunda fila.

## 5. Regla contable-operativa

CxC pendiente no es caja.

Los importes anteriores solo pasan a ingreso realizado cuando la fila correspondiente se marque `Pagado/Cobrado` y, cuando aplique, quede conciliada con el banco.
