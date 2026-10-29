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

### 2. Implementación de las Skills Especializadas
Para garantizar que el juego no fuese un simple conjunto de primitivas genéricas, se aplicó rigurosamente el protocolo de las dos skills de desarrollo:
* **`game-builder`**:
  * Definición formal del **Stage A**: `BRIEF.md` (bloqueado), matriz de referencias visuales bloqueadas en `refs-locked/` (`ref-01` a `ref-04`), registro de activos en `art/LEDGER.md` y la barra visual `art/BAR.md` (criterios universales C1–C5 + C6 tipografía N64 + C7 vestimenta ceremonial).
* **`game-builder-blender-assets`**:
  * En lugar de construir al personaje con cajas en el motor web, se ejecutó un pipeline en **Blender 5.2.2 LTS** (`build_bukele.py`).
  * Se modeló a Nayib Bukele en Blender con su chaquetón ceremonial negro, cuello mandarín con bordados dorados, la banda presidencial azul y blanco con el escudo nacional, peinado y barba característica.
  * Superó la compuerta de validación (*turnaround gate*) con renders frontal, lateral y posterior (`artifacts/stills/`), exportándose como asset oficial **`assets/models/bukele.glb`** que se carga en Three.js con `GLTFLoader`.
