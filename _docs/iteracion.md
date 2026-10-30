---
title: 4. Iteración y Mejora
description: "Ajustes de jugabilidad, game feel, solución de bugs de salto de escena y esculpido anatómico en Blender."
layout: default
nav_order: 4
permalink: /docs/iteracion/
---

# 4. Iteración y Mejora Continua

## 🔄 El Bucle de Vibecoding: Diagnóstico y Perfeccionamiento

En el desarrollo asistido por IA, la primera respuesta raramente cumple con los estándares de jugabilidad (*game feel*) ni con la fidelidad artística deseada. A continuación se documenta el ciclo de iteraciones técnicas ejecutadas para llegar al resultado final:

---

### 1. Ajuste del "Game Feel" del Salto (Física e Inercia)
* **Comportamiento inicial**: El personaje salía disparado hacia arriba a velocidad fija y caía lentamente de golpe, sintiéndose ingrávido y difícil de controlar para aterrizar sobre las plataformas.
* **Instrucción de mejora dada a la IA**:
  > *"El salto se siente flotante. Aumenta la fuerza de gravedad a -34 unidades y dale una velocidad de despegue más rápida. Agrega además una pequeña inercia horizontal para que si el jugador corre antes de saltar, conserve el impulso hacia adelante en el aire."*
* **Resultado**: El control pasó de sentirse como un prototipo rígido a tener la clásica parábola ágil de Super Mario 64.

---

### 2. Estilizado Visual del Protagonista en Escena de Juego
* **Comportamiento inicial**: El personaje se generó con cajas primitivas y proporciones genéricas.
* **Instrucción de mejora dada a la IA**:
  > *"Ajusta el modelo 3D: Nayib debe llevar su traje ceremonial negro con bordados dorados en cuello y mangas, banda presidencial azul y blanco sobre el pecho, peinado oscuro estilizado hacia atrás y barba bien delineada. Proyecta una sombra circular semitransparente bajo sus pies para calcular los aterrizajes."*
* **Resultado**: La silueta del personaje se volvió reconocible al instante y la sombra proyectada facilitó enormemente la precisión en los saltos.

---

### 3. Rotación y Resplandor de la Estrella
* **Comportamiento inicial**: La estrella era estática y se perdía con el fondo.
* **Instrucción de mejora dada a la IA**:
  > *"Haz que la Estrella Dorada oscile verticalmente con una función seno matemática (bobbing) y gire constantemente sobre su eje Y. Añade una luz puntual dorada (`PointLight`) que emita resplandor sobre la cima de la colina."*
* **Resultado**: La cumbre del nivel se convirtió en un foco de atención visual inmediato para el jugador.

---

### 4. Corrección del Salto Prematuro de Escena 2 (Bug de Transición)
* **Comportamiento defectuoso**: Al pasar de la Escena 1 (Título) a la Escena 2 (Rostro 3D), la segunda escena duraba menos de un segundo y saltaba automáticamente al juego sin permitir interactuar con la cabeza de Bukele.
* **Diagnóstico técnico**: 
  1. El evento global `mousedown` y `keydown` (tecla Espacio) propagaba el evento de avance de la Escena 1 inmediatamente hacia la Escena 2 si el usuario mantenía presionada la tecla o hacía doble clic.
  2. Los usuarios pulsaban la barra espaciadora por inercia gamer, lo que detonaba el salto de escena.
* **Solución de ingeniería**:
  - Se eliminó por completo la tecla `Space` como disparador de cambio en la Escena 2.
  - Se añadió un bloqueo de seguridad (*cooldown*) de **2.2 segundos** (`performance.now() - scene2EnterTime < 2200`).
  - La transición a la Escena 3 quedó sujeta de forma deliberada al clic en el botón multicolor **"PRESS START"** o a presionar `Enter`.
* **Resultado**: La Escena 2 permanece abierta de forma indefinida, permitiendo al jugador girar el rostro libremente con el puntero del ratón.

---

