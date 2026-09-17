# Auditoría de accesibilidad, UX y diseño responsive

## 1. Resumen ejecutivo

Se revisaron los archivos [index.html](index.html) y [styles.css](styles.css) con criterio de WCAG 2.2 AA, UX y diseño responsive. La estructura general es simple, clara y consistente con un enfoque mobile-first. No se detectaron problemas críticos de semántica ni de navegación por teclado en el código actual, porque la página no presenta elementos interactivos (botones, enlaces, formularios ni controles complejos) ni imágenes con contenido informativo.

Los aspectos que cumplen con buen nivel son:

- Estructura semántica: hay uso correcto de `header`, `main` y `footer` en [index.html](index.html#L10-L35).
- Jerarquía de encabezados: existe un solo `h1` y tres `h2`, con una jerarquía clara y sin saltos evidentes en [index.html](index.html#L11-L29).
- Textos alternativos: no hay imágenes, por lo que no hay `img` sin `alt` ni requisitos de `alt` aplicables.
- Nombres accesibles: el contenido textual es descriptivo y no depende de iconos sin texto.
- ARIA: no se usan atributos `aria-*` ni elementos complejos que requieran roles adicionales.
- Responsive: el CSS define una base mobile-first con una sola columna y una media query para pantallas mayores en [styles.css](styles.css#L19-L48).
- Prevención de overflow: no hay elementos con ancho fijo problemático o contenido desbordante a simple vista en los estilos revisados.

No obstante, debe destacarse que no existe un archivo JavaScript en el proyecto, por lo que no se puede evaluar comportamiento dinámico ni errores de script. La página es estática y no presenta lógica de interacción compleja.

## 2. Hallazgos críticos, altos, medios y bajos

### Críticos

- Ninguno verificado.

### Altos

- Ninguno verificado.

### Medios

- Falta de archivo JavaScript para evaluar comportamiento dinámico. La página es estática y, por tanto, no se puede verificar validación ni interactividad del lado del cliente.

### Bajos

- La capacidad de foco visible no puede evaluarse de forma útil porque no hay controles interactivos ni enlaces en la página.
- No hay un mecanismo de navegación por teclado más allá del comportamiento estándar del navegador, ya que no se definen elementos accionables por teclado.
- La página no implementa una experiencia de navegación real para móvil (nav, menú, tabs, filtros, etc.), pero tampoco presenta una navegación compleja que requiera patrones especiales.

## 3. Evidencia concreta

### [index.html](index.html) 

- Estructura principal: `header`, `main`, `footer` correctamente usados en [index.html](index.html#L10-L35).
- Jerarquía de encabezados: `h1` y `h2` bien ordenados en [index.html](index.html#L11-L29).
- Ausencia de imágenes: no hay elementos `img` ni `picture` en [index.html](index.html#L15-L29).
- Ausencia de botones y enlaces: no hay `button`, `a`, `input`, `select`, `textarea` ni `form` en [index.html](index.html#L15-L29).
- Semántica de artículos: el contenido de cada servicio se presenta como `article` dentro de una lista visual de tarjetas en [index.html](index.html#L16-L29).

### [styles.css](styles.css)

- Base mobile-first: `.galeria` inicia con una sola columna y luego cambia a tres columnas con media query en [styles.css](styles.css#L31-L48).
- Reset de caja: `box-sizing: border-box` en [styles.css](styles.css#L1-L4).
- Contraste general: `body` usa texto oscuro sobre fondo claro y `header`/`footer` usan fondo oscuro con texto claro en [styles.css](styles.css#L6-L18).
- Foco visible: no se define estilo `:focus` ni `:focus-visible`, lo que es aceptable en este caso porque no hay controles interactivos.
- Responsive y tamaño táctil: los elementos no son botones ni enlaces; las tarjetas están diseñadas con padding y contenido textual, con un tamaño general razonable para lectura y toque.
- Sin overflow horizontal evidenciado: el ancho del contenedor usa `max-width: 1000px` y `padding` con `box-sizing: border-box` en [styles.css](styles.css#L10-L18), sin anchos fijos problemáticos.
- Modo oscuro: `@media (prefers-color-scheme: dark)` en [styles.css](styles.css#L49-L58) ajusta colores, pero no se valida visualmente si el contraste sigue siendo adecuado en cada resolución.

## 4. Recomendación de corrección

### Hallazgos medidos

1. Falta de archivo JavaScript
   - Recomendación: si la intención es agregar interactividad, crear un archivo JavaScript con lógica explícita y probar su carga desde el HTML. Si la página debe permanecer estática, mantener la implementación actual y documentar que no requiere JS.

### Recomendaciones preventivas generales

- Mantener la estructura semántica actual: `header`, `main`, `footer`, `article` y `h1/h2` son adecuadas para una landing simple.
- Si se agregan enlaces o botones, definir estilos visibles de foco con `:focus` y `:focus-visible` para cumplir con WCAG 2.2 AA.
- Si se agregan imágenes, usar `alt` descriptivo y evitar texto embebido en imágenes cuando sea información esencial.
- Si se agregan interacción, validar teclado, estados de hover/focus y tamaños táctiles mínimos de 44x44 CSS px.
- Repetir validación visual y de accesibilidad en navegadores móviles reales para 320 px, 398 px, 768 px y escritorio.

## 5. Pruebas que deberían repetirse después de corregir los problemas

1. Verificación de HTML semántico
   - Validar el documento en un validador HTML.
   - Confirmar que no haya elementos de estructura mal anidados.

2. Verificación de encabezados
   - Revisar que exista un solo `h1` y que los niveles `h2`/`h3` sigan una jerarquía lógica.

3. Verificación de accesibilidad con teclado
   - Tabular por toda la página y comprobar que no haya elementos que queden inaccesibles.
   - Confirmar que cada control tenga foco visible.

4. Verificación de contrastes
   - Comprobar WCAG AA en textos normales y grandes.
   - Revisar modo claro y oscuro si se implementa.

5. Verificación responsive
   - Validar visualmente en 320 px, 398 px, 768 px y escritorio.
   - Confirmar que no haya desbordamiento horizontal ni elementos cortados.

6. Verificación táctil
   - Comprobar que los objetivos interactivos tengan al menos 44x44 px y sean fáciles de pulsar.

7. Verificación de imágenes
   - Si se agregan imágenes, confirmar que todas tengan `alt` correcto y que no exista contenido importante sin texto alternativo.

8. Verificación de JavaScript
   - Cuando exista archivo JavaScript, ejecutar `node --check` o la herramienta equivalente para verificar sintaxis.
   - Probar eventos, render y no producir errores en consola.

## Criterios que cumplen

- Estructura semántica: cumple.
- Jerarquía de encabezados: cumple.
- Nombres accesibles: cumple por ausencia de elementos complejos y por texto claro.
- Textos alternativos: cumple por ausencia de imágenes.
- Contraste de colores: cumple en la base clara y con dark mode razonablemente, aunque se recomienda comprobación visual específica.
- Navegación por teclado: cumple en el sentido de que no hay controles que requieran interacción, no obstante no existe una navegación compleja que deba validarse.
- Foco visible: no aplica a la estructura actual; no se detectan controles con foco.
- Botones y enlaces: no aplica; no existen elementos interactivos.
- ARIA: cumple porque no se usa de forma innecesaria.
- Tamaño táctil: no aplica a la estructura actual; no existen controles interactivos.
- Navegación móvil: cumple de manera básica para una página estática con diseño responsive simple.
- Overflow horizontal: no se detecta por inspección del código.
- Imágenes: cumple por ausencia de elementos `img`.
- JavaScript: no aplica porque no hay archivo JavaScript en el proyecto.

## Conclusión

La página actual es una implementación estática y minimalista con buena semántica HTML y un responsive básico. No se detectan hallazgos críticos ni altos en el código inspeccionado. Lo principal a monitorear es que, si se quiere ampliar la funcionalidad, se deben agregar pruebas de foco, contraste, teclado y responsive con elementos interactivos reales.
