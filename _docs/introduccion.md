---
title: 1. Introducción y Concepto
description: "Contexto de la actividad, evolución del concepto Super Bukele 64 y justificación de herramientas."
layout: default
nav_order: 1
permalink: /docs/introduccion/
---

# 1. Introducción y Concepto

## 🎯 Contexto y Objetivo
Esta actividad individual de **Semana 2** tiene como propósito aplicar técnicas de **vibecoding** y **prompt engineering** utilizando la inteligencia artificial como copiloto de desarrollo, demostrando de forma trazable **todo el proceso evolutivo** (y no únicamente el producto final):
* Dirección y control mediante **19 prompts progresivos** documentados paso a paso.
* Comprensión profunda de la arquitectura, matemáticas 3D, shaders y síntesis de audio.
* Iteración continua sobre geometría, iluminación, texturas, controles e interfaz.
* Diagnóstico empírico y corrección verificada de errores visuales y físicos reales.

---

## 🎮 Concepto y Evolución del Alcance: *Super Bukele 64*

### De un *Vertical Slice* Prototipo al Exterior Completo del Castillo
El proyecto partió como una *Vertical Slice* acotada (una colina geométrica con 5 Bitcoins y una estrella en la cima) para validar el bucle base en Three.js. Una vez consolidados los cimientos, la dirección iterativa permitió expandir el alcance hasta **replicar fielmente toda la secuencia introductoria y el exterior completo del Castillo de Peach (*Castle Grounds* de *Super Mario 64*)**:

1. **Secuencia Introductoria Canónica de 5 Escenas**:
   * **Escena 1**: Logotipo 3D en bloques facetados (*SUPER BUKELE 64*) sobre mosaico azul N64.
   * **Escena 2**: Rostro 3D interactivo de Nayib Bukele con seguimiento elástico del ratón e iluminación de estudio.
   * **Escena 3**: Tablero dorado *SELECT FILE* (`BUKELE A–D`) con cursor de mano enguantada 3D.
   * **Escena 4**: Pergamino real donde la Primera Dama Gabriela invita a Nayib al castillo con arpegio musical clásico.
   * **Escena 5**: Cinemática de vuelo de Lakitu calibrada al fotograma exacto en que emerge la tubería verde N64 (segundo 49.0), cediendo el relevo sin cortes al motor WebGL 3D.
2. **Escena 6 — Exterior Completo de *Peach's Castle Grounds* (Texturas HD)**:
   * Geometría auténtica de los jardines, colinas, foso perimetral, puente central de piedra, fachada con vitral, torreones con 4 banderas ondeantes, torre central alta con asta, cascada animada, 26 árboles clásicos con texturas HD de `RENDER96`, 4 carteles cómicos de madera con diálogo estilo N64 y **10 Bitcoins dorados (`₿`)** que guían el camino.
3. **El Héroe (Nayib Bukele)**:
   * Evolucionó en tres generaciones documentadas: (a) maniquí low-poly ceremonial en Blender (`bukele.glb`), (b) busto de alta resolución optimizado de 1.95M a 35k polígonos (`bukele_head.glb`) para la pantalla interactiva, y (c) cuerpo articulado formal con saco azul marino oscuro, camiseta negra y zapatos cafés (`bukele_body.glb`) ensamblado con la cabeza 3D recortada limpiamente en GPU mediante shader GLSL.
4. **Cierre Narrativo en las Puertas Estelares**:
   * Al cruzar el puente y llegar al pórtico real, ambas puertas de madera con emblema estelar dorado se abren hacia afuera sobre la alfombra roja con su sonido original de madera, Bukele entra al castillo, suena *"Here we go!"* seguido de la fanfarria clásica de victoria y se despliega el resumen estadístico de Bitcoins recolectados y tiempo de recorrido (`MM:SS`).

---

## 🛠️ Decisiones Tecnológicas y Pipeline de Herramientas

### 1. ¿Por qué Three.js (WebGL) en el navegador en lugar de un ejecutable local?
Aunque la guía inicial sugería opciones de escritorio como Python/Pygame, el catedrático permitió libre elección tecnológica. Se eligió **Three.js (WebGL ES Modules)** por tres razones académicas y prácticas:
1. **Evaluación instantánea sin fricción**: El catedrático puede jugar e inspeccionar el proyecto en un clic desde GitHub Pages sin instalar intérpretes ni dependencias locales.
2. **Renderizado 3D en tiempo real**: Cámara orbital en tercera persona, raycasting espacial en espacio de mundo, materiales con canal alfa, billboards en eje Y y modificación de shaders (`onBeforeCompile`).
3. **Sistema de Audio Híbrido**: Combina un sintetizador procedural en **Web Audio API** (`RetroAudio`) como respaldo sin dependencias con pistas y efectos originales extraídos y sintetizados desde secuencias `.m64` y muestras PCM `.aiff` de *Super Mario 64*.

### 2. Pipeline Multi-Herramienta Guiado por Metodología Estructurada
* **Diseño por Compuertas Visuales (`BRIEF.md`, `PLAN.md`, `art/BAR.md`, `art/LEDGER.md`)**: Ningún activo se dio por válido sin verificación visual mediante capturas en vivo desde el motor (`scripts/shot.sh` con Chromium headless + SwiftShader WebGL).
* **Modelado y Conversión Automatizada en Blender 5.2 LTS (`scripts/*.py`)**: Scripts reproducibles en Python para generar logotipos 3D, cursor enguantado, cuerpo articulado de Bukele y conversión de listas de despliegue RSP de Nintendo 64 (`gsSPDisplayList`, `gdSPDefLights1`) a formato estándar `.glb`.
