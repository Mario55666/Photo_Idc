# IDC Editor

> Editor de imágenes en línea para el Instituto de Educación Superior Público Diseño y Comunicación (IDC), Lima — Perú.
> Aplicación web progresiva (PWA) de un solo archivo, autocontenida, con identidad institucional.

---

## Índice

1. [Acerca del proyecto](#acerca-del-proyecto)
2. [Características](#características)
3. [Despliegue](#despliegue)
4. [Uso](#uso)
5. [Atajos de teclado](#atajos-de-teclado)
6. [Panel de Acciones](#panel-de-acciones)
7. [Arquitectura técnica](#arquitectura-técnica)
8. [Estructura del repositorio](#estructura-del-repositorio)
9. [Privacidad y datos](#privacidad-y-datos)
10. [Limitaciones conocidas](#limitaciones-conocidas)
11. [Hoja de ruta](#hoja-de-ruta)
12. [Créditos](#créditos)
13. [Licencia](#licencia)

---

## Acerca del proyecto

**IDC Editor** es un editor de imágenes profesional concebido como herramienta pedagógica para los cursos de diseño del IDC. Funciona íntegramente en el navegador del usuario, sin enviar datos a ningún servidor, e instalable como aplicación nativa mediante tecnología PWA.

Inspirado en interfaces como Photoshop y Photopea, ofrece un flujo de trabajo familiar para estudiantes y docentes de diseño gráfico, editorial y comunicación visual, con paneles dedicados a capas, color, historial y acciones, además de ajustes profesionales de imagen como Niveles y Curvas con histograma interactivo.

El proyecto se distribuye como un único archivo HTML de aproximadamente 470 KB que incluye toda la lógica, los estilos, el logotipo institucional y los íconos de la PWA codificados en base64.

---

## Características

### Herramientas (15)

Mover, marco rectangular, lazo, recorte, cuentagotas, pincel con dureza variable, lápiz, borrador, bote de pintura con tolerancia, texto editable, rectángulo, elipse, línea, mano (pan) y zoom.

### Sistema de capas

- Capas ilimitadas con miniatura en vivo de 36×36 px y fondo cuadriculado.
- 16 modos de fusión: Normal, Multiplicar, Trama, Superposición, Oscurecer, Aclarar, Sobreexponer, Subexponer, Luz fuerte, Luz suave, Diferencia, Exclusión, Tono, Saturación, Color y Luminosidad.
- Opacidad ajustable por capa.
- Bloqueo individual de capas (impide pintura y filtros).
- Reordenamiento por arrastrar y soltar.
- Acciones: nueva, duplicar, eliminar, combinar hacia abajo, acoplar imagen.
- Renombrado por doble clic.

### Ajustes y filtros

- **Niveles** con histograma del canal seleccionado (RGB / R / G / B / Luminosidad), control de punto negro, gamma, punto blanco y rango de salida. Botón **Auto** que estira al percentil 0.5–99.5.
- **Curvas** con editor interactivo de 256×256 px, histograma de fondo, puntos de control arrastrables, hasta cuatro canales independientes (RGB compuesto + R + G + B).
- Brillo / Contraste, Tono / Saturación, Posterizar, Umbral.
- Desenfoque gaussiano, Enfocar, Pixelar, Ruido.
- Escala de grises, Sepia, Invertir colores.
- Vista previa en vivo en todos los ajustes con sliders.

### Transformaciones

Tamaño de imagen, tamaño de lienzo (con anclaje configurable), rotación 90°/180°, voltear horizontal y vertical, recortar a selección.

### Panel de Acciones

Sistema completo estilo Photoshop para grabar, reproducir, guardar e intercambiar secuencias de operaciones. Incluye seis presets IDC predefinidos. Detalle en la sección [Panel de Acciones](#panel-de-acciones).

### Historial

30 estados con vista previa textual, navegación libre hacia atrás y adelante, *deshacer* y *rehacer* con `Ctrl+Z` / `Ctrl+Y`.

### Color

Selector de color con previsualización, entrada HEX y RGB, paleta institucional IDC y atajos rápidos para colores frecuentes. Color frontal y de fondo independientes con intercambio rápido (`X`) y restablecimiento (`D`).

### PWA (Progressive Web App)

- Instalable desde el navegador (Chrome, Edge, Brave, Firefox).
- Funciona sin conexión una vez instalada.
- Íconos para escritorio y móvil, incluyendo variante *maskable* con fondo naranja IDC.
- Indicador de conexión en la barra superior.

### Identidad institucional

Paleta IDC aplicada como variables CSS:

| Color | HEX | Uso |
|-------|-----|-----|
| Naranja IDC | `#f3a100` | Acento, color activo, marca |
| Azul IDC | `#0072b9` | Reservado para destacados secundarios |
| Gris IDC | `#555553` | Texto secundario |
| Gris oscuro IDC | `#545452` | Subdivisiones |

Logotipo blanco del IDC en la barra superior y como ícono de la PWA. Tipografía: `system-ui` para interfaz y `JetBrains Mono` para datos numéricos.

### Importar y exportar

- Importar PNG, JPEG, WebP, GIF, BMP por menú o arrastrar y soltar.
- Importar como nueva capa o como documento nuevo.
- Exportar PNG, JPEG (calidad 92), WebP (calidad 92).
- Exportar capa individual.
- Importar y exportar conjuntos de Acciones en formato JSON.

---

## Despliegue

### Opción 1 — Uso local rápido (sin PWA)

Abrir directamente `idc_editor.html` en cualquier navegador moderno haciendo doble clic. La aplicación funciona completamente, salvo el modo offline y la instalación como aplicación, que requieren un servidor.

```
file:///ruta/a/idc_editor.html
```

### Opción 2 — Servidor local (PWA completa)

Para activar la instalación como aplicación y el modo offline:

1. Coloca `idc_editor.html` en una carpeta vacía. Renómbralo a `index.html` si deseas que cargue por defecto.
2. Desde el editor, ve a `Archivo → Descargar Service Worker (PWA)`. Esto descarga `sw.js`. Colócalo en la misma carpeta que el HTML.
3. Desde una terminal, sirve la carpeta:

   ```bash
   # Python 3
   python3 -m http.server 8080
   ```

4. Abre `http://localhost:8080/idc_editor.html` en el navegador.
5. El navegador ofrecerá instalar la aplicación; también aparece el botón **Instalar** en la barra superior.

### Opción 3 — Hosting estático

Sube `idc_editor.html` y `sw.js` al mismo directorio en cualquier hosting estático compatible con HTTPS:

- **GitHub Pages** — recomendado para uso institucional.
- **Netlify**, **Vercel**, **Cloudflare Pages**.
- Servidor propio del IDC con HTTPS.

Una vez en HTTPS, la PWA queda instalable en cualquier dispositivo desde el navegador.

> **Nota técnica.** El Service Worker debe ser un archivo externo (`sw.js`) servido desde el mismo origen que el HTML. Los navegadores modernos rechazan registrar Service Workers desde URLs `blob:` o `data:` por razones de seguridad.

---

## Uso

### Crear un documento

Al abrir la aplicación se muestra automáticamente el diálogo de **Nuevo documento** con presets:

- Personalizado
- Full HD (1920 × 1080)
- A4 a 300 ppp (2480 × 3508)
- Carta a 300 ppp (2550 × 3300)
- Instagram cuadrado (1080 × 1080)
- Instagram historia (1080 × 1920)

### Trabajar con capas

El panel **Capas** ocupa la columna derecha. Cada elemento muestra: ojo de visibilidad, miniatura, nombre y candado.

- **Clic** sobre una capa para activarla.
- **Doble clic** sobre el nombre para renombrarla.
- **Clic en el candado** para bloquear o desbloquear.
- **Arrastrar y soltar** para reordenar.
- Los botones del encabezado del panel: añadir, duplicar y eliminar capa.
- Los controles de **Opacidad** y **Modo de fusión** afectan a la capa activa.

### Aplicar ajustes

Niveles, Curvas y los demás ajustes están en el menú **Filtro**. Todos abren un diálogo modal con vista previa en vivo. *Aplicar* confirma; *Cancelar* revierte sin tocar el historial.

### Selecciones

Las herramientas de marco y lazo crean selecciones que limitan el área editable. Usar `Ctrl+A` para seleccionar todo, `Ctrl+D` para deseleccionar, `Ctrl+C` y `Ctrl+V` para copiar y pegar como nueva capa.

---

## Atajos de teclado

### Herramientas

| Tecla | Herramienta |
|-------|-------------|
| `V` | Mover |
| `M` | Marco rectangular |
| `L` | Lazo |
| `C` | Recortar |
| `I` | Cuentagotas |
| `B` | Pincel |
| `N` | Lápiz |
| `E` | Borrador |
| `G` | Bote de pintura |
| `T` | Texto |
| `U` | Forma |
| `H` | Mano |
| `Z` | Zoom |
| `[` / `]` | Disminuir / aumentar tamaño de pincel |
| `X` | Intercambiar color frontal y de fondo |
| `D` | Restablecer colores por defecto |

### Documento

| Combinación | Acción |
|-------------|--------|
| `Ctrl+N` | Nuevo documento |
| `Ctrl+O` | Abrir imagen |
| `Ctrl+S` | Guardar como PNG |

### Edición

| Combinación | Acción |
|-------------|--------|
| `Ctrl+Z` | Deshacer |
| `Ctrl+Y` | Rehacer |
| `Ctrl+X` | Cortar |
| `Ctrl+C` | Copiar |
| `Ctrl+V` | Pegar como nueva capa |
| `Suprimir` | Borrar selección |

### Selección

| Combinación | Acción |
|-------------|--------|
| `Ctrl+A` | Seleccionar todo |
| `Ctrl+D` | Deseleccionar |

### Capas

| Combinación | Acción |
|-------------|--------|
| `Ctrl+Shift+N` | Nueva capa |
| `Ctrl+J` | Duplicar capa |
| `Ctrl+E` | Combinar hacia abajo |
| `Ctrl+]` | Subir capa |
| `Ctrl+[` | Bajar capa |
| `Ctrl+/` | Bloquear / desbloquear capa |

### Filtros

| Combinación | Acción |
|-------------|--------|
| `Ctrl+L` | Niveles |
| `Ctrl+M` | Curvas |
| `Ctrl+I` | Invertir colores |

### Vista

| Combinación | Acción |
|-------------|--------|
| `Ctrl++` | Acercar |
| `Ctrl+-` | Alejar |
| `Ctrl+0` | Ajustar a pantalla |
| `Ctrl+1` | Píxeles reales (100%) |
| `Espacio` | Mano temporal (mientras se mantiene presionada) |
| `F11` | Pantalla completa |
| `?` | Ver todos los atajos |

---

## Panel de Acciones

El panel de Acciones, ubicado en la columna derecha, replica el flujo del panel homónimo de Photoshop y permite automatizar tareas repetitivas: especialmente útil para procesar lotes de imágenes con el mismo tratamiento o demostrar paso a paso un proceso a estudiantes.

### Conceptos

- **Conjunto**: carpeta que agrupa acciones relacionadas (por ejemplo, "Presets IDC").
- **Acción**: secuencia de pasos con un nombre.
- **Paso**: una operación individual con sus parámetros.

### Operaciones

Pulsar **●** para grabar, **■** para detener, **▶** para reproducir la selección. El botón **⊞** alterna el modo botón, una grilla de botones grandes ideal para uso en clase.

Los pasos individuales pueden activarse o desactivarse con la casilla a la izquierda sin necesidad de eliminarlos.

### Presets IDC incluidos

| Acción | Pasos |
|--------|-------|
| Optimizar para web (JPG) | Redimensionar a 1920 × 1080, enfocar, exportar JPG |
| B/N editorial | Escala de grises, contraste +25 |
| Sepia vintage | Sepia, brillo +10 contraste +15, ruido 8 |
| Alto contraste duotono | Escala de grises, umbral 128 |
| Pixel-art ×8 | Pixelar 8, posterizar 4 niveles |
| Cuadrado Instagram (1080) | Tamaño de lienzo 1080 × 1080 centrado |

### Persistencia

Las acciones se guardan automáticamente en `localStorage` bajo la clave `idc_editor_actions_v1`. Para compartir entre dispositivos o con estudiantes, usar **Exportar** (genera `idc-acciones.json`) e **Importar**. La importación añade conjuntos a los existentes sin reemplazarlos.

### Operaciones reproducibles

Aproximadamente 30 operaciones son grabables: todos los filtros (con sus parámetros exactos), transformaciones (rotar, voltear, redimensionar imagen y lienzo, recortar), operaciones de capa (nueva, duplicar, eliminar, mover, combinar, bloquear), selección (todo, deseleccionar), rellenos y exportaciones (PNG, JPG, WebP).

Las operaciones que dependen de gestos puntuales (trazos de pincel, posiciones específicas) **no son grabables**, lo cual es coherente con el propósito de las acciones como flujo de tratamiento por lotes.

---

## Arquitectura técnica

### Stack

- HTML5 con Canvas API estándar.
- CSS3 con custom properties para temizar.
- JavaScript ES2020 *vanilla* (sin frameworks ni dependencias externas).
- Service Worker API para la PWA.
- LocalStorage para persistencia de acciones.

### Diseño de un solo archivo

El archivo final `idc_editor.html` es completamente autocontenido:

- HTML, CSS y JavaScript inlineados en un único documento.
- Logotipo IDC e íconos PWA codificados como `data:image/png;base64,...`.
- Web App Manifest inlineado como `data:application/manifest+json;base64,...`.
- Sin peticiones de red, sin CDN, sin dependencias externas.

Esto garantiza portabilidad total y supervivencia del recurso a largo plazo: el archivo es el proyecto entero.

### Service Worker

`sw.js` se sirve como archivo externo (requisito de los navegadores modernos). Implementa una estrategia *cache-first* que precachea la aplicación al instalar y responde con la versión cacheada en visitas subsecuentes, garantizando funcionamiento offline. El cache se identifica por la clave `idc-editor-v1`.

### Renderizado

Cada capa es un `<canvas>` independiente con su propio contexto 2D. La función `redraw()` compone las capas en orden, aplicando opacidad y modo de fusión por capa mediante `globalAlpha` y `globalCompositeOperation`. La selección se renderiza en un canvas overlay con animación de *marching ants*.

### Algoritmos relevantes

- **Bote de pintura**: *flood fill* por escaneo de líneas con tolerancia configurable.
- **Niveles**: precomputo de LUT (look-up table) de 256 entradas por canal, luego iteración lineal sobre los píxeles.
- **Curvas**: LUT generada por interpolación lineal entre puntos de control ordenados.
- **Histograma**: tres arrays `Uint32Array(256)` para R/G/B más uno para luma calculada con coeficientes ITU-R BT.601.
- **Desenfoque**: caja en dos pasadas (horizontal y vertical) para aproximación rápida del gaussiano.

### Tamaño y rendimiento

El archivo final pesa aproximadamente 470 KB sin comprimir. Comprimido con gzip baja a unos 130 KB. Carga inicial inferior a 200 ms en conexión local. Las operaciones por píxel se realizan sobre `Uint8ClampedArray` para evitar conversiones de tipo.

---

## Estructura del repositorio

```
idc-editor/
├── idc_editor.html          # Aplicación completa (entregable)
├── sw.js                    # Service Worker para PWA
├── README.md                # Este archivo
├── docs/                    # Documentación adicional (opcional)
│   ├── shortcuts.pdf
│   └── teaching-guide.md
└── src/                     # Fuentes de desarrollo (opcional)
    ├── part_html.html
    ├── part_css.css
    ├── part_js.js
    ├── part_sw.js
    └── build.py             # Ensambla el archivo final
```

Para producción solo son necesarios `idc_editor.html` y `sw.js` en el mismo directorio.

---

## Privacidad y datos

- **Cero telemetría**. La aplicación no envía absolutamente ningún dato a servidores externos.
- **Procesamiento local**. Todas las imágenes se procesan en el navegador del usuario.
- **Sin cuentas**. No requiere registro ni autenticación.
- **Almacenamiento local**. Solo se utiliza `localStorage` para guardar las acciones del usuario, en su propio dispositivo.
- **Cookies**. No se utilizan.
- **Service Worker**. Solo cachea los archivos de la propia aplicación; no intercepta ni registra navegación a otros sitios.

Esto hace al editor adecuado para uso académico con estudiantes menores de edad y para entornos institucionales con políticas estrictas de protección de datos.

---

## Limitaciones conocidas

- La selección invertida requiere implementación de máscara avanzada (pendiente).
- El bote de pintura usa *scanline fill* sin antialiasing en bordes; bordes suaves se ven escalonados.
- El texto se renderiza como mapa de bits al confirmar; no es editable después como vector.
- No existen capas de ajuste no destructivas; los filtros se aplican directamente al canvas de la capa.
- El bloqueo de capa es total (no separa lock de transparencia, posición o pixeles como Photoshop).
- Las acciones no graban gestos individuales (trazos de pincel, clics de cuentagotas).
- Las imágenes de gran tamaño (más de 4096 × 4096 px) pueden ralentizar filtros como Desenfoque por la cantidad de operaciones por píxel.
- El historial está limitado a 30 estados para mantener el uso de memoria razonable.

---

## Hoja de ruta

Funciones consideradas para versiones futuras, sin compromiso de fechas:

- Selección invertida con máscara real basada en `ImageData`.
- Capas de ajuste no destructivas (Niveles, Curvas, Tono/Saturación).
- Máscaras de capa.
- Texto editable persistente como objeto vectorial.
- Herramienta de varita mágica.
- Modo de regla y guías personalizadas.
- Exportación SVG de las formas vectoriales.
- Plantillas IDC predefinidas para entregas académicas (caratulas, diagramaciones).
- Integración opcional con generación de imágenes por IA mediante el menú IA ya presente.

---

## Créditos

**Desarrollo, diseño y dirección**
Mg. Mario Rafael Quiroz Martínez
Profesor de Tipografía, Semiótica de la Imagen, Diseño de Información y Diseño Editorial — Universidad Tecnológica del Perú (UTP)
Coordinador e investigador — Instituto de Educación Superior Público Diseño y Comunicación (IDC)

**Identidad de marca**
d3magindesign

**Institución**
Instituto de Educación Superior Público Diseño y Comunicación
Lima, Perú

**Contacto**
c12139@utp.edu.pe

---

## Licencia

Este proyecto se distribuye con fines educativos para uso interno del Instituto de Educación Superior Público Diseño y Comunicación, sus estudiantes, docentes y comunidad académica vinculada.

Para usos distintos al académico, distribución pública con modificaciones, o integración en productos comerciales, contactar al autor a través del correo institucional.

El logotipo del IDC y la identidad d3magindesign son marcas reservadas y no se transfieren bajo esta licencia.

---

<sub>**IDC Editor** · Construido con Canvas API estándar · Sin frameworks · Sin dependencias · Sin telemetría</sub>
