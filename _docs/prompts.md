---
title: 3. Evidencia de Prompts (Vibecoding)
description: "Registro cronológico y justificación técnica de los prompts progresivos utilizados para guiar el desarrollo con IA."
layout: default
nav_order: 3
permalink: /docs/prompts/
---

# 3. Evidencia de Prompts (Vibecoding Progresivo)

Uno de los requisitos indispensables de la actividad académica es evidenciar que el desarrollo **no fue un "one-shot" automatizado**, sino un proceso riguroso y reflexivo de **Vibecoding Guiado** donde el estudiante toma el rol de director técnico y creativo, guiando a la IA paso a paso, detectando fallos y solicitando refinamientos específicos.

---

## 📌 Prompt 1: Creación del Mundo Base, Cámara y Personaje 3D

### Texto del Prompt enviado a la IA:
> *"Quiero desarrollar un mini-juego 3D en el navegador usando Three.js que sirva como homenaje a Super Mario 64. Crea la estructura inicial en un archivo HTML con Three.js: una pradera verde con árboles low-poly y cielo azul. El personaje principal debe ser Nayib Bukele estilizado en 3D (traje azul marino, camiseta oscura, barba recortada y cabello negro hacia atrás). Agrega controles de movimiento en 3D con WASD y salto con Espacio, junto con una cámara en tercera persona que lo siga suavemente."*

### Explicación y Justificación:
* **Qué se pidió**: Inicializar la escena básica, iluminación ambiental/direccional, geometrías del personaje y física elemental de movimiento.
* **Por qué se acotó así**: Era vital establecer los cimientos del movimiento y la estética del personaje antes de saturar el contexto con niveles, enemigos o coleccionables. Si los controles o la cámara se sentían toscos, era el momento exacto para corregirlos.

---

## 📌 Prompt 2: Nivel 3D, Coleccionables (Bitcoins) y la Estrella Dorada

### Texto del Prompt enviado a la IA:
> *"Ahora necesitamos el nivel y los objetivos. Modifica la escena para agregar una colina escalable con rampas y un par de plataformas flotantes. Distribuye 5 monedas doradas flotantes de Bitcoin con rotación continua y detección de colisión con el jugador (deben desaparecer al tocarlas). En la cima de la colina, coloca una Estrella Dorada 3D brillante con resplandor para que funcione como el objetivo final."*

### Explicación y Justificación:
* **Qué se pidió**: Construir el diseño del nivel (*level design*), la mecánica de recolección y el punto de victoria.
* **Por qué se ajustó o refinó**: En la primera prueba de colisión, el personaje atravesaba las plataformas flotantes al saltar. Se refinó la instrucción para implementar una comprobación de altura y colisión delimitada sobre las plataformas del escenario.

---

## 📌 Prompt 3: Efectos de Sonido (Web Audio API), HUD y Cinemática de Victoria

### Texto del Prompt enviado a la IA:
> *"Para completar el pulido: agrega un HUD en pantalla que muestre el contador de Bitcoins recolectados y el objetivo actual. Implementa efectos de sonido retro usando Web Audio API nativo (sonido 'boing' al saltar, 'pling' al recoger un Bitcoin y fanfarria al ganar). Cuando el jugador toque la Estrella Dorada, congela los controles, haz que la cámara enfoque de frente a Nayib celebrando y muestra un modal de felicitaciones indicando que la Princesa Gabriela ha sido rescatada de Bowser con opción de reiniciar."*

### Explicación y Justificación:
* **Qué se pidió**: Audio inmersivo, retroalimentación visual (HUD) y la pantalla de fin de juego con condición de victoria.
* **Por qué se ajustó o refinó**: Para evitar errores de carga de archivos de audio por bloqueos de CORS o URLs rotas en GitHub Pages, se especificó expresamente el uso del oscilador de la **Web Audio API** del navegador.

---

## 📌 Prompt 4: Pantalla de Título N64 y Activación de Skills de Blender

### Texto del Prompt enviado a la IA:
> *"Al igual que en el juego Mario 64 de Nintendo, comienza con la pantalla de bienvenida clásica con fondo negro, pero dirá 'SUPER BUKELE 64' en bloques 3D con textura de madera y colores rojo, azul, amarillo y verde. Abajo debe decir ©2026 Kodigo Academy con resplandor cian retro. Por favor asegúrate de usar las skills especializadas de Blender (`game-builder` y `game-builder-blender-assets`) para modelar los activos en lugar de usar cajas primitivas."*