### 5. Esculpido Anatómico en Blender y Fidelidad Facial (ref-07)
* **Comportamiento inicial**: La cabeza de Bukele era una esfera UV genérica con una textura estirada, sin relieve en la nariz ni contorno de mandíbula, viéndose plana y deformada al girar.
* **Instrucción de mejora dada a la IA**:
  > *"El rostro de Bukele es irreconocible. Tienes que esforzarte en lograr algo creíble y que demuestre atención al detalle. Te adjunto una fotografía frontal nítida con su traje de gala para usar como referencia visual."*
* **Pipeline ejecutado con la skill `game-builder-blender-assets`**:
  1. Se recortó la textura frontal limpia en alta resolución (`bukele_face_crop_clean.png`).
  2. Mediante un script Python para Blender (`build_bukele_head.py`), se esculpieron las características anatómicas reales:
     - **Nariz 3D proyectada (+0.35Y)** con tabique recto y volumen lateral.
     - **Mandíbula angulada y mentón proyectado** con barba delineada.
     - **Pómulos y cuencas oculares** modeladas.
     - **Orejas anatómicas 3D** en ambos costados (+X / -X).
     - **Cabello con volumen pompadour peinado hacia atrás**.
     - **Cuello mandarín ceremonial con anillo de oro metálico y banda presidencial**.
  3. Mapeo UV cilíndrico/esférico frontal calibrado y exportación en formato GLB optimizado (453 KB).
* **Resultado**: Un busto tridimensional creíble, fidedigno a la fotografía de referencia y con la iluminación especular y estética característica de la era de Nintendo 64.


---

### 6. Transición de "Foto en Esfera" a Modelo Poligonal Estilizado N64
* **Comportamiento defectuoso**: Al intentar mapear una fotografía 2D sobre una esfera UV deformada, se produjo el "síndrome de la cabeza de huevo": ojos estirados lateralmente hacia las orejas, nariz en forma de pico afilado y parte superior con aspecto de gorro de baño.
* **Criterio aplicado según la skill `game-builder-blender-assets`**:
  - En *Super Mario 64*, la pantalla de título original de 1996 nunca usó fotos; utilizó **geometría poligonal estilizada** con volúmenes claros y materiales limpios.
  - La skill clasifica cualquier activo de cámara principal con forma de esfera deformada como **FAIL automático en el Turnaround Gate**.
* **Nueva Implementación Técnica**:
  1. **Cabeza y Mandíbula**: Cráneo anatómico con mandíbula angulada y mentón cuadrado característico de Bukele.
  2. **Nariz 3D Real**: Puente nasal recto con inclinación de 22°, punta redondeada y aletas nasales separadas.
  3. **Ojos N64 Auténticos**: Conjunto de 4 elementos por ojo: esclera marfil, iris castaño, pupila negra y destello blanco (*eye glint*).
  4. **Barba y Bigote Volumétricos**: Geometría en 3D que abraza la mandíbula y el labio superior, permitiendo que la iluminación y las sombras se proyecten de forma natural.
  5. **Cabello Pompadour 3D**: Volumen superior elevado, copete frontal y ondas laterales que caen en las patillas.
  6. **Indumentaria Presidencial**: Cuello mandarín alto con doble anillo de oro metálico y banda presidencial tricolor con escudo nacional.
* **Resultado**: Un busto tridimensional limpio, carismático y técnicamente impecable, que rinde un tributo visual auténtico a Nintendo 64 sin artefactos ni deformaciones grotescas.


---

### 7. Integración Definitiva: Pipeline Híbrido Tripo3D AI + Blender 5.2 LTS
* **Problema a resolver**: El modelado procedural por código matemático en Blender alcanzaba un límite estético evidente al intentar reproducir la anatomía facial humana orgánica, generando muñecos de baja similitud.
* **Solución de ingeniería híbrida**:
  1. **Generación Multimodal**: Se generó el busto 3D de alta definición en Tripo3D a partir de la fotografía de gala de Bukele.
  2. **Extracción y Descompresión**: Se recuperó el activo binario `meshopt` y se decodificó con `@gltf-transform/cli` para compatibilidad universal con Blender.
  3. **Optimización WebGL en Blender (`process_tripo_glb.py`)**:
     - Reducción del conteo poligonal de **1,956,516 polígonos** (pesado para navegadores) a **35,000 polígonos limpios** mediante el algoritmo `DecimateWeb`, conservando el 100% del mapa de normales y detalles faciales.
     - Centrado del punto de pivote en el centro de gravedad del cráneo para permitir un seguimiento suave e hipnótico del cursor del ratón.
     - Normalización de escala a 1.6 unidades para ajuste exacto a la cámara perspectiva de Three.js.
  4. **Turnaround Gate & Verificación**:
     - Renders de control generados en `turnaround-bukele-tripo-sheet.png`.
     - Captura en vivo confirmando 0 deformaciones y renderizado PBR fotorrealista sobre el fondo de mosaico azul "SUPER BUKELE 64".
