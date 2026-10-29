---
title: 2. Decisiones Técnicas y Arquitectura
description: "Estructura modular del motor en Three.js, bucle de renderizado y Web Audio API."
layout: default
nav_order: 2
permalink: /docs/arquitectura/
---

# 2. Decisiones Técnicas y Arquitectura

## 🧱 Estructura de Dos Repositorios

Para asegurar un proyecto limpio de nivel profesional, se dividió el trabajo en dos repositorios independientes:

1. **Repositorio del Juego (`pj-vibe-game`)**:
   * Contiene el código fuente del motor web (Three.js), físicas, controladores de cámara, lógica de colisiones y HUD.
   * Despliegue automatizado en GitHub Pages como aplicación web a pantalla completa.
2. **Repositorio de Documentación (`pj-vibe-game-docs`)**:
   * Construido con **Jekyll** y el tema **`jekyll-vitepress-theme`** de Carmine Paolino.
   * Contiene el reporte académico exigido por la rúbrica de la Semana 2, tablas de prompts, evidencias de bugs y análisis de aprendizaje.

---

## ⚙️ Arquitectura del Motor (Three.js)

El juego se organiza en torno a módulos desacoplados para garantizar que el código sea fácil de explicar y mantener:

```
┌────────────────────────────────────────────────────────┐
│                      Game Loop                         │
│  (requestAnimationFrame con delta time normalizado)    │
└───────────────────────────┬────────────────────────────┘
                            │
       ┌────────────────────┼────────────────────┐
       ▼                    ▼                    ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Input & Move │     │  Collision   │     │ Camera & HUD │
│ Controller   │     │   & Physics  │     │  Controller  │
└──────────────┘     └──────────────┘     └──────────────┘
       │                    │                    │
       ▼                    ▼                    ▼
┌────────────────────────────────────────────────────────┐
│                   Three.js WebGL Scene                 │
│      (Personaje Nayib, Monedas Bitcoin, Estrella)      │
└────────────────────────────────────────────────────────┘
```

### Componentes Principales:
1. **Máquina de Estados de Escenas**:
   * **Escena 1 (Title Screen)**: Logotipo 3D biselado con textura de madera y licencia `©2026 Kodigo Academy`.
   * **Escena 2 (3D Bukele Head Screen)**: Pantalla icónica con la cabeza 3D de Nayib Bukele (modelada en Blender), fondo en mosaico azul "SUPER BUKELE 64", seguimiento de cursor de ratón en tiempo real y tipografía arcoíris "PRESS START".
   * **Escena 3 (Gameplay 3D)**: Nivel en tercera persona con físicas, colisiones de plataformas, recolección de Bitcoins y la Estrella.
   * **Escena de Victoria**: Cinemática con fanfarria y saludo presidencial.
2. **Bucle Principal (`animate`)**: Utiliza `requestAnimationFrame` y calcula un `delta` temporal para asegurar que la velocidad del salto y carrera sea idéntica sin importar los Hz del monitor.
3. **Controlador del Personaje**: Sistema con aceleración, desaceleración (fricción con el suelo), rotación suave hacia la dirección de movimiento y salto parabólico con gravedad constante.
4. **Cámara en Tercera Persona (Orbital)**: Sigue al personaje manteniendo una distancia y altura fijas con interpolación lineal (`lerp`), evitando movimientos bruscos.
5. **Sintetizador Web Audio API**: No requiere descargar archivos `.mp3` o `.wav` de servidores externos; sintetiza ondas cuadradas y senoidales en tiempo real para simular el sonido de salto, recolección de moneda y fanfarria.