### Explicación y Justificación:
* **Qué se pidió**: Recrear con precisión milimétrica la tipografía isométrica y la licencia del título de N64, activando el pipeline profesional de Blender 5.2 LTS headless.
* **Por qué se ajustó o refinó**: Eleva la fidelidad de la entrega académica de un prototipo web a un tributo fiel a la consola de 64 bits.

---

## 📌 Prompt 5: Escena 2 Interactiva (Rostro 3D de Bukele estilo Mario 64)

### Texto del Prompt enviado a la IA:
> *"La escena dos es un clásico: aparece el rostro en 3D en grande sobre un fondo de mosaico azul con las letras 'SUPER BUKELE 64'. Quiero que en lugar de la cara de Mario aparezca la de Nayib Bukele, y que el jugador pueda interactuar con el ratón haciendo que el rostro siga el cursor en tiempo real, junto con el botón arcoíris 'PRESS START' en la esquina inferior izquierda."*

### Explicación y Justificación:
* **Qué se pidió**: Modelado del busto de Bukele con tracking de ratón en tiempo real (pitch/yaw) y reproducción de la ambientación del menú icónico de Nintendo 64.

---

## 📌 Prompt 6: Refinamiento Crítico de Jugabilidad y Fidelidad Anatómica

### Texto del Prompt enviado a la IA:
> *"Ya funcionó, pero la segunda escena dura menos de un segundo (se salta sola sin dar tiempo a interactuar), aparte que el rostro de Bukele se ve genérico e irreconocible. Te adjunto una nueva fotografía frontal en alta resolución con su uniforme ceremonial y banda presidencial. Tienes que esforzarte en lograr algo creíble y que demuestre atención al detalle."*

### Explicación y Justificación:
* **Qué se pidió**: Solucionar el problema de salto abrupto de escenas y re-esculpir en Blender la cabeza con proporciones anatómicas reales (nariz 3D proyectada, mandíbula, orejas, cabello peinado hacia atrás y cuello ceremonial bordado).
* **Demostración de criterio técnico**: Demuestra que el estudiante no aceptó un resultado defectuoso o superficial, sino que evaluó el comportamiento interactivo, diagnosticó la falla y exigió máxima calidad estética.

---

## 📌 Prompt 7: Aplicación Rigurosa de la Skill de Blender (Cero Fotos en Huevos, Escultura N64 Pura)

### Texto del Prompt enviado a la IA:
> *"La mecánica de que sigue al mouse y gira está bien, pero el diseño en sí del rostro es fatal (parece un huevo deformado con una foto estirada). Dime cómo utilizando las skills que hablamos podemos mejorar esto, porque lo que me has entregado está muy lejos de ser un buen inicio. Procede y hazlo bien, sigue al pie de la letra la skill de Blender (`game-builder-blender-assets`) para lograr un busto 3D estilizado creíble."*

### Explicación y Justificación:
* **Qué se pidió**: Abandonar totalmente el atajo erróneo de "pegar fotos en esferas" y construir el busto de Bukele mediante escultura poligonal estilizada (*stylized 3D low-poly caricature*) respetando la estética genuina de Super Mario 64.
* **Por qué se ajustó o refinó**: La skill de Blender prohíbe el uso de cajas o esferas deformadas en activos de cámara principal. Este prompt redirigió el desarrollo hacia una topología de 6.6k polígonos con materiales PBR vectoriales limpios (ojos con esclera, iris y destello, barba y cabello con volumen 3D real y ornamentación ceremonial en oro).

---

## 📌 Prompt 8: Integración de IA Generativa Multimodal 3D (Tripo3D) y Pipeline de Optimización en Blender

### Texto del Prompt enviado a la IA:
> *"No me deja exportarlo sin suscripción, pero te dejo 15 imágenes de la rotación 360 del visor de Tripo. [Tras descubrir el método de extracción de red en WebGL]: Ya descargué el archivo `.glb` original en mi carpeta Downloads (`tripo_pbr_model_90b7e5bb-e652-4561-a9ed-d309aab99399_meshopt.glb`). Por favor procésalo en local, optimízalo e intégralo al juego."*

