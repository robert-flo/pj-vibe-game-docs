---
title: 5. Validación y Corrección de Bugs
description: "Metodología de pruebas WebGL y bitácora completa de 9 bugs reales diagnosticados y resueltos durante el proceso."
layout: default
nav_order: 5
permalink: /docs/validacion/
---

# 5. Validación y Corrección de Bugs

## 🧪 Metodología de Pruebas Empíricas y Automatizadas

Para validar que cada iteración funcionara de verdad (y no solo compilara sin errores sintácticos), se combinaron pruebas interactivas con capturas deterministas desde el motor en ejecución:

1. **Verificación Visual Automatizada con WebGL Headless (`scripts/shot.sh`)**:
   * Ejecución de Chromium headless con `--use-gl=angle --use-angle=swiftshader` apuntando a parámetros de diagnóstico (`?scene=6&pos=x,y,z&cam=cx,cy,cz,tx,ty,tz`).
   * Cada ajuste de geometría, UVs, interfaz o físicas se inspeccionó visualmente en capturas reales antes de dar por cerrado un commit.
2. **Inspección de Consola y Niveles Acústicos (`ffmpeg volumedetect`)**:
   * Verificación de cero excepciones JavaScript/GLSL en consola y medición de niveles RMS/pico (`-22.9 dB` medio / `-1.4 dB` pico) en todos los archivos MP3 generados.
3. **Pruebas de Frontera Espacial y Colisiones**:
   * Validación de pendientes, barandillas, troncos de los 26 árboles, caída al agua del foso (*respawn* seguro junto a la tubería verde) y activación exacta en el umbral del pórtico (`Z ∈ [-32.2, -28.8], Y > 7.2`).

---

## 🐛 Bitácora Histórica de Errores Reales Diagnosticados y Resueltos

### Error 1: Salto Infinito en el Aire (*Air-Jumping*) — Fase Inicial
* **Descripción del fallo**: Al pulsar repetidamente `Espacio` durante la caída, el personaje volvía a impulsarse en el aire indefinidamente.
* **Causa técnica**: No se exigía contacto efectivo con el suelo (`isGrounded === true`) antes de asignar `velocityY = JUMP_FORCE`.
* **Solución aplicada**:
  ```javascript
  if (keys['Space'] && isGrounded) {
    velocityY = JUMP_FORCE;
    isGrounded = false;
    playMarioVoice();
  }
  ```

### Error 2: Bloqueo de Autoplay del `AudioContext` en Navegadores Modernos
* **Descripción del fallo**: Advertencia `The AudioContext was not allowed to start. It must be resumed after a user gesture on the page`.
* **Causa técnica**: Las políticas de reproducción automática bloquean el audio hasta el primer gesto explícito del usuario.
* **Solución aplicada**: Inicialización y `ctx.resume()` diferidos al primer evento `keydown` o `mousedown`, con `.play().catch(...)` de respaldo hacia el sintetizador `RetroAudio`.

### Error 3: "Uncanny Valley" y Rotación Descentrada en la Cabeza 3D (Escena 2)
* **Descripción del fallo**: En las primeras pruebas de la Escena 2, proyectar una fotografía plana sobre una esfera producía deformación grotesca, y al migrar al busto 3D la rotación giraba alrededor de la base del cuello en lugar del centro craneal.
* **Causa técnica**: El origen local de la malla exportada no coincidía con el eje anatómico de giro y la luz direccional dura acentuaba sombras faciales oscuras.
* **Solución aplicada**: Se diezmó el modelo de alta densidad de 1.95M a 35k polígonos en Blender conservando UVs, se anidó dentro de un nodo jerárquico `headPivot` centrado en el eje craneal y se diseñó un esquema de iluminación cálida de 3 puntos más brillo ocular (*catchlight*).

### Error 4: Terreno "Arcoíris" y Círculos Negros Opacos al Exportar *Castle Grounds*
![Evidencia del Error 4: terreno arcoíris y sombras negras]({{ '/assets/images/proceso/etapa2_bug_arcoiris_sombras.png' | relative_url }})
* **Descripción del fallo**: La primera exportación de `castle_grounds.glb` mostraba colinas fucsias, naranjas y moradas junto con cuadrados negros sólidos bajo los árboles.
* **Causa técnica**: En Nintendo 64, cuando `G_LIGHTING` está activo, los últimos bytes de cada vértice `Vtx` almacenan **componentes de normal con signo (`int8`, -128..127)** y no colores RGB (`uint8`). Además, la textura `0900BC00` es una calcomanía de sombra en escala de grises + alfa que se estaba renderizando como geometría opaca con escritura en Z-buffer.
* **Solución aplicada**: Se implementó el cálculo real de producto punto normal-luz (`gdSPDefLights1`) en `scripts/export_castle_grounds.py` y se configuró `transparent: true`, `depthWrite: false` y `polygonOffset` para el material `0900BC00`.

