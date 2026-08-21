# Checklist QA financiero

Antes de cerrar una modificación:

## Estructura
- [ ] Se leyeron encabezados actuales antes de escribir.
- [ ] No se sobrescribieron columnas manuales no relacionadas.
- [ ] Dropdowns y formatos relevantes siguen presentes.

## Fórmulas
- [ ] No hay `#REF!`.
- [ ] No hay `#VALUE!`.
- [ ] No hay `#N/A` inesperado.
- [ ] No hay `#ERROR!`.
- [ ] Fórmulas spill/array tienen espacio para expandirse.

## Transacciones
- [ ] USD tiene TC 1.
- [ ] SOL tiene TC 0.28.
- [ ] BOB usa TCO oficial correspondiente a la fecha o último oficial anterior.
- [ ] Monto USD sigue la convención correcta.
- [ ] `Pendiente` no se cuenta como realizado.

## CxC / CxP
- [ ] Ingreso + Pendiente aparece en CxC.
- [ ] Egreso + Pendiente aparece en CxP.
- [ ] Pagado/Cobrado deja de aparecer como pendiente.

## Bancos
- [ ] Ingresos y egresos se filtran por banco, moneda, mes y estado.
- [ ] Saldo calculado es correcto.
- [ ] Saldo final real no fue sobrescrito.
- [ ] Dashboard no suma meses históricos.

## Dashboard / Runway
- [ ] CxC y CxP coinciden con las vistas.
- [ ] Cash usa el último cierre completo real.
- [ ] Ingresos y burn usan movimientos realizados.
- [ ] Runway no duplica CxC/CxP con Transacciones.
