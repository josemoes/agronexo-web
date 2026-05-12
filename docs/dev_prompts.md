# Guía de prompts · Construir la web de AgroNexo con Claude Code

> Orden recomendado de trabajo. Cada paso es una sesión de Claude Code.
> Antes de empezar cada paso, asegúrate de tener guardados los cambios anteriores (commit).
> Los prompts están redactados para copiar y pegar directamente.

---

## Paso 0 · Setup de branding en el repo

**Acciones manuales antes de Claude Code:**

1. Mueve el `logo.png` que descargaste a `agronexo-web/public/logo.png`.
2. Mueve el `branding_agronexo.pdf` a `agronexo-web/docs/`.
3. Sustituye el `CLAUDE.md` antiguo por el nuevo (versión 3, con el branding integrado).
4. Haz un commit: `chore: add branding assets`.

**Prompt en Claude Code:**

> He actualizado el CLAUDE.md con el branding real de la marca. Léelo de nuevo entero, junto con docs/PROJECT_CONTEXT.md. Cuando termines, confírmame que has entendido:
>
> 1. La paleta corporativa real (5 colores) y cómo se usa cada uno.
> 2. Las dos tipografías y su escala.
> 3. El tagline y el tono de voz.
> 4. La inspiración estructural de carmowood.com.
>
> No generes código todavía.

**Qué revisar:** que reconoce los 5 hex codes correctos y nombra Montserrat + DM Sans. Si dice algún color de la paleta antigua del journey, redirígelo.

---

## Paso 1 · Sistema de diseño + BaseLayout + Header + Footer

Aquí construimos las piezas que aparecen en todas las páginas. Es el "esqueleto" de la web.

**Prompt en Claude Code:**

