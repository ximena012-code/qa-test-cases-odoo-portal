# TC — Service Reports (Portal FSM)

**Módulo:** Service Reports  
**Ambiente:** QA / Demo  
**Rol principal:** Despachador (DSP)

## TC-01 — Acceso al listado (DSP)
**Precondiciones:** Usuario DSP autenticado en el portal.  
**Pasos:**
1. Ir a `/my/fsm/service_reports`
2. Verificar título "Service Reports" y contador de registros
3. Verificar columnas: Appointment, Contact, Technicians, Signed By, Completed On
**Esperado:** Listado visible con encabezados y datos o estado vacío coherente.

## TC-02 — Búsqueda
**Pasos:**
1. Escribir un término que exista en Appointment/Contact
2. Ejecutar búsqueda
3. Buscar un término inexistente (`zzzzz_no_match`)
**Esperado:** Filtra resultados; sin coincidencias muestra estado vacío.

## TC-03 — Orden por Completed On
**Pasos:**
1. Ordenar Asc
2. Ordenar Desc
**Esperado:** El orden de fechas cambia según la dirección.

## TC-04 — Paginación
**Precondiciones:** > 25 registros con `limit=25`.  
**Pasos:**
1. Verificar página 1
2. Ir a página 2
3. Volver con Previous
**Esperado:** Pager activo; datos distintos por página; contador total estable.

## TC-05 — Descarga / apertura PDF
**Pasos:**
1. Clic en PDF de un registro con reporte
**Esperado:** Se abre o descarga el PDF del appointment.

## TC-06 — Signed By vacío
**Precondiciones:** Registro con firma/documento pero `signed_by` vacío.  
**Pasos:**
1. Localizar el registro en listado
2. Abrir PDF si aplica
**Esperado:** Columna Signed By vacía o guion; no rompe la fila ni el PDF.

## TC-07 — i18n EN / ES
**Pasos:**
1. Cambiar idioma a ES
2. Volver a EN
**Esperado:** Títulos y UI se traducen; datos de negocio se mantienen.

## TC-08 — Permisos TEC
**Pasos:**
1. Login como TEC
2. Abrir URL directa `/my/fsm/service_reports`
**Esperado:** Acceso denegado / 404 según regla de producto (sin menú Service Reports).

## TC-09 — Permisos PRT (sin FSM)
**Pasos:**
1. Login como usuario portal sin grupo FSM
2. Abrir `/my/fsm/service_reports`
**Esperado:** 403 / página de acceso denegado.

## TC-10 — Persistencia tras recarga
**Pasos:**
1. Anotar un registro y el contador total
2. Abrir PDF y volver al listado
3. Recargar la vista
**Esperado:** Mismos datos del registro y mismo contador.
