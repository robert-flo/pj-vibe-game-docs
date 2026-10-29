---
title: 1. Introducción y Concepto
description: "Contexto de la actividad, concepto del juego Super Bukele 64 y justificación de herramientas."
layout: default
nav_order: 1
permalink: /docs/introduccion/
---

# 1. Introducción y Concepto

## 🎯 Contexto y Objetivo
Esta actividad individual de **Semana 2** tiene como propósito aplicar técnicas de **vibecoding** y **prompt engineering** utilizando la inteligencia artificial como copiloto de desarrollo, demostrando:
* Dirección y control mediante prompts progresivos y claros.
* Comprensión del código generado.
* Iteración sobre la lógica, controles y estética.
* Capacidad de validación y resolución de errores.

---

## 🎮 Concepto: *Super Bukele 64: Misión Rescate*

### Inspiración
El proyecto toma como referencia el icónico inicio de **Super Mario 64** (el patio del castillo y la primera misión de *Bob-omb Battlefield*). En lugar de intentar replicar un juego completo e inabarcable, se diseñó una **Vertical Slice (Demo de 1 Estrella)**: un micro-nivel 3D autocontenido, completamente jugable y pulido, con objetivo de victoria claro.

### Trama y Personajes
* **El Héroe (Nayib Bukele)**: Modelado en estilo *low-poly* reminiscente de la era Nintendo 64, con sus rasgos distintivos (traje azul marino formal, camiseta oscura, barba y bigote recortados, y cabello engominado hacia atrás).
* **El Objetivo (Princesa Gabriela)**: Esposa del protagonista y Primera Dama, quien ha sido encerrada en la fortaleza por el villano Bowser.
* **El Antagonista (Bowser)**: Ha bloqueado el acceso al castillo con sellos mágicos que solo se rompen al reunir la primera **Estrella Dorada**.
* **Coleccionables (Bitcoins Dorados)**: Monedas doradas flotantes con el símbolo de Bitcoin que giran en el escenario y aumentan la puntuación del jugador.
* **La Estrella de Victoria**: Una estrella tridimensional dorada situada en lo alto de la colina que, al ser alcanzada, activa la cinemática de victoria y el mensaje de rescate.

---

## 🛠️ Decisiones Iniciales y Entorno de Desarrollo

### 1. ¿Por qué Three.js en el navegador en lugar de Python?
Aunque la guía inicial de la asignatura sugería Python (como Pygame), el catedrático permitió libre elección tecnológica. Se optó por **Three.js (WebGL)** en el navegador por razones clave:
1. **Accesibilidad inmediata para el evaluador**: El catedrático puede abrir el juego directamente desde un enlace de GitHub Pages en cualquier navegador (Chrome, Firefox, Safari) sin instalar intérpretes de Python ni lidiar con dependencias de librerías locales.
2. **Capacidades 3D reales**: Permite una cámara en tercera persona dinámica, iluminación direccional y sombras, y renderizado espacial fiel al homenaje de Mario 64.
3. **Audio sin dependencias externas pesadas**: Empleo de la **Web Audio API** para sintetizar efectos retro en tiempo real directamente desde el navegador.

### 2. Exploración de herramientas avanzadas (Skills)
Durante la fase previa de preparación, se investigaron e instalaron en el entorno de desarrollo dos skills especializadas:
* `game-builder`: Metodología para guiar la paridad visual entre referencias de juegos comerciales y prototipos generados por IA.
* `game-builder-blender-assets` y suite completa de **Blender 5.2 LTS**: Para evaluar el modelado de assets 3D en formato GLB.
* **Conclusión de diseño**: Para mantener el código comprensible, auditable por el estudiante y de carga ultrarrápida en GitHub Pages, se optó por construir la geometría de Nayib y los props de forma procedural estilizada directamente con primitivas agrupadas y materiales optimizados de Three.js.
