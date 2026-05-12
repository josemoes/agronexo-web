# PROJECT_CONTEXT · TFM AgroNexo

> Documento maestro de contexto del proyecto.
> Subir al **knowledge base** del proyecto Claude.ai para que todos los chats arranquen con el mismo contexto.

---

## 1. Quién soy yo y qué hago

- Estudiante de TFM trabajando sobre un caso real: **AgroNexo Granada**.
- Estoy desarrollando un modelo de negocio Phygital con tres líneas de ingreso y un bot Telegram como motor de captación.
- Material y decisiones se construyen iterativamente; pido **lenguaje llano** y entregables concretos.

---

## 2. La empresa: AgroNexo

**Sector:** Agricultura andaluza (Granada). Especialización en olivar y almendro.
**Cliente B2B:** Cooperativas agrícolas + explotaciones medianas (~15-25 ha).
**Modelo Phygital:** Bot conversacional (lead magnet) + AgroNexo Advisory (asesoría in-situ).

### Producto estrella
- **Hidroinfiltrador** · sistema patentado por la UGR para llevar agua y nutrientes a la raíz.

### Las 3 líneas de ingreso

**Línea 1 · PRODUCTOS** (intermediación con compra directa en web)
- Melaza · Hidroinfiltradores · Nitrato potásico · Urea.
- Modelo: comisión sobre venta intermediada.

**Línea 2 · SERVICIOS** (AgroNexo Advisory)
- Servicios puntuales: Poda · Análisis de suelo · Visita técnica.
- Servicios integrales:
  - SCAN (diagnóstico in-situ)
  - DESIGN (plan de optimización)
  - DEPLOY (implementación)
  - CONTROL (seguimiento continuo)
  - FUNDING (gestión de subvenciones)

**Línea 3 · ARRENDAMIENTOS** (AgroNexo FINCAS)
- Activación de tierras infrautilizadas con paquete completo: arrendamiento + asesoramiento + servicios + productos.

---

## 3. Cliente ideal: Manuel Ortega Cabrera

- 52 años · Loja (Granada) · Olivicultor de segunda generación.
- **25 ha de olivar de regadío** productivas (variedad picual) pero con margen año a año más ajustado.
- **15 ha de olivar de secano infrautilizadas** que no gestiona pero le pesan moralmente.
- Socio de la **Cooperativa San Isidro de Loja** (canal B2B2C de captación).
- Conocimiento técnico medio. Escéptico con tecnología compleja. Usa WhatsApp a diario, no descarga apps nuevas.
- Sus hijos no quieren seguir el negocio salvo que vean rentabilidad sostenida y moderna.
- Es el **cliente ideal agregado**: combina los detonantes de las 3 líneas en un único perfil.

---

## 4. Customer Journey · 6 fases (versión validada v2)

### Fase 1 · Descubrimiento
QR en la cooperativa + boca a boca. Captación.

### Fase 2 · Cuestionario, diagnóstico y oferta inmediata · ⭐ MOMENTO CRÍTICO
Mientras Manuel completa el cuestionario en WhatsApp ya recibe:
- Diagnóstico personalizado.
- **Ofertas de productos con compra directa en web** (melaza, hidroinfiltrador, nitrato, urea).
- **Ofertas de servicios puntuales** (poda, análisis de suelo, visita técnica) con reserva inmediata.

AgroNexo monetiza desde el primer minuto, no espera al final del funnel.

### Fase 3 · Oferta de asesoramiento y estudio a medida · ⭐ MOMENTO CRÍTICO
Como camino opcional más ambicioso, se ofrece el SCAN + DESIGN. Quien quiere ir más allá del producto suelto.

### Fase 4 · Proyecto y seguimiento (recurrencia)
Si Manuel acepta el asesoramiento:
- Proyecto integral implementado (DEPLOY).
- Seguimiento continuo (CONTROL) con alertas WhatsApp contextuales.
- Productos recomendados en el momento agronómicamente justo.
- Servicios puntuales bajo demanda.