### Explicación y Justificación:
* **Qué se pidió**: Adoptar un enfoque híbrido de vanguardia: generación de la escultura 3D de alta resolución mediante IA generativa visual (Tripo3D), extracción del activo nativo WebGL y posprocesamiento con herramientas de ingeniería local (descompresión `gltf-transform`, decimado geométrico de 1.95 millones a 35k polígonos en Blender 5.2 LTS, centrado de pivote y normalización de escala para Three.js).
* **Demostración de criterio técnico**: Evidencia la capacidad de combinar herramientas de IA de frontera con pipelines profesionales de optimización de activos 3D para web.

---

## 📌 Prompt 9: Corrección de Orientación Inicial del Modelo y Cinemática del Cursor

### Texto del Prompt enviado a la IA:
> *"No permite rotar el rostro, el movimiento del mouse no es el adecuado, al principio lo tenías bien (el modelo aparecía mirando hacia el perfil izquierdo a 90 grados)."*

### Explicación y Justificación:
* **Qué se pidió**: Ajustar la orientación en reposo del modelo 3D importado y restaurar la cinemática de seguimiento del cursor en los 3 ejes (pitch, yaw, roll).
* **Diagnóstico y Solución Técnica**:
  - Tripo3D orienta la malla con la cara hacia el eje local `+X`. Al aplicar una rotación genérica de 180°, el rostro quedaba apuntando hacia el costado izquierdo.
  - Se desacopló la orientación estática del modelo (`-Math.PI / 2`) introduciendo un contenedor `headPivot` en Three.js.
  - Esto resolvió el bloqueo de ejes (*gimbal lock*), restaurando el control intuitivo del ratón: movimiento horizontal gira el rostro hacia los lados (yaw), vertical hacia arriba/abajo (pitch), y arrastrar con clic añade rotación táctil con retorno elástico suave como en Super Mario 64.

---

## 📌 Prompt 10: Humanización y Corrección del "Uncanny Valley" (Luz Cálida de Estudio vs. Sombras Tétricas)

### Texto del Prompt enviado a la IA:
> *"En el original de Tripo la apariencia era más agradable, en la nuestra se ve un poco tétrica, ¿hay algo que se pueda hacer? [adjuntando captura comparativa de Tripo vs. Three.js]"*

### Explicación y Justificación:
* **Qué se pidió**: Ajustar la iluminación, sombreado y tratamiento de materiales para eliminar el efecto de "valle inquietante" (*uncanny valley*) o apariencia cadavérica.
* **Diagnóstico y Solución Técnica**:
  1. **Eliminación de Luz Fría de Relleno**: La escena tenía una luz puntual cian/azul (`0x93c5fd`) a alta potencia que proyectaba tintes azulados sobre la piel, haciéndola lucir enferma. Se reemplazó por un relleno melocotón cálido (`0xffeedb`).
  2. **Luz Ambiental de Estudio Fotográfico**: Se añadió `THREE.AmbientLight(0xfff5ea, 1.7)` para rellenar las sombras oscuras del interior de la boca, cuencas oculares y cuello.
  3. **Destello Vital en los Ojos (*Catchlight*)**: Luz puntual frontal blanca que refleja un brillo en ambas pupilas, otorgando una mirada despierta y amigable.
  4. **Suavizado de Normales y Mateado de Piel**: Se eliminaron las facetas poligonales de la frente aplicando `shade_smooth` a 65,000 polígonos y ajustando la rugosidad PBR a 0.58 con mapeo tonal `ACESFilmicToneMapping` a 1.18.

---

## 📌 Prompt 11: Rediseño Auténtico del Logo de Pantalla de Título (Bloques de Madera 3D N64)

### Texto del Prompt enviado a la IA:
> *"Estas son las dos pantallas de bienvenida, la de nuestro juego y la original, tomando en cuenta que este juego no será compartido ni monetizado y que su existencia es efímera, ¿no es posible usar un diseño más parecido al original? [adjuntando capturas comparativas de la pantalla actual vs. el título original de Super Mario 64 en Nintendo 64]"*