### Error 5: Ausencia de la Torre Central Alta y Superficies sin Textura (`G_CC_SHADE`)
![Evidencia del Error 5: castillo sin torre central alta]({{ '/assets/images/proceso/etapa3_sin_torre_ni_actores.png' | relative_url }})
* **Descripción del fallo**: El castillo carecía de su emblemática torre central superior (solo flotaba una ventana aislada en el cielo) y el hueco interior tras las puertas lucía blanco en vez de oscuro.
* **Causa técnica**: El exportador inicial recorría arreglos sueltos e ignoraba el submodelo `areas/1/3` (`special_level_geo_03`, desplazado a `(0, 2867, -3924)`) así como el apagado de texturas `gsSPTexture(..., G_OFF)` (`G_CC_SHADE`).
* **Solución aplicada**: Se reescribió el intérprete para ejecutar recursivamente las listas de despliegue RSP (`gsSPDisplayList`) en orden exacto de hardware e incluir `areas/1/3`, `7` y `8` junto con un material `untextured_shade` de color de vértice puro.

### Error 6: Caída a Través del Suelo y Desaparición de Coleccionables por Normales en Espacio Local
* **Descripción del fallo**: Al iniciar directamente en Gameplay (`?scene=6`), el personaje se hundía bajo la arena y no aparecía ningún Bitcoin ni cartel sobre el puente.
* **Causa técnica**: Dos causas combinadas:
  1. `Raycaster.intersectObjects()` en Three.js devuelve `hit.face.normal` en **espacio local del objeto**. Como Blender exporta nodos GLTF con rotación de ejes (`Z-up` ➔ `Y-up`), los pisos horizontales tenían normal local `(0, 0, 1)` (`normal.y = 0`), siendo descartados por el filtro `Math.abs(h.face.normal.y) > 0.42`.
  2. La gravedad se ejecutaba durante los primeros milisegundos previos a que `castle_grounds.glb` terminara de cargar.
* **Solución aplicada**: Transformación explícita de la normal a espacio de mundo antes de evaluar la pendiente y guardia `!castleLoaded`:
  ```javascript
  _worldNormal.copy(h.face.normal).transformDirection(h.object.matrixWorld);
  if (Math.abs(_worldNormal.y) > 0.42) return h.point.y;
  ```

### Error 7: Residuo del Busto en el Cuello del Personaje Jugable y Doble Descarga de 12 MB
* **Descripción del fallo**: Al acoplar `bukele_head.glb` sobre el cuerpo formal `bukele_body.glb`, sobresalía una franja gris del cuello/hombros del busto original en la nuca, y el archivo de 12 MB se descargaba dos veces por red.
* **Causa técnica**: `bukele_head.glb` incluye la parte superior de los hombros pensada para la Escena 2, y se invocaba `gltfLoader.load()` por separado en dos funciones.
* **Solución aplicada**: Carga única en memoria clonando la escena para el héroe e inyectando un recorte espacial en GPU mediante `material.onBeforeCompile`:
  ```glsl
  if (vHeadPos.y < -0.34 || (vHeadPos.y < -0.21 && vHeadPos.x < -0.04) || ...) discard;
  ```

### Error 8: Articulación Entrecortada al Sintetizar Secuencias Musicales `.m64`
* **Descripción del fallo**: En la primera prueba del sintetizador Python sobre las secuencias originales, las notas largas de trompeta y cuerdas sonaban artificialmente cortadas.
* **Causa técnica**: En el motor de audio de *Super Mario 64* (`seqplayer.c`), el byte `noteDuration` no representa el tiempo encendido sino la **fracción de silencio (`off-time`)**: `off_ticks = (noteDuration * delay) // 256`, donde `note1` fija `noteDuration = 0` (100% legato).
* **Solución aplicada**: Se corrigió la fórmula de duración en `scripts/render_sm64_audio.py`, obteniendo fraseo legato idéntico al hardware original en `castle_grounds_bgm.mp3` y `star_fanfare.mp3`.

### Error 9: Giro del Símbolo `₿` en Tapas de Cilindro y Visibilidad de `#sign-dialog`
* **Descripción del fallo**: El cartel `#sign-dialog` aparecía vacío al iniciar el nivel y el símbolo `₿` en las caras de los Bitcoins lucía rotado 90°/invertido.
* **Causa técnica**: En `css/style.css` cada componente definía su propio modificador `.hidden` y faltaba `.sign-dialog.hidden`; por su parte, las tapas UV de `CylinderGeometry` al rotar `disc.rotation.x = Math.PI / 2` mapean el eje vertical del mundo sobre `-X` del canvas.
* **Solución aplicada**: Se añadió `.sign-dialog.hidden { display: none; }` con `@keyframes signDialogPop` conservando `translateX(-50%)`, y se rotó el contexto 2D del canvas `-Math.PI / 2` para que `₿` se lea derecho en ambas caras de cada moneda.
