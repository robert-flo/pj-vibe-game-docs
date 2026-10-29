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