### Fase 5 · Paquete completo para fincas sin cuidar · ⭐ MOMENTO CRÍTICO
Cuando Manuel revela que tiene las 15 ha infrautilizadas, AgroNexo le ofrece un paquete completo (arrendamiento + asesoramiento + servicios + productos) gestionado end-to-end.

### Fase 6 · Fidelización y prescripción
Finca demo · Programa de referidos · Boca a boca en la cooperativa. Cierra el flywheel devolviendo nuevos leads a la Fase 1.

---

## 5. Reglas de comunicación y estilo

- **Lenguaje llano**. Nada de CAPEX/OPEX, lock-in tecnológico, marketplace contextual, B2B2C en mitad de la prosa.
- **Sin KPIs económicos** (sin euros, sin %, sin LTV, sin ticket medio, sin comisiones) hasta que se definan formalmente.
- KPIs **de comportamiento sí** (tasas de conversión, NPS, frecuencia, renovación).
- Idioma: **español**.
- Tono profesional pero accesible. Imaginar que se lo cuento a Manuel.

---

## 6. Identidad visual · Paleta de colores

Códigos hex consistentes en todos los entregables visuales:

| Concepto | Fill | Stroke |
|---|---|---|
| Descubrimiento (ámbar) | `#fef3c7` | `#92400e` |
| Productos (verde) | `#d1fae5` | `#065f46` |
| Servicios (azul) | `#dbeafe` | `#1e40af` |
| Arrendamientos (rosa/granate) | `#fce7f3` | `#9f1239` |
| Fidelización (morado) | `#e9d5ff` | `#6b21a8` |

---

## 7. Entregables generados hasta ahora

- `agronexo_customer_journey.docx` · Customer Journey v2 en Word con diagrama embebido.
- `agronexo_customer_journey_cliente_ideal_v2.md` · Fuente markdown.
- `agronexo_customer_journey_diagram.png` · Flowchart visual del journey.
- `01_journey_map.png` · Customer Journey Map con swimlanes (6 fases × 7 dimensiones).
- `02_service_blueprint.png` · Service Blueprint (frontstage / backstage / sistemas / equipos).
- `03_persona_card.png` · Persona card visual de Manuel.
- `04_flywheel.png` · Diagrama del flywheel (cómo F6 retroalimenta F1).
- `chatbot_flow_diagram.mermaid` · Flujo del bot Telegram (rutas quiz / catálogo / asesor).
- `agronexo_customer_journey_brief.md` · Brief general del customer journey.

---

## 8. Bot Telegram (estado)

- Implementado en **n8n self-hosted** (workflow ID `Z89a9LVWpn0QYyOg` en `https://n8n.civica-soft.com`).
- 3 rutas principales: Quiz · Catálogo · Asesor (con sub-rutas 3a y 3b).
- Integrado con Google Sheets vía OAuth2 para guardar leads.
- Comando `/reset` global.
- Pendientes: definir precios reales del catálogo S01-S10, arreglar consulta libre Gemini, tracking del embudo.

---

## 9. Pendientes y decisiones futuras

- Precios reales del catálogo de servicios (sustituir "A consultar").
- Tracking analítico del embudo (% abandono por pregunta).
- Email opcional como dato adicional en el bot.
- Política de privacidad formal (GDPR).
- Notificación email al asesor cuando entra lead caliente.
- Definir KPIs económicos del modelo cuando estén listos.

---

## 10. Cómo usar este documento

- Siempre que arranques un chat nuevo en el proyecto, Claude ya tendrá este contexto.
- No hace falta repetir quién es Manuel, qué son las 3 líneas, ni las 6 fases del journey.
- Si actualizas decisiones importantes (por ejemplo, precios cuando los tengas), edita este documento y vuélvelo a subir al knowledge base.
