# Importación de extractos bancarios

## Prioridad de formatos
1. CSV
2. XLSX
3. PDF con texto estructurado
4. PDF escaneado / imagen (último recurso)

Preferir archivos estructurados para reducir errores de extracción.

## Flujo recomendado

`Archivo bancario → extracción → staging → normalización → deduplicación → revisión → Transacciones`

## Staging recomendado: Importación extractos

Campos mínimos:
- Fecha
- Banco
- Descripción original
- Tipo detectado
- Moneda
- Monto
- Categoría detectada
- ID bancario, si existe
- Clave deduplicación
- Estado duplicado
- Importar Sí/No

## Normalización

- Ingresos positivos / egresos negativos deben convertirse al esquema explícito Tipo + Monto positivo.
- Mantener la descripción original para trazabilidad.
- No inferir categoría cuando no exista una regla clara.

## Deduplicación

Preferencia:
1. ID nativo de transacción del banco.
2. Si no existe: hash/clave de `Banco + Fecha + Monto + Descripción normalizada`.

Estados recomendados:
- `Nuevo`
- `Posible duplicado`
- `Ya registrado`

No importar automáticamente `Posible duplicado` sin validación.

## PDF

Para PDF:
- extraer tabla antes de tocar Transacciones;
- validar totales si el extracto incluye saldo inicial/final;
- comparar suma de movimientos contra variación de saldo cuando sea posible;
- si el PDF es escaneado, tratar OCR como proceso menos confiable y exigir revisión.

## Conciliación posterior

Después de importar movimientos:
- Transacciones aplica categorización y TC;
- Bancos recalcula ingresos/egresos del mes;
- comparar saldo calculado con saldo final real del extracto;
- cualquier diferencia debe investigarse, no ocultarse.
