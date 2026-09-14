# ICN292 — Laboratorio 3: Automatización de procesos con n8n

**Iván González Vela · UTFSM Campus Vitacura · 2026**

---

## Descripción

Este repositorio contiene los workflows de n8n desarrollados para el Laboratorio 3 del curso ICN292 (Gestión de Procesos de Negocios). El caso de negocio es AndesHogar SpA, empresa de e-commerce que recibe solicitudes de devolución de productos.

El objetivo del laboratorio es automatizar el proceso de triage de solicitudes mediante un flujo n8n que clasifica cada caso según las reglas de negocio definidas y responde automáticamente.

## Parámetros personales

| Parámetro | Valor |
|-----------|-------|
| Semilla S | 360 |
| Umbral de monto U | $40.000 |
| Plazo máximo D | 7 días |

## Archivos

| Archivo | Descripción |
|---------|-------------|
| `ICN292-Lab3-Gonzalez-Ivan-triage.json` | Flujo principal: recibe solicitudes por webhook, las clasifica y responde |
| `ICN292-Lab3-Gonzalez-Ivan-emisor.json` | Flujo auxiliar: envía las 15 solicitudes al webhook de triage |
| `ICN292-Lab3-Gonzalez-Ivan-resumen.json` | Flujo programado: genera resumen diario de solicitudes procesadas |

## Reglas de clasificación

1. **DATOS_INVALIDOS** — falta `id_solicitud` o `monto ≤ 0`
2. **RECHAZO** — `dias_desde_compra > 7` o `estado_producto = danado_por_uso`
3. **REVISION** — `monto > 40.000` o `estado_producto = con_fallas`
4. **APROBACION** — todo lo demás

*Borrador — se actualizará con el informe final.*