### Explicación y Justificación:
* **Qué se pidió**: Abandonar la aproximación tipográfica plana de CSS y crear un logotipo idéntico al original de 1996: bloques tridimensionales de madera de pino con caras frontales de colores primarios vivos (Rojo, Azul, Amarillo, Verde), disposición curvada, el bloque "64" rojo con bisel dorado inclinado en perspectiva isométrica y el clásico aviso de copyright retro azul neón.
* **Diagnóstico y Solución Técnica**:
  - **Fallo de renderizado web en CSS**: La combinación de degradados `linear-gradient` con `-webkit-background-clip: text` y `text-shadow` pesada en navegadores modernos provoca que la sombra opaque el relleno o se renderice marrón oscuro a través de la transparencia del texto.
  - **Pipeline Automatizado en Blender 5.2 LTS (`render_super_bukele_logo.py`)**:
    1. Se modeló por script cada letra de "SUPER" y "BUKELE" en geometría 3D biselada utilizando la tipografía pesada Noto Sans Black.
    2. Se programó un shader de madera de pino procedural con coordenadas de textura estiradas y distorsión de vetas de aserrío para los laterales y bloques inferiores.
    3. Se separaron las normales de las caras frontales para asignar colores primarios con acabado de juguete plástico brillante:
       - **SUPER**: S (Rojo), U (Azul), P (Amarillo), E (Azul), R (Verde).
       - **BUKELE**: B (Azul), U (Verde), K (Amarillo), E (Rojo), L (Verde), E (Azul).
       - **64**: Extrusión profunda en rojo con laterales y biseles dorados, rotado -15° en la esquina superior derecha.
    4. Se renderizó en canal alfa transparente RGBA (1600x750) con iluminación solar cenital y luz de relleno cálida, integrándolo en la interfaz con animación sutil de flotación (`logoFloat`).


---

## 📌 Prompt 12: Mosaico Acolchado N64 para el Fondo de la Escena 2 con Tipografía Oficial de Mario 64

### Texto del Prompt enviado a la IA:
> *"Al igual en la escena 2, el fondo se puede mejorar con una fuente similar y colocar bukele 64 en el fondo. Revisa la carpeta /home/omarchy/Desktop/assets ahí te dejo la fuente, instálala y úsala y unos gifs que generé si eso te ayuda con la tarea [adjuntando capturas de la cuadrícula de mosaico azul original de Super Mario 64 con SUPER MARIO 64 repetido en celdas acolchadas]"*

### Explicación y Justificación:
* **Qué se pidió**: Instalar la tipografía oficial del juego original (`TypefaceMario64-ywA93.otf`) en el sistema operativo y en el proyecto web, y sustituir el fondo degradado provisional de CSS por una cuadrícula de mosaico fiel a Nintendo 64 donde cada baldosa muestre "SUPER BUKELE 64" en relieve 3D.
* **Diagnóstico y Solución Técnica**:
  1. **Instalación y Configuración de Fuente**:
     - Se instaló la fuente en `~/.local/share/fonts/` ejecutando `fc-cache -f -v` para disponibilidad en el SO y en Blender.
     - Se copió a `assets/fonts/TypefaceMario64.otf` y se declaró con `@font-face` en CSS para la interfaz web.
  2. **Modelado y Renderizado de Baldosa Procedural en Blender (`render_n64_tile.py`)**:
     - Se modeló una baldosa cuadrada ortográfica (512x512) con shader de viñeta radial (`ShaderNodeVectorMath` distancia de coordenadas UV al centro) mezclado con micro-ruido procedural para evocar la textura de tela/denim azul de la N64.
     - Se crearon los textos 3D en relieve con biselado: `SUPER` (arriba), `BUKELE` (abajo) en color celeste hielo reflectante, y `64` en rojo Nintendo intenso en el lateral derecho.
     - Se añadieron ranuras perimetrales oscuras en los 4 bordes para crear el característico efecto de celda acolchada al repetirse.
  3. **Integración Web y Tipografía Rainbow**:
     - Se configuró `.head-bg-mosaic` con repetición perfecta a 190x190px.
     - Se asignó la fuente Mario 64 al botón rainbow `PRESS START` de la esquina inferior izquierda.


---

## 📌 Prompt 13: Unificación Estética Total entre Escena 1 y Escena 2 (Fuente Mario 64 en Logo 3D y Fondo N64)

### Texto del Prompt enviado a la IA:
> *"La primer pantalla no tiene el diseño que sí tiene la segunda [adjuntando capturas comparativas de la pantalla de bienvenida con el logo anterior vs. la pantalla del rostro 3D con la tipografía y el fondo de mosaico N64]"*