* **Resultado**: La pantalla interactiva de la cara 3D alcanza un estándar gráfico sobresaliente, manteniendo un rendimiento fluido de 60 FPS en el navegador.


---

### 8. Desacoplamiento de Ejes en Three.js con `headPivot` y Retorno Elástico
* **Problema detectado**: El modelo aparecía girado 90° mirando hacia el hombro izquierdo y la rotación con el cursor se sentía trabada y desfasada.
* **Causa técnica**:
  - Confusión de coordenadas entre el espacio local de la malla generada por Tripo (+X como vector frontal) y el espacio de cámara de Three.js (-Z como vector de visión).
  - Rotar directamente la malla provocaba desfase de ejes al interpolar el pitch y yaw simultáneamente.
* **Solución de ingeniería**:
  - Se estructuró una jerarquía de dos niveles:
    - **Nivel hijo (`bukeleHeadMesh`)**: Fija la corrección angular permanente en `-Math.PI / 2` en reposo, garantizando que el rostro mire de frente a la cámara.
    - **Nivel padre (`headPivot`)**: Recibe limpiamente las coordenadas normalizadas del cursor `(mouseNormalizedX, mouseNormalizedY)` multiplicadas por sus factores angulares y aplica suavizado `lerp` a 10 unidades/delta.
  - Se implementó interacción de arrastre (*drag*) con resorte elástico: al mantener pulsado el botón izquierdo y arrastrar, la cabeza sigue el tirón del ratón, y al soltarlo regresa elásticamente a la posición de la mirada.
* **Resultado**: La cabeza de Bukele arranca mirando fijamente al jugador en el centro y se mueve con total naturalidad en todas las direcciones siguiendo el puntero.


---

### 9. Iluminación Cálida de Estudio y Eliminación del Efecto Tétrico
* **Problema visual**: Aunque el modelo 3D era exacto, en el render de Three.js lucía tétrico: frente facetada con sombras duras triangulares, ojos opacos sin vida, sonrisa con fondo negro inquietante y tinte verdoso/azulado sobre la piel.
* **Causa técnica**:
  1. Uso de luz puntual fría azul (`0x93c5fd`) que destrozaba el color cálido de la piel salvadoreña.
  2. Falta de luz ambiental difusa que permitía que las cavidades faciales cayeran en sombra absoluta (0 lúmenes).
  3. Facetas poligonales visibles en la frente debido a normales duras tras la decimación.
  4. Piel con exceso de brillo especular tipo plástico mojado.
* **Solución de ingeniería**:
  1. **Esquema de Iluminación de Retrato Profesional**:
     - `AmbientLight(0xfff5ea, 1.7)` cálida envolvente.
     - `DirectionalLight(0xfffaee, 1.8)` frontal principal.
     - `PointLight(0xffeedb, 1.3)` lateral de relleno melocotón.
     - `PointLight(0xffffff, 1.1)` a nivel de cámara para destello de vida (*eye catchlight*).
  2. **Pipeline de Suavizado Geométrico**:
     - Se aumentó el presupuesto a 65,000 polígonos con `shade_smooth` completo en Blender y cálculo automático de normales de vértices en Three.js.
  3. **Calibración Cinematográfica PBR**:
     - Activación de `ACESFilmicToneMapping` con exposición calibrada a 1.18.
     - Rugosidad PBR establecida en 0.58 (acabado de piel mate natural).
