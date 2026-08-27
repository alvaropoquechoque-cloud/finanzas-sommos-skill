# Ejemplos de uso

## Consultar CxC

Prompt:

```text
$finanzas-sommos revisa la CxC actual, agrúpala por mes de vencimiento y dime qué está vencido
```

Comportamiento esperado:

1. Leer `CxC`/`Transacciones` en vivo.
2. No usar el snapshot como sustituto.
3. Separar vencido, próximo mes y futuro.
4. Mostrar montos en moneda original y USD cuando sea útil.

## Cargar una nueva CxC

Prompt:

```text
$finanzas-sommos agrega una cuenta por cobrar de USD 5,000 a Cliente X con vencimiento 30/09/2026
```

Comportamiento esperado:

1. Buscar duplicado.
2. Confirmar/obtener país y categoría si no pueden deducirse de reglas existentes.
3. Crear en `Transacciones` como `Ingreso + Pendiente`.
4. Verificar que aparezca en CxC.
5. Verificar que no aumente ingresos realizados ni caja.

## Cargar CxP

Prompt:

```text
$finanzas-sommos registra esta deuda con proveedor Y y actualiza el runway
```

Comportamiento esperado:

1. Crear `Egreso + Pendiente`.
2. Verificar CxP.
3. Verificar que banco/burn realizado no cambien.
4. Revisar runway por fecha de vencimiento.

## Importar extracto

Prompt:

```text
$finanzas-sommos importa este extracto de BancoSol y concilia el mes
```

Comportamiento esperado:

1. Calcular totales del extracto.
2. Staging.
3. Detectar duplicados.
4. Importar movimientos únicos.
5. Actualizar Bancos.
6. Comprobar diferencia.
7. Ejecutar QA.

## Presupuesto

Prompt:

```text
$finanzas-sommos agrega septiembre al Presupuesto con las mismas categorías y deja el Budget vacío para carga manual
```

Comportamiento esperado:

1. Leer layout actual.
2. Mantener mismo diseño/colores.
3. Crear Budget manual, P&L automático y %.
4. Consolidar Salaries.
5. Verde si ejecutado < Budget; rojo si ejecutado > Budget.
6. Verificar Dashboard/runway si tienen dependencias.

## Cierre mensual

Prompt:

```text
$finanzas-sommos haz el checklist de cierre de agosto y dime qué falta antes de cerrarlo
```

Comportamiento esperado:

- bancos;
- movimientos pendientes;
- por categorizar;
- CxC/CxP;
- presupuesto;
- runway;
- Dashboard;
- errores de fórmula.
