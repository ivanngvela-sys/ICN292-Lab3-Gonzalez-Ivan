# ICN292 — Laboratorio 3: Automatización de procesos con n8n

**Nombre:** Iván González Vela  
**RUT:** 20.817.360  
**Semilla S:** 360 — **Umbral U:** $40.000 — **Plazo D:** 7 días  
**Fecha:** Septiembre 2026  
**Repositorio:** https://github.com/ivanngvela-sys/ICN292-Lab3-Gonzalez-Ivan

---

## Descripción

Flujos n8n para el caso AndesHogar SpA. El proceso automatiza el triage de solicitudes de devolución: recibe cada caso por webhook, lo clasifica según las reglas de negocio y responde con la decisión.

## Archivos

| Archivo | Descripción |
|---------|-------------|
| `ICN292-Lab3-Gonzalez-Ivan-triage.json` | Flujo principal de clasificación |
| `ICN292-Lab3-Gonzalez-Ivan-emisor.json` | Flujo auxiliar que envía las 15 solicitudes |
| `ICN292-Lab3-Gonzalez-Ivan-resumen.json` | Flujo programado de resumen diario |

## Cómo reproducir

**Requisito:** cuenta en [n8n.io](https://n8n.io) (cloud o instancia local).

1. En n8n, ir a **Workflows → Import from file**.
2. Importar primero `triage.json`. Activar el workflow y copiar la URL del nodo Webhook.
3. Importar `emisor.json`. En el nodo **Enviar a triage**, reemplazar la URL por la copiada en el paso anterior.
4. Abrir el triage en modo test (botón **Test workflow**), luego ejecutar el emisor con **Test workflow**.
5. Importar `resumen.json`. Se ejecuta automáticamente cada día a las 23:00 UTC (20:00 Chile).

## Reglas de clasificación

| Prioridad | Condición | Resultado |
|-----------|-----------|-----------|
| 1 | `id_solicitud` vacío | DATOS_INVALIDOS |
| 2 | `monto ≤ 0` | DATOS_INVALIDOS |
| 3 | `dias_desde_compra > 7` | RECHAZO |
| 4 | `estado_producto = danado_por_uso` | RECHAZO |
| 5 | `monto > 40.000` | REVISION |
| 6 | `estado_producto = con_fallas` | REVISION |
| — | Todo lo demás | APROBACION |