* **Resultado**: El rostro recuperó su calidez, amabilidad y viveza, viéndose tan acogedor y fotogénico como en el visor original de Tripo, pero completamente interactivo a 60 FPS.


---

### 10. Recreación del Logo 3D en Bloques de Madera Auténticos de Nintendo 64
* **Problema visual detectado**: La pantalla de título original de Super Mario 64 destaca por sus letras de juguete de madera con caras de colores saturados y su característico bloque "64" dorado. En contraste, la versión inicial en el juego utilizaba spans HTML con sombras CSS que se veían planas, apagadas y con artefactos de color marrón oscuro debido al solapamiento de `-webkit-text-fill-color: transparent` con `text-shadow`.
* **Causa técnica**:
  - Los motores de renderizado de los navegadores (Blink / Gecko) no pueden calcular oclusión ambiental real, biseles tridimensionales ni texturas de madera de ángulo oblicuo mediante CSS puro sin glitches de transparencia y rendimiento.
* **Solución de ingeniería con Blender headless (`render_super_bukele_logo.py`)**:
  1. **Generación Geométrica 3D**:
     - Se crearon las mallas de texto en Blender con biselado paramétrico (`bevel_depth = 0.045`, `extrude = 0.72`) y se convirtieron a mallas poligonales con rotación en el espacio de mundo.
     - Se clasificaron los polígonos por vector normal: normales frontales (`normal.y < -0.32`) reciben el material del color primario correspondiente, mientras que las caras laterales e inferiores reciben el material de madera de pino.
  2. **Shader de Madera Pino N64**:
     - Implementación de un nodo `ShaderNodeTexWave` con distorsión sobre coordenadas de objeto y rampa de color dual (`#c77a38` veta ámbar / `#f5c280` pino claro) para simular el grano de los bloques de madera tallada.
  3. **Disposición y Arqueo Clásico**:
     - Fila superior curvada con "SUPER" (Rojo, Azul, Amarillo, Azul, Verde) y el bloque "64" inclinado a -15° con bordes dorados y el "TM" superior.
     - Fila inferior imponente con "BUKELE" (Azul, Verde, Amarillo, Rojo, Verde, Azul) con extrusión profunda que revela los bloques inferiores.
  4. **Encuadre Óptico y Render RGBA**:
     - Cámara a 52mm focal alineada en perspectiva isométrica, iluminación de sol cenital con luces de relleno cálidas e inferiores, exportando a 1600x750 en canal alfa transparente.
  5. **Integración Web**:
     - Sustitución de las 50 líneas de CSS obsoleto por la imagen de alta fidelidad `.n64-3d-logo`, combinada con animación suave de respiración `logoFloat`, el rótulo brillante `©2026 Kodigo Academy` y el botón pulsante `PRESS START`.
* **Resultado**: La pantalla de inicio alcanza una estética 100% fidedigna y nostálgica de Nintendo 64, idéntica en espíritu y paleta al juego original.


---

### 11. Cuadrícula de Fondo Acolchada N64 con Fuente Oficial "Typeface Mario 64"
* **Problema visual detectado**: El fondo de la Escena 2 dependía de un pseudo-elemento CSS con texto repetido rotado a -6deg sobre un degradado genérico. Carecía de la textura granular, el relieve 3D de las letras y la cuadrícula de botones acolchados característica del inicio de Super Mario 64.
* **Causa técnica**:
  - CSS estándar no permite aplicar texturas de tela retro ni biseles sombreados tridimensionales por celda que coordinen con una tipografía vintage sin una sobrecarga masiva de DOM.