### Explicación y Justificación:
* **Qué se pidió**: Resolver la discrepancia de diseño entre ambas pantallas iniciales para que la Escena 1 comparta el mismo ADN visual que la Escena 2:
  1. Que el logotipo 3D en bloques de madera utilice la geometría facetada oficial de `Typeface Mario 64` en lugar de una fuente genérica sans-serif.
  2. Que el fondo de la pantalla de título adopte la misma cuadrícula de mosaico acolchado azul N64 con viñeta cinematográfica.
  3. Que los textos de interfaz (`©2026 KODIGO ACADEMY` y `PRESS START`) adopten la tipografía auténtica del juego.
* **Diagnóstico y Solución Técnica**:
  - **Re-renderizado 3D en Blender (`render_super_bukele_logo.py`)**: Se sustituyó `NotoSans-Black` por `TypefaceMario64.otf`, recalculando las mallas poligonales biseladas para reproducir las aristas angulares características de las letras clásicas de Mario 64 (la B con muescas, la U con base pentagonal, el 64 emblemático).
  - **Composición del Fondo en Escena 1**: Se actualizó `.title-scene` con la textura de mosaico `n64_bg_tile.png` suavizada con un degradado radial oscuro que hace destacar el logo tridimensional flotante.
  - **Cohesión Tipográfica**: Se asignó `TypefaceMario64` al botón pulsante `PRESS START` y al copyright de Kodigo Academy.


---

## 📌 Prompt 14: Ajuste Espacial del Bloque "64" (Eliminación de Solapamiento con la R y Texto Inferior)

### Texto del Prompt enviado a la IA:
> *"Mucho mejor, vas muy bien, pero el 64 está sobre el demás texto, sepáralo por favor, ahora ya tenemos un punto de inicio bueno [adjuntando captura donde el número 64 cubría parcialmente la letra R y la E de Bukele]"*

### Explicación y Justificación:
* **Qué se pidió**: Reubicar el bloque tridimensional "64" en el render de Blender para garantizar legibilidad completa, evitando colisiones con la letra `R` de "SUPER" y la fila inferior de "BUKELE".
* **Diagnóstico y Solución Técnica**:
  - En la versión inicial con la tipografía oficial, el bloque "64" (de 1.85 unidades de ancho con alineación central en `x = 3.95`) extendía su caja delimitadora hacia `x = 2.75`, invadiendo el espacio de la `R` (`x = 2.4` a `3.1`).
  - Se recalculó la posición tridimensional en Blender (`render_super_bukele_logo.py`):
    - Se desplazó el "64" hacia la derecha a `x = 4.45` y se elevó a `z = 1.25`, logrando una separación limpia de más de 1.3 unidades respecto a la `R`.
    - Se reubicó el bloque "TM" a `(5.65, -0.25, 2.15)`.
    - Se reencuadró la cámara ortográfica en `x = 0.55` para centrar perfectamente la silueta extendida del logotipo.

---

## 📌 Prompt 15: Implementación de la Escena 3 ("SELECT FILE" Screen con Cursor de Mano 3D y Avance Global)

### Texto del Prompt enviado a la IA:
> *"Esta es la 3 pantalla del juego, básicamente permite seleccionar un perfil y el mouse tiene forma de una mano, pero para efectos de nuestro juego, en cualquier lugar de la pantalla que de clic pasará a la siguiente pantalla... Aprobado, puedes ver la secuencia en este video segundos 5 al 8 https://youtu.be/CL8rDvttmjY?si=ePAGF4OayX1eJiTF"*

### Explicación y Justificación:
* **Qué se pidió**: 
  1. Recrear con máxima fidelidad retro la tercera pantalla de la secuencia introductoria de *Super Mario 64*: la pantalla dorada de selección de partida ("SELECT FILE").
  2. Sustituir el cursor del sistema por la icónica mano enguantada blanca tridimensional de Mario 64, siguiendo el movimiento del ratón por toda la pantalla.
  3. Comportamiento interactivo simplificado: hacer clic en cualquier lugar de la pantalla o presionar `Enter`/`Espacio` transiciona inmediatamente a la siguiente escena (el nivel 3D en la pradera).
  4. Mantener la paleta cromática, los 4 slots de partida ("BUKELE A, B, C, D" con el rótulo multicolor "NEW"), los 4 bloques de comando biselados inferiores ("SCORE", "COPY", "ERASE", "STEREO") y el marco biselado dorado.
