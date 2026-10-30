---
title: 6. Reflexión Académica
description: "Análisis pedagógico sobre el aprendizaje con IA, ventajas y límites del vibecoding y áreas técnicas trabajadas."
layout: default
nav_order: 6
permalink: /docs/reflexion/
---

# 6. Reflexión Académica

## 🎓 Respuestas a los Cuestionamientos de la Rúbrica

### a. ¿Qué aprendí usando la Inteligencia Artificial para programar?
Aprender a construir software interactivo mediante **vibecoding guiado** transforma el rol del estudiante: de ser un redactor aislado de sintaxis a desempeñarse como **director técnico, arquitecto de sistemas e ingeniero de control de calidad**. A lo largo de las 18 iteraciones comprobé que el resultado nunca depende de un "prompt mágico", sino de descomponer problemas complejos (como replicar la secuencia introductoria de *Super Mario 64*, ensamblar mallas 3D en Blender o depurar normales de colisión) en entregas pequeñas, verificables y respaldadas por commits atómicos.

### b. ¿Qué ventajas y límites identifiqué del Vibecoding?
* **Ventajas**:
  1. *Iteración interdisciplinaria acelerada*: Permitió conectar herramientas muy distintas en un mismo flujo: Three.js/WebGL en el navegador, scripts de Blender en Python, edición precisa de video con FFmpeg y decodificación de secuencias musicales `.m64`.
  2. *Capacidad de refinamiento progresivo*: Partir de una colina prototipo funcional facilitó escalar con seguridad hacia el exterior completo de *Peach's Castle Grounds* con texturas HD sin romper la base jugable.
  3. *Documentación y trazabilidad en vivo*: Mantener registros estructurados (`PLAN.md`, `art/LEDGER.md`, `next.md`) hizo posible auditar cada decisión tomada.
* **Límites**:
  1. *El espejismo del código que "compila pero falla visualmente"*: Varios errores críticos (terreno multicolor por normales firmadas N64, personajes hundiéndose porque `hit.face.normal` venía en espacio local, o el símbolo `₿` invertido en tapas UV cilíndricas) no arrojaban ninguna excepción en consola; solo pudieron descubrirse exigiendo capturas reales del motor y revisándolas con ojo crítico.
  2. *El peligro del "One-Shot"*: Intentar resolver geometría, audio, cinemáticas y físicas en una sola instrucción produce acoplamientos frágiles; el control humano etapa por etapa fue indispensable.
  3. *Criterio estético, narrativo y "Game Feel"*: La sincronía exacta del corte en el segundo 49.0 sobre la tubería verde, el tono humorístico de los carteles o la sensación del salto y la apertura de las puertas dependen íntegramente de la dirección humana.

### c. ¿Qué partes del código comprendo y cuáles necesito reforzar?
* **Partes que comprendo plenamente**:
  * La máquina de 8 estados de escena que coordina superposiciones DOM/CSS con la escena tridimensional de Three.js (`js/game.js`).
  * El bucle principal `requestAnimationFrame`, la integración de gravedad/salto con paso de tiempo acotado y el seguimiento suave de cámara con interpolación lineal (`lerp`).
  * El uso de `Raycaster` para detectar altura de terreno (`sampleGround`) y paredes (`wallAhead`), incluyendo por qué es obligatorio transformar las normales locales de la malla a coordenadas de mundo (`matrixWorld`).
  * La carga asíncrona de activos `.glb` mediante `GLTFLoader` y la reutilización en memoria por clonación.
* **Áreas a seguir reforzando conceptualmente**:
  * Programación de *shaders* personalizados en GLSL (`onBeforeCompile`) más allá del recorte geométrico `discard` aplicado al cuello del personaje.
  * Formato interno de listas de despliegue gráficas RSP (`Fast3D`) y secuenciadores de síntesis por tabla de ondas (`.m64` / bancos PCM) de consolas de 64 bits.
  * Optimización avanzada de mallas y texturas (compresión Draco / KTX2) para reducir aún más los tiempos de carga inicial en dispositivos móviles.