* **Solución de ingeniería**:
  1. **Aprovisionamiento e Instalación de Fuente**:
     - Extracción e instalación de `TypefaceMario64-ywA93.otf` en el sistema Linux con `fc-cache` e importación web en `pj-vibe-game/assets/fonts/`.
  2. **Pipeline de Renderizado Ortográfico en Blender (`render_n64_tile.py`)**:
     - Modelado de baldosa unitaria cuadrada (4x4 unidades mundiales) con cámara ortográfica frontal y resolución 512x512.
     - **Shader de Baldosa Acolchada**: Gradiente de viñeta radial calculado con `VectorMath.DISTANCE` desde el centro UV (0.5, 0.5), proyectando azul cobalto en el núcleo y azul marino profundo en los extremos, combinado con un mapa de ruido `TexNoise` a 24.0 de escala para reproducir la trama textil de los cartuchos de 64 bits.
     - **Tipografía en Relieve 3D**: Letras extruidas con caras en celeste hielo saturado (`#5897fa`) y biseles en sombra azul oscuro (`#0b1640`), junto al bloque `64` en rojo bermellón (`#e52521`).
     - **Costuras de Cuadrícula**: Micro-ranuras oscuras en los 4 bordes exteriores para delimitar cada cuadrante.
  3. **Montaje en el Juego y Tipografía en el HUD**:
     - Sustitución del texto CSS por `background-image: url('../assets/img/n64_bg_tile.png')` con tamaño de celda a 190px.
     - Aplicación de la fuente oficial a los caracteres multicolor de `PRESS START`.
* **Resultado**: El busto 3D de Bukele ahora reposa sobre la misma e inconfundible cuadrícula azul acolchada de Super Mario 64, logrando cohesión estilística absoluta entre el modelo 3D y su entorno.


---

### 12. Unificación Integral del Arte: Logotipo 3D Poligonal y Mosaico en Pantalla de Inicio
* **Problema visual detectado**: Aunque la Escena 2 (rostro interactivo) ya contaba con la cuadrícula de mosaico acolchado y la tipografía oficial `Typeface Mario 64`, la Escena 1 (pantalla de bienvenida) se sentía desconectada estilísticamente: el logo 3D utilizaba letras redondeadas de Noto Sans y el fondo permanecía en un negro plano.
* **Causa técnica**:
  - El render inicial de `super_bukele_64_logo.png` fue generado previo a la instalación de la tipografía retro, resultando en caracteres curvos no canónicos que contrastaban con las facetas poligonales de 64 bits de la segunda escena.
* **Solución de ingeniería**:
  1. **Re-modelado Tridimensional con `TypefaceMario64.otf`**:
     - Se adaptó el pipeline de Blender para cargar la tipografía facetada en cada letra de "SUPER" y "BUKELE", así como en el bloque "64" inclinado y "TM".
     - Cada bloque de madera extruido adoptó la silueta geométrica exacta de la fuente original de Nintendo 64.
  2. **Continuidad de Fondo con Doble Capa**:
     - Se integró el mosaico acolchado `n64_bg_tile.png` en `.title-scene` mediante `background-image` con un viñeteado radial oscuro (`rgba(10, 25, 80, 0.72)` al centro y `rgba(2, 5, 20, 0.95)` a los bordes) para mantener legibilidad y protagonismo del logo.
  3. **Tipografía Unificada en Interfaz**:
     - La licencia `©2026 KODIGO ACADEMY` y el botón `PRESS START` se actualizaron a `TypefaceMario64`.
* **Resultado**: La experiencia visual desde que el usuario entra al juego es 100% homogénea, nostálgica y profesional, transmitiendo una estética de cartucho original de Nintendo 64 de principio a fin.


---

### 13. Calibración Espacial del Logotipo: Desacoplamiento y Despeje del Bloque "64"
* **Problema visual detectado**: Al adoptar las métricas anchas de la fuente oficial `Typeface Mario 64`, el bloque rojo "64" colisionaba con la cara frontal y la madera de la letra `R` de "SUPER", además de quedar encimado sobre la `E` de "BUKELE".
* **Causa técnica**:
  - Las proporciones de caja tipográfica de la fuente Mario 64 son considerablemente más anchas y anguladas que las de fuentes convencionales, requiriendo un espaciado horizontal ampliado para los elementos asimétricos flotantes.
* **Solución de ingeniería**:
  1. **Reajuste de Coordenadas 3D en Blender**:
     - Traslación del objeto `Logo_64` de `x = 3.95` a `x = 4.45` y elevación a `z = 1.25`, otorgando un espacio negativo nítido entre la `R` y el número.
     - Traslación coordinada del objeto `Logo_TM` a `x = 5.65`, `z = 2.15`.
  2. **Reencuadre de Cámara Focal**:
     - Se ajustó el centro de la cámara en el eje horizontal a `x = 0.55` para garantizar que ambos extremos del logotipo (desde la `B` hasta el `TM`) cuenten con márgenes simétricos idénticos en la pantalla 16:9.
