# CLAUDE.md · Prototipo web AgroNexo

> Este archivo lo lee Claude Code automáticamente al arrancar en este directorio. No lo borres ni lo muevas.

---

## Qué es este proyecto

Prototipo de web corporativa de **AgroNexo Granada** para el TFM.

Es un **prototipo navegable**: un conjunto de páginas estáticas con navegación entre ellas para demostrar el modelo de negocio y la experiencia de usuario. **No es un producto operativo.** Los botones de "Comprar", "Reservar" o "Contactar" NO son funcionales. Llevan a `#` o redirigen a `/contacto`.

El objetivo es defenderlo en el TFM, no venderle a un cliente real.

---

## Identidad de marca

**Tagline:** *Del dato a la rentabilidad agrícola*

**Estrategia de marca:** AgroNexo se posiciona como el nexo entre la **tradición agrícola** y la **tecnología aplicada**, aportando valor real y tangible al agricultor. El logo combina una hoja (tradición, naturaleza, oficio milenario) con un circuito impreso (tecnología, datos, modernidad).

**Mood:** mediterráneo, terroso, tradicional con un toque tech. Inspirado en olivares de Andalucía y Toscana, mosaicos romanos antiguos, manos curtidas de agricultor, aceitunas, hojas de olivo. La tecnología nunca grita: aparece de forma discreta, al servicio del campo.

**Tono de voz:**
- Profesional pero accesible. Imagina que lo lee Manuel en el móvil sentado en su tractor.
- Lenguaje llano. Cero "innovación disruptiva", "sinergia", "liderazgo", "transformación".
- Frases cortas. Beneficios concretos, no abstracciones.
- Cuando hablamos de la marca, podemos ser poéticos (el olivar como herencia, el dato como herramienta). Cuando hablamos del producto, somos directos (qué hace, qué cuesta, cómo se pide).

---

## Persona objetivo

Cliente ideal: **Manuel Ortega**. Olivicultor de 52 años en Loja (Granada).

- Mobile-first sin discusión. Usa WhatsApp a diario, no descarga apps.
- Escéptico con tecnología compleja, confía en el boca a boca.
- Decisiones rápidas si ve la cosa clara.

Detalles completos en `docs/PROJECT_CONTEXT.md`. Consúltalo cuando necesites contexto sobre la persona, el journey o las 3 líneas de negocio.

---

## Inspiración estilística