> Vamos a montar el sistema de diseño y los componentes compartidos. En este orden:
>
> 1. Configura `tailwind.config.mjs` con la paleta corporativa (agronexo-dark, agronexo-olive, agronexo-text, agronexo-warm, agronexo-bg) y las dos fuentes (Montserrat para display, DM Sans para body). Ver CLAUDE.md sección "Paleta corporativa" y "Tipografías".
> 2. Crea `src/styles/global.css` con los estilos base: reset, smooth scroll, selección de texto en verde oliva, scrollbar discreto. Importa las fuentes desde Google Fonts con `display=swap` y solo los pesos que vamos a usar.
> 3. Crea `src/layouts/BaseLayout.astro` con `<head>` completo (meta tags, viewport, fuentes precargadas, favicon placeholder) y los slots para Header, contenido y Footer.
> 4. Crea `src/components/Header.astro` con:
>    - Logo a la izquierda (alto 36px móvil, 44px desktop), referencia /logo.png
>    - Navegación con los 6 links: Inicio, Productos, Servicios, Asesoramiento, Fincas, Contacto
>    - En móvil, el menú colapsa a un hamburguesa con `<details>` (sin JS)
>    - Fondo blanco con sombra muy sutil al hacer scroll (CSS-only con backdrop-filter si se puede)
> 5. Crea `src/components/Footer.astro` estilo carmowood:
>    - Fondo verde oscuro (#193b29)
>    - Tagline gigante "Del dato a la rentabilidad agrícola" en Montserrat blanco
>    - 3 columnas debajo: AgroNexo (líneas), Empresa (sobre, contacto), Legal (aviso legal, privacidad, cookies)
>    - Logo en blanco arriba a la izquierda (por ahora usa /logo.png; reemplazaremos por versión blanca cuando la tengamos)
>    - Copyright al final
> 6. Modifica `src/pages/index.astro` para que use BaseLayout y muestre solo "Home en construcción" temporalmente, así podemos ver el header/footer en localhost.
>
> Antes de empezar, dame un mini plan de archivos que vas a tocar y espera mi visto bueno.

**Qué revisar después:**
- Header se ve limpio en móvil y desktop, el menú colapsa correctamente sin JS.
- Footer tiene presencia y el tagline se lee bien.
- Las fuentes Montserrat y DM Sans se aplican (verifica abriendo Inspector y mirando el computed font-family).
- Los colores son los exactos del branding.

**Iteraciones probables:**
- Espaciado del Header demasiado apretado o demasiado generoso.
- Logo mal proporcionado en móvil.
- Tagline del Footer demasiado grande o pequeño.

**Cuando estés contento → commit:** `feat: add base layout, header and footer`.

---

## Paso 2 · Home

La pieza clave. Define el feel de toda la web. Aquí merece la pena iterar varias veces.

**Prompt en Claude Code:**

> Vamos a construir la Home. Antes de generar código, dame un plan de secciones en este formato:
>
> "Sección 1: [nombre] — [qué contiene] — [color dominante]"
>
> Mi propuesta inicial es:
>
> 1. Hero pantalla completa con imagen de fondo de olivar (de momento usa placeholder de unsplash.com/photos directamente como background-image: `url('https://images.unsplash.com/photo-...')`, busca un olive grove panorámico), título grande "Del dato a la rentabilidad agrícola", subtítulo de una línea, dos CTAs (uno primario "Descubre AgroNexo" y uno secundario "Habla con un asesor").
> 2. Sección "Quiénes somos" con storytelling estilo carmowood: párrafo poético conectando tradición y tecnología. Texto a la izquierda, foto a la derecha (otro placeholder unsplash: foto de manos de agricultor o aceitunas).
> 3. Sección "Tres líneas, un mismo nexo": tres cards grandes en grid (1 columna en móvil, 3 en desktop). Cada card: icono, nombre de la línea (Productos / Servicios / Arrendamientos), descripción de 2 líneas, link "Conoce más →".
> 4. Sección "Casos" estilo Carmowood: 4 cards de fincas con foto, categoría (Olivar / Almendro / Viñedo), ubicación (Loja, Antequera, etc.) y nombre del proyecto. Inventados pero verosímiles para Granada/Andalucía.
> 5. CTA final: banda verde oscuro con tagline + botón "Habla con AgroNexo" que lleva a /contacto.
>
> Si crees que sobra o falta algo, dímelo. Cuando esté validado, generamos el código componente por componente. No hace falta crear un componente para cada sección si solo se usa en la home, puedes meter la sección directamente en index.astro.

**Qué revisar después:**
- El hero se ve impactante en móvil y desktop, el texto se lee bien sobre la imagen (probablemente necesitará un overlay oscuro).
- El storytelling tiene tono adecuado (poético pero no cursi, conectado al campo).
- Las tres cards de líneas se ven equilibradas y diferenciadas.
- Los casos tienen buena pinta visual.
- El CTA final tiene fuerza.

**Iteraciones probables (muy comunes en home):**
- Cambiar la imagen del hero (probar varias hasta dar con una).
- Ajustar el contraste del overlay del hero.
- Reescribir el copy del storytelling (puedes pedirme a mí ese copy, te lo doy yo en el chat web y se lo pegas a Claude Code).
- Pulir el espaciado entre secciones.

**Cuando estés contento → commit:** `feat: home page first version`.

---

## Paso 3 · Productos (página piloto de una línea)

Una sola página de línea para validar el patrón antes de replicarlo a las otras dos.

**Prompt en Claude Code:**

> Vamos a construir /productos. Esta es nuestra página piloto de "página de línea" — el patrón que aplicaremos también a /servicios y /fincas, así que merece la pena pulirlo bien.
>
> Antes de código, dame el plan de secciones. Mi propuesta:
>
> 1. Hero más contenido que la home: imagen de fondo a media altura con texto encima, título "Productos para tu olivar", subtítulo de una frase, breadcrumb opcional.
> 2. Intro: párrafo de 2-3 líneas explicando qué tipo de productos vende AgroNexo (intermediación con compra directa, calidad seleccionada, recomendados según diagnóstico).
> 3. Grid de productos: 4 cards (melaza, hidroinfiltrador, nitrato potásico, urea). Cada card:
>    - Imagen del producto (placeholder gris o stock unsplash)
>    - Nombre del producto
>    - Descripción corta de 1-2 líneas
>    - Etiqueta del beneficio principal (ej: "Mejora la vida del suelo")
>    - Botón decorativo "Solicita información" que lleva a /contacto
>    En móvil 1 columna, en desktop 2 columnas, alternando alineación si queda elegante.
> 4. Sección "Cómo lo comprarás": 3 pasos visuales (1. Habla con AgroNexo → 2. Recibe recomendación personalizada → 3. Pídelo y te llega a la finca). Cada paso un número grande, título, descripción corta.
> 5. CTA final: "¿Quieres saber qué producto le va mejor a tu finca?" con botón a /asesoramiento.
>
> Reutiliza el componente ProductCard si tiene sentido. Si solo se usa en /productos, mételo inline en la página.

**Contenido sugerido para las cards de producto:**

- **Melaza** · "Alimenta la vida del suelo y mejora la asimilación de nutrientes. Ideal como complemento en agricultura ecológica." · Beneficio: "Suelo más vivo"
- **Hidroinfiltrador** · "Sistema patentado por la UGR que lleva el agua directamente a la raíz. Reduce el consumo y mejora la eficiencia hídrica." · Beneficio: "Ahorro de agua"
- **Nitrato potásico** · "Fertilizante de alta solubilidad para la fase de cuajado y engorde del fruto. Liberación inmediata." · Beneficio: "Más calibre"
- **Urea** · "Aporte nitrogenado de larga duración para el desarrollo vegetativo. Versátil y económico." · Beneficio: "Crecimiento robusto"

**Qué revisar después:**
- La página se siente parte del mismo mundo que la home (paleta, tipografía, espaciados coherentes).
- Las cards de producto son atractivas y comunican bien el beneficio.
- El patrón es replicable a servicios y fincas sin forzar.

**Cuando estés contento → commit:** `feat: productos page`.

---

## Paso 4 · Iteración crítica · STOP y revisión

**No empieces a generar las otras páginas todavía.** Pausa.

Abre `localhost:4321/` y `localhost:4321/productos` y míralas juntas:

- ¿Sigue la misma identidad visual?
- ¿La altura del hero es proporcional entre páginas?
- ¿Los espaciados entre secciones son consistentes?
- ¿La tipografía se siente coherente?
- ¿Los botones tienen siempre el mismo estilo?
- ¿Algún componente que repites entre Home y Productos podría extraerse a `src/components/` para reutilizar?

**Prompt en Claude Code:**

> Antes de seguir con las otras páginas, hagamos una pasada de coherencia. Mira la Home y /productos en paralelo y dime:
>
> 1. ¿Hay inconsistencias visuales entre las dos páginas? (espaciados, tamaños de heading, paleta).
> 2. ¿Hay piezas de código que se repiten y deberíamos extraer a componentes reutilizables?
> 3. ¿La altura de los heros es coherente y la jerarquía visual funciona?
> 4. ¿Algo que mejorarías antes de duplicar este patrón en /servicios y /fincas?
>
> Dame solo el análisis. Después decidimos qué cambiar.

**Si te propone cambios sensatos, aplícalos antes de seguir.** El coste de pulir aquí es bajo. El coste de pulir después de replicar a 3 páginas es triple.

**Commit:** `refactor: extract shared components and align spacing`.

---

## Paso 5 · Servicios, Fincas y Asesoramiento

Aplica el patrón validado de /productos a estas tres landings. Cada una con su matiz.

**Prompt en Claude Code (servicios):**

> Construye /servicios siguiendo el mismo patrón estructural de /productos. Diferencias importantes:
>
> 1. Hero con título "Servicios para tu finca" + subtítulo "Desde una poda puntual hasta un plan integral de optimización".
> 2. Intro distinguiendo dos tipos de servicio.
> 3. Sección "Servicios puntuales": 3 cards (Poda, Análisis de suelo, Visita técnica). Estilo similar a las cards de productos.
> 4. Sección "Servicios integrales: AgroNexo Advisory": 5 pasos en formato horizontal scrollable o vertical en móvil, con SCAN → DESIGN → DEPLOY → CONTROL → FUNDING. Cada paso: título, una línea de descripción, icono o número grande.
> 5. CTA final: "¿No sabes cuál encaja con tu finca?" con botón a /asesoramiento.
>
> Dame el plan antes de generar. Reutiliza componentes que ya tengamos.

**Prompt en Claude Code (fincas):**

> Construye /fincas. Es la landing del paquete completo de arrendamiento — más larga y narrativa que las otras, porque vende confianza, no producto.
>
> Plan propuesto:
>
> 1. Hero con foto de paisaje de olivar abandonado o infrautilizado + título "Tu finca, cuidada. Tu renta, garantizada." + subtítulo de una línea.
> 2. Sección "¿Tienes tierras que no estás aprovechando?": párrafo emocional dirigido a Manuel, con foto de manos sobre tierra a la derecha.
> 3. Sección "Qué hace AgroNexo FINCAS por ti": 4 bloques (Evaluación técnica → Diseño productivo → Búsqueda del explotador → Acompañamiento contractual).
> 4. Sección "Caso real" (decorativo): un caso ejemplo de finca activada, con foto, datos resumidos y un quote del propietario inventado pero verosímil.
> 5. CTA final: "Cuéntanos qué finca tienes y la valoramos sin compromiso" + botón a /contacto.
>
> Plan antes del código.

**Prompt en Claude Code (asesoramiento):**

> Construye /asesoramiento. Es la landing del estudio a medida — más corta y directa que /fincas, más comercial.
>
> Plan propuesto:
>
> 1. Hero con título "Un estudio hecho para tu olivar" + subtítulo.
> 2. Sección "¿Qué incluye el asesoramiento?": lista de 5-6 puntos (visita técnica, análisis de riego, plan de mejora, identificación de subvenciones, etc.).
> 3. Sección "Cómo funciona": 3 pasos visuales similares a los de /productos.
> 4. Sección "Por qué confiar en nosotros": 3 razones cortas con iconos.
> 5. CTA final: "Reserva tu primera visita" + botón a /contacto.
>
> Plan antes del código.

**Commits:**
- `feat: servicios page`
- `feat: fincas page`
- `feat: asesoramiento page`

---

## Paso 6 · Contacto + páginas legales

Lo más rápido del proceso, porque ya tenemos todos los patrones.

**Prompt en Claude Code:**

> Construye /contacto y las páginas legales mínimas.
>
> /contacto:
> - Hero pequeño con título "Hablemos de tu olivar" + subtítulo.
> - Dos columnas: a la izquierda formulario decorativo (nombre, email, teléfono, tipo de consulta como select, mensaje, botón "Enviar" que no hace nada o muestra un mensaje "Esta es una demo del prototipo TFM"). A la derecha, datos de contacto: email, teléfono, ubicación (Granada), enlaces a redes sociales (placeholders).
> - Mapa decorativo opcional con embed estático de Granada (sin Google Maps real, una imagen estática es suficiente).
>
> Páginas legales mínimas (en /legal/*):
> - /legal/aviso-legal
> - /legal/privacidad
> - /legal/cookies
>
> Para estas tres, plantilla mínima: BaseLayout + título + texto placeholder genérico de un párrafo explicando que es un prototipo TFM y que el contenido legal real se desarrollaría en producción.
>
> Actualiza el Footer para que los links a estas páginas funcionen.
>
> Plan antes del código.

**Commit:** `feat: contacto and legal pages`.

---

## Paso 7 · Pulido global

Pasada final. Esto es lo que diferencia un prototipo decente de uno que defiende bien.

**Prompt en Claude Code:**

> Hagamos una pasada de pulido global. Quiero que revises y mejores:
>
> 1. **Responsive**: abre cada página y dime cómo se ve en breakpoints clave (375px iPhone, 768px tablet, 1280px laptop, 1920px monitor). Identifica problemas concretos y arréglalos.
> 2. **Accesibilidad básica**: contraste de texto (WCAG AA mínimo), alt en todas las imágenes, focus visible en todos los elementos interactivos, jerarquía correcta de headings (un solo h1 por página).
> 3. **SEO básico**: title y meta description únicos por página, og:image en BaseLayout, lang="es" en html.
> 4. **Performance**: lazy loading en imágenes que están below the fold, fuentes con display=swap, ningún CSS-in-JS innecesario.
> 5. **Microinteracciones CSS-only**: hover en cards (lift sutil + sombra), focus ring en links, transición suave de color en botones, smooth scroll para anclas internas.
> 6. **Favicon**: genera un favicon simple a partir del logo, o pídeme que te lo prepare yo si no puedes.
>
> Dame un informe de lo que has encontrado antes de tocar nada. Luego decidimos qué arreglar en qué orden.

**Commit:** `polish: responsive, a11y, seo and microinteractions`.

---

## Cuándo pedirme cosas a mí (en el chat web de Claude.ai)

Hay cosas que tiene más sentido pedirme a mí que a Claude Code:

- **Copy/contenido** de cualquier sección (yo tengo el contexto del journey y la voz de Manuel).
- **Decisiones estratégicas** ("¿debo añadir una sección de testimonios o no?").
- **Recomendaciones de imágenes** (búsquedas concretas en Unsplash).
- **Microcopy** de botones, errores, formularios.
- **Iconografía** (qué iconos lucide encajan con cada concepto).

Para todo lo que sea ejecutar código, Claude Code.

---

## Atajo: cómo pedir contenido sin gastar tokens en Claude Code

Cuando le pidas a Claude Code que monte una página y haya texto que escribir, **pásale el copy listo en el prompt**. Así no improvisa y no gasta tokens generando opciones.

Para conseguir ese copy listo: me lo pides aquí en el chat web ("dame el copy del hero de la home, 3 versiones para elegir") y me das una vuelta. Luego pegas la versión elegida en el prompt de Claude Code. Mucho más eficiente.

---

## Resumen de los 7 pasos

| Paso | Qué se hace | Sesión típica | Iteraciones esperadas |
|---|---|---|---|
| 0 | Setup branding | 10 min | 0 |
| 1 | Layout + Header + Footer | 1-2 h | 2-3 |
| 2 | Home | 2-3 h | 3-5 (es la pieza clave) |
| 3 | Productos (piloto) | 1 h | 1-2 |
| 4 | Iteración crítica | 30 min | — |
| 5 | Servicios + Fincas + Asesoramiento | 1-2 h cada una | 1 cada una |
| 6 | Contacto + legales | 1 h | 1 |
| 7 | Pulido global | 1-2 h | varias rondas |

Total estimado: 10-15 horas de trabajo distribuidas a tu ritmo.