* **Resultado**: El logotipo "SUPER BUKELE 64" alcanza su máxima claridad tipográfica, con cada letra y bloque tridimensional respirando de forma independiente sin oclusiones indeseadas.

---

### 14. Escena 3: Pantalla SELECT FILE (Homage a Mario 64 con Cursor de Mano 3D y Transición Universal)
* **Objetivo de diseño**: Reproducir fielmente la tercera fase de la introducción canónica de *Super Mario 64* (segundos 5 a 8 de la secuencia del cartucho), donde el jugador accede al tablero dorado de selección de perfil antes de descender al mundo exterior.
* **Componentes implementados**:
  1. **Tablero Dorado con Marco Biselado**:
     - Estructura CSS centrada con marco perimetral biselado de 24px con doble tonalidad de oro y bronce (`#fde047`, `#a16207`, `#713f12`, `#eab308`).
     - Título "SELECT FILE" con letras en relieve facetado multicolor (`c-green`, `c-pink`, `c-yellow`).
  2. **Slots de Perfil "BUKELE A, B, C, D"**:
     - Cuatro ranuras de guardado con marco de acero biselado e icono de retrato en escala de grises de Nayib Bukele (`assets/img/bukele_file_icon.png`).
     - Insignia retro "NEW" en tipografía tricolor N64 (cian, amarillo y rojo).
  3. **Botones de Función Inferiores**:
     - Bloques cúbicos biselados de colores representativos: verde (`SCORE`), azul (`COPY`), rojo (`ERASE`) y púrpura (`STEREO`).
  4. **Cursor de Mano 3D N64 Enguantada**:
     - Modelado e iluminación en Blender (`render_hand_cursor.py`), exportado en PNG transparente de 256x256.
     - Elemento flotante (`#n64-hand-cursor`) con cursor nativo del sistema ocultado (`cursor: none`), sincronizado en tiempo real con la posición del ratón.
     - Posicionamiento predeterminado sobre el archivo "BUKELE A" para emular el arranque exacto del juego original.
  5. **Mecánica de Avance Global (Any-Click Transition)**:
     - El usuario puede hacer clic en cualquier punto del tablero o presionar `Enter`/`Espacio` para avanzar inmediatamente a la Escena 4 (el gameplay 3D en la pradera con Bukele recolectando Bitcoins).
* **Resultado**: La transición entre la interacción de la cabeza 3D y la partida jugable es idéntica en estética y ritmo a la obra maestra de Nintendo 64.

---

### 15. Secuencia Cinemática Adaptada: Carta de Gabriela y Vuelo de Lakitu
* **Objetivo de diseño**: Resolver la incoherencia narrativa que supondría proyectar a Mario y a la Princesa Peach en la cinemática inicial del video original, creando una experiencia puente personalizada ("Opción 2") que une la nostalgia auténtica de N64 con los personajes de la parodia.
* **Componentes implementados**:
  1. **Pantalla del Pergamino de la Primera Dama (`#scene-letter`)**:
     - Emulación de la carta original de Peach con una composición centrada flotante, marco biselado dorado de 10px y textura de pergamino cálido.
     - Texto adaptado:
       > *"Querido Nayib: Por favor ven al castillo. Te he preparado una sorpresa... Con cariño-- Primera Dama Gabriela"*.
     - Sello real circular en oro y bronce con icono de corona.
     - Reproducción síncrona del arpegio de piano original de la carta (`assets/audio/letter_bgm.mp3`).
  2. **Cinemática de Vuelo de Lakitu (`#scene-cinematic`)**:
     - Recorte y transcodificación optimizada a 720p 60fps (`assets/video/lakitu_castle_flight.mp4`, 4.2 MB) del vuelo sobre el foso y jardines del castillo.
     - Reproducción a pantalla completa tras leer la carta.
     - Indicador flotante estilizado `[Pulsa ESPACIO para saltar cinemática ⏩]`.
  3. **Control y Salto Universal**:
     - El jugador puede presionar `Espacio`, `Enter`, `Escape` o hacer clic en cualquier instante para omitir la cinemática y entrar inmediatamente a la Escena 6 (el nivel 3D en la pradera con Bukele).