Web de referencia: [carmowood.com](https://www.carmowood.com/).

Lo que tomamos de ahí:
- **Hero impactante** con video o foto grande de fondo + tagline contundente.
- **Storytelling poético** en la sección "sobre nosotros": metáforas que conecten producto y valores humanos.
- **Marca paraguas con divisiones diferenciadas**: ellos tienen CarmoFarm + CarmoForm. Nosotros: Productos + Servicios + Arrendamientos. Cada línea es casi una submarca dentro de AgroNexo.
- **Sección de casos/obras** con foto grande, categoría, ubicación y nombre del proyecto.
- **Aire generoso** entre secciones. Sin saturar.
- **Tipografía con personalidad**: títulos grandes, anchos, con peso.

Lo que NO copiamos:
- El loader animado del inicio (innecesario para el prototipo).
- Múltiples idiomas (solo español).
- Estructura de menús anidados de 3 niveles (sobre-complicado para nuestras 6 páginas).

---

## Stack

- **Astro** (sin TypeScript)
- **Tailwind** para estilos
- **Cero JavaScript en runtime**: HTML estático generado en build.
- Sin Alpine, sin React, sin Vue, sin islas interactivas.

Si en algún momento necesitas una pieza con estado (carrusel, acordeón), prioriza una solución CSS-only o el `<details>` nativo de HTML. Solo si no hay forma, hablamos de añadir algo más.

---

## Las 6 páginas

```
/                 → Home (hero + las 3 líneas + storytelling + CTA)
/productos        → Landing de productos: cards estáticas de melaza,
                    hidroinfiltrador, nitrato potásico, urea.
/servicios        → Landing de servicios: puntuales (poda, análisis,
                    visita técnica) + integrales (SCAN, DESIGN,
                    DEPLOY, CONTROL, FUNDING).
/asesoramiento    → Landing del estudio a medida (Fase 3 del journey).
/fincas           → Landing del paquete completo para fincas sin
                    cuidar (Fase 5).
/contacto         → Página con formulario decorativo (no funcional).
```

Sin slugs dinámicos. Sin fichas individuales de producto/servicio. Cada landing agrupa sus cards en la misma página.

---

## Paleta corporativa

Estos cinco colores son la marca. No se sale de aquí salvo para microvariaciones (opacidades, sombras tenues) o excepciones explícitamente documentadas más abajo.

```js
// tailwind.config.mjs (extracto)
theme: {
  extend: {
    colors: {
      // Verde oscuro corporativo (textos principales sobre fondo claro, botones primarios)
      'agronexo-dark': '#193b29',
      // Verde oliva (acentos, hover, badges, divisores de marca)
      'agronexo-olive': '#6c8e32',
      // Gris oscuro casi negro (textos largos sobre blanco)
      'agronexo-text': '#2E2E2E',
      // Gris cálido (fondos sutiles, líneas suaves, texto secundario)
      'agronexo-warm': '#A2A092',
      // Blanco (fondos principales)
      'agronexo-bg': '#ffffff',
    }
  }
}
```

**Cómo se usan:**

- **#193b29 (verde oscuro)** → títulos grandes, botones primarios, fondos de secciones impactantes (con texto blanco encima), footer.
- **#6c8e32 (verde oliva)** → acentos: hover de links, líneas decorativas, iconos destacados, badges, el segundo color del logo. NO usar como fondo grande de sección.
- **#2E2E2E (gris muy oscuro)** → texto largo de cuerpo, encabezados secundarios.
- **#A2A092 (gris cálido)** → texto descriptivo secundario, líneas divisorias, fondos sutiles tipo `bg-agronexo-warm/10`.
- **#ffffff (blanco)** → fondo principal de la web, texto sobre verde oscuro.

**Cómo NO usarla:** mezclar más de tres colores en una misma sección. Mantener cada sección con un color dominante + uno o dos acentos.

**Excepción documentada — color CTA:**

- **#c4622d (terracota)** → token `agronexo-cta`. Uso exclusivo del botón flotante de Telegram (FAB en `BaseLayout.astro`). Color complementario al verde en la rueda de color; encaja con el mood mediterráneo del moodboard (terracota, ocre). **No usar en ningún otro elemento de la web.** Definido en `src/styles/global.css` como `--color-agronexo-cta`.

---

## Tipografías

Dos familias, ambas de Google Fonts.

- **Montserrat** → títulos, headings, tagline, navegación. Geométrica, moderna, con autoridad. Pesos 600 (semibold) y 700 (bold).
- **DM Sans** → cuerpo de texto, descripciones, párrafos largos, formularios. Humanista, legible, accesible. Pesos 400 (regular) y 500 (medium).

Configura el `<link>` de Google Fonts en `BaseLayout.astro` precargando solo los pesos que se usan.

```js
// tailwind.config.mjs (extracto)
fontFamily: {
  display: ['Montserrat', 'system-ui', 'sans-serif'],
  body: ['"DM Sans"', 'system-ui', 'sans-serif'],
}
```

**Escala tipográfica sugerida (mobile-first):**

| Uso | Tamaño móvil | Tamaño desktop | Familia | Peso |
|---|---|---|---|---|
| Hero title | 36px (`text-4xl`) | 64px (`md:text-6xl`) | Montserrat | 700 |
| Section title | 28px (`text-3xl`) | 40px (`md:text-5xl`) | Montserrat | 700 |
| Card title | 20px (`text-xl`) | 24px (`md:text-2xl`) | Montserrat | 600 |
| Body | 16px (`text-base`) | 18px (`md:text-lg`) | DM Sans | 400 |
| Body small | 14px (`text-sm`) | 16px (`md:text-base`) | DM Sans | 400 |
| Caption | 12px (`text-xs`) | 14px (`md:text-sm`) | DM Sans | 500 |

---

## Logo y assets disponibles

```
public/
├── logo.png             → logo principal en color, fondo claro
                           (a futuro: convertir a SVG para mejor calidad)
├── favicon.svg          → (pendiente de generar)
└── images/              → (pendiente; se va llenando con stock photos
                           y assets conforme vayamos avanzando)
```

**Uso del logo:**
- En el Header: alto 36px en móvil, 44px en desktop. Mantener proporción.
- En el Footer: variante en blanco (cuando tengamos `logo-white.png`) sobre fondo verde oscuro.
- En el hero o secciones impactantes: NO repetir logo, queda redundante.

---

## Componentes a crear

Estructura sugerida en `src/components/`:

- `Header.astro` — navegación principal (logo + 6 links + tagline opcional)
- `Footer.astro` — footer amplio con tagline grande tipo Carmowood
- `Hero.astro` — hero reutilizable (props: title, subtitle, cta, backgroundImage)
- `SectionTitle.astro` — título de sección con estilo consistente
- `ProductCard.astro` — card de producto
- `ServiceCard.astro` — card de servicio
- `CaseCard.astro` — card de caso/obra (estilo Carmowood)
- `CTASection.astro` — sección de llamada a la acción genérica
- `ThreeLines.astro` — sección "Las 3 líneas" para la home

En `src/layouts/`:

- `BaseLayout.astro` — layout base con `<head>`, Header y Footer

---

## Reglas de código

- **Idioma del código y comentarios:** inglés.
- **Idioma del contenido visible al usuario:** español.
- **Naming:** camelCase para variables, PascalCase para componentes, kebab-case para archivos.
- **Funciones pequeñas**, una responsabilidad cada una.
- **Mobile-first** siempre. Empieza estilando para móvil y añade breakpoints hacia arriba.
- **Prettier** con configuración default.

---

## Reglas de contenido

- **Tono profesional pero accesible.** Imagina que lo lee Manuel en el móvil sentado en su tractor.
- **Lenguaje llano.** Cero "innovación disruptiva", "sinergia", "liderazgo", "transformación".
- **Frases cortas. Beneficios concretos**, no abstracciones.
- **NO inventar precios reales.** Donde haya precio, "Consulta precio" o "Desde X €" claramente decorativo.
- **NO inventar testimonios de clientes**, nombres reales o datos económicos.
- **Los CTA son decorativos**: "Pídelo en cooperativa", "Solicita información", "Habla con un asesor". No "Compra ahora" si no se va a poder comprar.

---

## Reglas operativas para Claude Code

- **Antes de empezar una tarea nueva**, consulta `docs/PROJECT_CONTEXT.md` si necesitas contexto.
- **Para cada página nueva**, dime primero el plan de secciones (mini brief: qué secciones, en qué orden, qué CTA). Espera confirmación antes de generar código.
- **No instales dependencias nuevas** sin avisarme y justificarlas.
- **No cambies el stack** decidido (Astro + Tailwind, sin TS, sin islas) sin proponérmelo primero.
- **No mezcles paletas**: la paleta de la web es la corporativa (5 colores). La paleta de los diagramas del journey (ámbar, azul, rosa, morado) NO se usa en la web.
- **Commits** en inglés, formato Conventional Commits (`feat:`, `fix:`, `style:`, etc.).
- **Si encuentras una contradicción** entre lo que te pido y lo que dice este CLAUDE.md, párate y pregúntame.

---

## Lo que NO quiero ver en esta web

- Carrito real, persistencia, base de datos.
- Pasarela de pago.
- Formularios que envíen a algún sitio (todos son decorativos).
- Componentes React/Vue/Svelte.
- TypeScript estricto.
- Animaciones gratuitas que ralenticen el móvil.
- Loaders al inicio (innecesarios).
- Modales que cubran la pantalla al entrar (pop-up newsletter, etc.).
- Cookie banners gigantes (uno discreto en footer está bien).
- Lenguaje corporativo vacío.
- Colores fuera de la paleta corporativa (salvo `agronexo-cta` en el FAB de Telegram, que está documentado).

---

## Referencias en `docs/`

- `PROJECT_CONTEXT.md` — persona, journey, líneas, decisiones.
- `agronexo_customer_journey.docx` — customer journey completo en Word.
- `01_journey_map.png` — Journey Map con swimlanes (uso interno TFM, no web).
- `02_service_blueprint.png` — Service Blueprint (uso interno TFM, no web).
- `03_persona_card.png` — Persona card visual de Manuel.
- `04_flywheel.png` — Diagrama del flywheel.
- `chatbot_flow_diagram.mermaid` — flujo del bot Telegram (contexto del lead).

---

## Notas de sesión

[Sección viva: añade aquí decisiones importantes a medida que vayan surgiendo, con fecha y resumen breve.]

- 
