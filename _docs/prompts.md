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