* **Resultado**: El arco narrativo introductorio queda completo: Título ➔ Rostro 3D ➔ Selección de Partida ➔ Carta de Gabriela ➔ Vuelo al Castillo ➔ Jugabilidad 3D.

---

### 16. Calibración Fina de la Cinemática y Relevo Espacial de la Tubería Verde N64
* **Objetivo de diseño**: Perfeccionar el montaje de la cinemática de Lakitu para que comience limpiamente en el cielo azul despejado y termine exactamente en el brote de la tubería verde N64 (segundo 49), permitiendo que el motor WebGL 3D ("Super Bukele 64") tome el relevo in situ sin que Mario llegue a aparecer.
* **Componentes implementados**:
  1. **Edición Milimétrica del Clip (`assets/video/lakitu_castle_flight.mp4`)**:
     - **Corte de Inicio (26.5s del video original)**: Se desplazó 3.5 segundos hacia adelante respecto al corte previo, eliminando los fotogramas del vitral de Peach. El video arranca directamente en el cielo azul de pradera con nubes blancas.
     - **Corte Final (49.0s del video original)**: Se congeló el punto de término en el instante en que la tubería verde emerge y se fija al suelo, finalizando la cinemática a cero fotogramas de que Mario salga. Duración final: 22.5 segundos.
  2. **Construcción Procedural de la Tubería Verde N64 en Three.js**:
     - Se implementó `createWarpPipe(x, z)` en `js/game.js`:
       - Base terrosa circular (`0xe5c07b`) idéntica a la textura de arena del video.
       - Tubería cilíndrica de polígonos facetados con material `MeshStandardMaterial` verde brillante (`0x22c55e`).
       - Borde superior cilíndrico ensanchado e interior hueco oscuro (`0x052e16`).
       - Volumen de colisión agregado a `colliders` para física sólida.
  3. **Continuidad del Relevo en Gameplay (`SCENE_6_GAMEPLAY`)**:
     - Al concluir la cinemática o al saltarla, el jugador aparece posicionado en `(0, 0, 8.8)`, justo al frente de la tubería verde recién emergida en `(0, 11.5)`.
     - La cámara en 3ª persona se sitúa detrás para ofrecer una perspectiva inmediata de la pradera y la colina de Bitcoins.
* **Resultado**: Una transición cinemática-jugabilidad 100% coherente y fluida que respeta el ritmo del clásico de 1996 adaptado con humor y fidelidad técnica al universo de Super Bukele 64.


---

