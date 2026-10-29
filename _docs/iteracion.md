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
