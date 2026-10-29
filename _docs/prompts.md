---
title: 3. Evidencia de Prompts (Vibecoding)
description: "Registro y explicación de los 3 prompts progresivos utilizados para desarrollar el juego con IA."
layout: default
nav_order: 3
permalink: /docs/prompts/
---

# 3. Evidencia de Prompts (Vibecoding)

Uno de los requisitos indispensables de la actividad es evidenciar que el desarrollo **no fue un "one-shot" milagroso**, sino un proceso iterativo de **Vibecoding** donde el estudiante guía a la IA de manera progresiva.

---

## 📌 Prompt 1: Creación del Mundo Base, Cámara y Personaje 3D

### Texto del Prompt enviado a la IA:
> *"Quiero desarrollar un mini-juego 3D en el navegador usando Three.js que sirva como homenaje a Super Mario 64. Crea la estructura inicial en un archivo HTML con Three.js: una pradera verde con árboles low-poly y cielo azul. El personaje principal debe ser Nayib Bukele estilizado en 3D (traje azul marino, camiseta oscura, barba recortada y cabello negro hacia atrás). Agrega controles de movimiento en 3D con WASD y salto con Espacio, junto con una cámara en tercera persona que lo siga suavemente."*

### Explicación y Justificación:
* **Qué se pidió**: Inicializar la escena básica, iluminación ambiental/direccional, geometrías del personaje y física elemental de movimiento.
* **Por qué se acotó así**: Era vital establecer los cimientos del movimiento y la estética del personaje antes de saturar el prompt con niveles, enemigos o coleccionables. Si los controles o la cámara se sentían toscos, era el momento exacto para corregirlos.

---

## 📌 Prompt 2: Nivel 3D, Coleccionables (Bitcoins) y la Estrella Dorada

### Texto del Prompt enviado a la IA:
> *"Ahora necesitamos el nivel y los objetivos. Modifica la escena para agregar una colina escalable con rampas y un par de plataformas flotantes. Distribuye 5 monedas doradas flotantes de Bitcoin con rotación continua y detección de colisión con el jugador (deben desaparecer al tocarlas). En la cima de la colina, coloca una Estrella Dorada 3D brillante con resplandor para que funcione como el objetivo final."*

### Explicación y Justificación:
* **Qué se pidió**: Construir el diseño del nivel (*level design*), la mecánica de recolección y el punto de victoria.
* **Por qué se ajustó o refinó**: En la primera prueba de colisión, el personaje atravesaba las plataformas flotantes al saltar. Se refinó la instrucción para implementar una comprobación de altura y raycasting sobre las plataformas del escenario.

---

## 📌 Prompt 3: Efectos de Sonido (Web Audio API), HUD y Cinemática de Victoria

### Texto del Prompt enviado a la IA:
> *"Para completar el pulido: agrega un HUD en pantalla que muestre el contador de Bitcoins recolectados y el objetivo actual. Implementa efectos de sonido retro usando Web Audio API nativo (sonido 'boing' al saltar, 'pling' al recoger un Bitcoin y fanfarria al ganar). Cuando el jugador toque la Estrella Dorada, congela los controles, haz que la cámara enfoque de frente a Nayib celebrando y muestra un modal de felicitaciones indicando que la Princesa Gabriela ha sido rescatada de Bowser con opción de reiniciar."*

### Explicación y Justificación:
* **Qué se pidió**: Audio inmersivo, retroalimentación visual (HUD) y la pantalla de fin de juego con condición de victoria.
* **Por qué se ajustó o refinó**: Para evitar errores de carga de archivos de audio por bloqueos de CORS o URLs rotas en GitHub Pages, se especificó expresamente el uso del oscilador de la **Web Audio API** del navegador.