### 17. Replicación Completa de *Peach's Castle Grounds* (RENDER96 HD), Héroe 3D Fiel a `assets2` y Cinemática de Puertas Estelares
* **Objetivo de diseño**: Construir el exterior completo y auténtico del Castillo de Peach (*Castle Grounds*, Área 1 de *Super Mario 64*) con texturas de alta definición `RENDER96-HD-TEXTURE-PACK`, integrar el modelo 3D de cuerpo entero de Nayib Bukele fiel a `Desktop/assets2` y cerrar el arco jugable cuando el jugador abre y cruza las grandes puertas estelares del castillo.
* **Componentes implementados**:
  1. **Extracción Arquitectónica Completa (`scripts/export_castle_grounds.py`, `scripts/export_castle_actors.py`)**:
     - Recorrido en orden exacto de las listas de despliegue RSP (`gsSPDisplayList`) de `levels/castle_grounds/areas/1/` incluyendo terreno, senderos, puente de piedra, fachada con vitral de Peach, torreones laterales, **torre central alta con asta (`areas/1/3`, `special_level_geo_03`)**, calcomanías alfa de sombra (`areas/1/4`, `0900BC00`) y rejillas sumergidas (`areas/1/7` y `8`).
     - Horneado de iluminación direccional `gdSPDefLights1` en colores de vértice y soporte de materiales sin textura (`G_CC_SHADE`) en `assets/models/castle_grounds.glb` (3.0 MB).
     - Exportación de actores 3D independientes: `assets/models/castle_door.glb` (puertas de madera pulida con pomo dorado y emblema estelar simétrico `zero_star_door_sign.rgba16.png`) y `assets/models/wooden_signpost.glb`.
  2. **Personaje Jugable 3D Nayib Bukele (`scripts/build_bukele_hero.py`)**:
     - Cuerpo articulado en Blender (`assets/models/bukele_body.glb`) con saco formal azul marino oscuro, camiseta negra lisa, pantalón azul marino y zapatos cafés conforme a `Desktop/assets2`.
     - Carga única e instanciación clonada de `assets/models/bukele_head.glb` asentada directamente sobre el cuello del saco con recorte limpio de busto mediante `onBeforeCompile`.
  3. **Entorno Vivo, Física en Espacio de Mundo y Coleccionables (`js/game.js`)**:
     - Transformación de normales de impacto de raycast a espacio de mundo (`transformDirection(matrixWorld)`) en `sampleGround()` y `wallAhead()`, garantizando colisión sólida sobre pendientes, puente y muros, con guardia de gravedad previa a la carga del nivel (`castleLoaded`).
     - 26 árboles oficiales con texturas HD (`tree_left_side.rgba16.png`, `tree_right_side.rgba16.png`) en billboard sobre eje Y (`special_bubble_tree`) y colisión cilíndrica de tronco.
     - Cascada del acantilado (`movtext.inc.c`), foso y laguna con desplazamiento UV continuo, 4 banderas rojas ondeando en las torres (`bhvCastleFlagWaving`), 4 carteles cómicos interactivos (`#sign-dialog`) y 10 Bitcoins con emblema `₿` orientado verticalmente a lo largo del recorrido.
  4. **Secuencia de Victoria en el Pórtico (`SCENE_DOOR_OPENING` ➔ `SCENE_VICTORY`)**:
     - Al alcanzar el pórtico (`Z ≈ -29.5, Y > 7.2`), ambas puertas estelares pivotan hacia afuera (`±1.62 rad`) con temporización independiente de fotogramas (`performance.now()`), Bukele camina hacia el interior del castillo y se despliega `#victory-modal` con Bitcoins recolectados (`X / 10`) y tiempo total (`MM:SS`).
* **Resultado**: Una recreación tridimensional fiel, nítida y viva de los jardines del Castillo de Peach en el navegador.

---

### 18. Extracción y Síntesis de Música, Voces y Efectos Auténticos desde la ROM Original de *Super Mario 64*
* **Objetivo de diseño**: Reemplazar los efectos provisionales por la banda sonora y muestras acústicas auténticas de *Super Mario 64* a partir de la ROM norteamericana original del usuario, manteniendo estricta higiene del repositorio (cero binarios de ROM versionados).
* **Componentes implementados**:
  1. **Conversión `.V64` ➔ `.z64` y Extracción de Bancos de Audio**:
     - Conversión byte-swapped (`0x37804012` a big-endian `0x80371240`) fuera del repositorio Git y extracción automatizada de bancos PCM `.aiff`, definiciones JSON de instrumentos y secuencias `.m64`.
  2. **Motor de Síntesis de Secuencias `.m64` (`scripts/render_sm64_audio.py`)**:
     - Decodificación de pistas `.m64` acoplada al banco de instrumentos `22` respetando la frecuencia base `gNoteFrequencies` y la fracción de articulación `noteDuration` de `seqplayer.c`.
     - Generación y verificación de niveles (`volumedetect`) de `castle_grounds_bgm.mp3` (`03_level_grass`), `star_fanfare.mp3` (`01_cutscene_collect_star`), `coin.mp3` (`.sound_general_coin`), `door_open.mp3` (`.sound_general_open_wood_door`), `mario_0C.mp3` (*"Here we go!"*) y las 5 voces clásicas de salto.
* **Resultado**: Identidad sonora 100% fiel a Nintendo 64 integrada en cada acción de salto, recolección de Bitcoins, recorrido por los jardines y apertura triunfal de las puertas del castillo.