* **Diagnóstico y Solución Técnica**:
  - **Modelado y Renderizado del Cursor en Blender (`render_hand_cursor.py`)**: Se modeló proceduralmente en Blender la mano enguantada blanca de baja poligonalidad con material cel-shading retro, puño cilíndrico inclinado, dedo índice extendido hacia arriba a la izquierda y las costuras negras en el dorso, exportado a `assets/img/n64_hand_cursor.png` (256x256 RGBA).
  - **Generación del Retrato de Partida (`bukele_file_icon.png`)**: Se procesó el perfil de Nayib Bukele en escala de grises con contraste calibrado para integrarse en las miniaturas metálicas de los slots A, B, C y D.
  - **Composición de la Pantalla SELECT FILE (`index.html` + `css/style.css`)**:
    - Marco biselado dorado de 24px (`#fde047`, `#a16207`, `#713f12`, `#eab308`) sobre fondo satinado ámbar cálido.
    - Cabecera con tipografía `TypefaceMario64` en colores alternados verde, fucsia y amarillo con relieve sombreado.
    - Cuadrícula 2x2 de tarjetas de partida y botones inferiores cúbicos con biseles prismáticos.
  - **Integración en la Máquina de Estados (`js/game.js`)**:
    - Se incorporó `SCENE_3_FILESELECT` entre la interacción de la cabeza 3D (`SCENE_2_HEAD`) y el juego 3D (`SCENE_4_GAMEPLAY`).
    - Se implementó el cursor seguidor con coordenadas de ratón en tiempo real y posicionamiento automático inicial sobre el slot A.
    - Se configuró el listener global de clic y teclas de acción para avanzar inmediatamente al nivel 3D.

---

## 📌 Prompt 16: Integración Cinemática (Carta Parodia de Gabriela + Vuelo de Lakitu al Castillo)

### Texto del Prompt enviado a la IA:
> *"A partir del segundo 6 al 46 hay un video que no es interactivo en el juego original? podrias incrustar ese video? dame tu opinion? https://youtu.be/CL8rDvttmjY?si=1Hs8D5QKc1FyYDTN ... 2 [Selección de Opción 2: Carta adaptada a Bukele + Video del castillo]"*

### Explicación y Justificación:
* **Qué se pidió**: 
  1. Analizar la secuencia cinemática no interactiva de *Super Mario 64* (segundos 6 al 46) que sigue a la selección de archivo.
  2. Evaluar la viabilidad técnica y conveniencia de diseño de incrustar el video en el juego web.
  3. Ejecutar la **Opción 2**: Adaptar la pantalla de la carta introductoria a la narrativa de "Super Bukele 64" (la Primera Dama Gabriela invitando a Nayib Bukele al castillo) con su tema musical retro, y enlazarla suavemente con el video original remasterizado del vuelo de Lakitu sobrevolando el castillo de Peach antes de comenzar el nivel jugable.
* **Diagnóstico y Solución Técnica**:
  - **Aclaración de Motor Retro**: Se explicó que en la consola N64 esta secuencia no era un video pre-grabado sino una cinemática generada en tiempo real por el chip de la consola, pero que para el navegador un reproductor HTML5 optimizado brinda una fluidez perfecta a 60 fps sin coste de cómputo WebGL.
  - **Extracción y Optimización de Audio y Video**:
    - Se extrajo el tema musical de la carta (`assets/audio/letter_bgm.mp3`).
    - Se procesó el vuelo cinemático de Lakitu a 720p 60fps H.264 (`assets/video/lakitu_castle_flight.mp4`, 4.2 MB) para carga instantánea.
  - **Diseño del Pergamino de Gabriela (`#scene-letter`)**:
    - Estructura con textura de pergamino envejecido (`#fdfbf7` a `#eee1c4`), marco perimetral biselado dorado de 10px y sello real con corona.
    - Tipografía serif elegante con el texto parodia: *"Querido Nayib: Por favor ven al castillo. Te he preparado una sorpresa... Con cariño-- Primera Dama Gabriela"*.
  - **Transición y Flujo Cinematográfico (`js/game.js`)**:
    - El flujo secuencial se amplió: `Título` ➔ `Cabeza 3D` ➔ `Select File` ➔ `Carta de Gabriela` ➔ `Vuelo de Lakitu` ➔ `Gameplay 3D`.
    - Se incluyó la opción universal de saltar la cinemática en cualquier momento pulsando `[ESPACIO]` o haciendo clic.


