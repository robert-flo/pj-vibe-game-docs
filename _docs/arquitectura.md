---
title: 2. Decisiones Técnicas y Arquitectura
description: "Arquitectura del motor en Three.js, pipelines offline en Blender/Python, raycasting 3D y audio híbrido."
layout: default
nav_order: 2
permalink: /docs/arquitectura/
---

# 2. Decisiones Técnicas y Arquitectura

## 🧱 Estructura de Dos Repositorios Independientes

Para mantener separación estricta entre el software interactivo y la memoria académica evaluable, el trabajo se organizó en dos repositorios con historiales de commits atómicos:

1. **Repositorio del Juego (`pj-vibe-game`)**:
   * Motor WebGL en **Three.js** (ES Modules sin empaquetadores opacos, legible directamente desde `index.html`, `css/style.css` y `js/game.js`).
   * Carpeta `scripts/` con los pipelines reproducibles en Python y Blender 5.2 LTS para construcción de activos `.glb` y síntesis de audio `.m64`.
   * Despliegue directo en GitHub Pages a pantalla completa.
2. **Repositorio de Documentación (`pj-vibe-game-docs`)**:
   * Construido con **Jekyll** y **`jekyll-vitepress-theme`**.
   * Conserva el historial cronológico íntegro de los 19 prompts, las 18 iteraciones, capturas intermedias de errores reales y análisis de ingeniería.

---

## 🔄 Evolución de la Máquina de Estados de Escenas

La arquitectura comenzó con 3 estados básicos en las primeras iteraciones y creció de forma modular hasta una máquina de **8 estados** sincronizados entre capas DOM/CSS y la escena WebGL:

```
[1. SCENE_1_TITLE]      Pantalla de título con logo 3D en bloques N64 y mosaico azul
        │ (Click / Enter / Espacio)
        ▼
[2. SCENE_2_HEAD]       Cabeza 3D interactiva de Bukele (seguimiento de ratón + headPivot)
        │ ( Botón Rainbow PRESS START / Enter tras cooldown de 2.2s )
        ▼
[3. SCENE_3_FILESELECT] Tablero dorado SELECT FILE (BUKELE A-D) + cursor de mano 3D N64
        │ (Any-Click / Enter / Espacio)
        ▼
[4. SCENE_4_LETTER]     Pergamino real de la Primera Dama Gabriela + arpegio de piano
        │ (Click / Enter / Espacio)
        ▼
[5. SCENE_5_CINEMATIC]  Vuelo de Lakitu (corte exacto seg 26.5 -> 49.0 en tubería verde)
        │ (Fin del clip o salto con Espacio / Click)
        ▼
[6. SCENE_6_GAMEPLAY]   Relevo 3D junto a la tubería en Peach's Castle Grounds HD
        │ (Cruzar el puente y llegar al pórtico Z ≈ -29.5, Y > 7.2)
        ▼
[65. SCENE_DOOR_OPENING] Apertura exterior (±1.62 rad) de las puertas estelares + caminata
        │ (1.75s independientes de FPS)
        ▼
[7. SCENE_VICTORY]      "Here we go!" + Star Fanfare + Modal de estadísticas y reinicio
```

---

## ⚙️ Arquitectura en Tiempo de Ejecución (`js/game.js`)

```
┌──────────────────────────────────────────────────────────────────────┐
│                   Bucle Principal (animate / rAF)                    │
│     Delta acotado + animación UV (cascada, foso) + banderas +        │
│             billboards en eje Y para los 26 árboles HD               │
└──────────────────────────────────┬───────────────────────────────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          ▼                        ▼                        ▼
┌───────────────────┐    ┌───────────────────┐    ┌───────────────────┐
│ Control & Entrada │    │ Física Raycasting │    │ Cámara & Interfaz │
│ WASD / Flechas /  │    │ sampleGround() y  │    │ 3ª persona lerp + │
│ Salto / Arrastre  │    │ wallAhead() mundo │    │ diálogos carteles │
└─────────┬─────────┘    └─────────┬─────────┘    └─────────┬─────────┘
          └────────────────────────┼────────────────────────┘
                                   ▼
┌──────────────────────────────────────────────────────────────────────┐
│                        Escena WebGL (Three.js)                       │
│  • castle_grounds.glb (terreno, puente, fachada, torre central, alfa)│
│  • castle_door.glb (2 hojas articuladas) + wooden_signpost.glb (x4)  │
│  • bukele_body.glb + clon bukele_head.glb (recorte GLSL en cuello)   │
│  • 10 Bitcoins (₿) + tubería verde N64 + domo oceánico de cielo      │
└──────────────────────────────────────────────────────────────────────┘
```

### Subsistemas Técnicos Clave:
1. **Instanciación Única y Shader GLSL de Recorte (`onBeforeCompile`)**:
   * El modelo `bukele_head.glb` (12 MB) se descarga **una sola vez** por red: la malla original alimenta la Escena 2 y un clon con material independiente se inyecta sobre `bukele_body.glb` para el gameplay.
   * Un bloque GLSL inyectado en el *fragment shader* descarta (`discard`) los fragmentos inferiores del busto y cuello trasero según coordenadas locales `vHeadPos`, logrando un ensamble limpio con el saco azul marino de `assets2`.
2. **Física por Raycasting con Normales en Espacio de Mundo**:
   * En lugar de cajas estáticas limitadas a planos rectangulares, `sampleGround(x, z, fromY)` y `wallAhead(dx, dz)` lanzan rayos contra las 25 mallas reales de `castle_grounds.glb`.
   * Las normales locales de triángulo (`hit.face.normal`) se transforman a espacio de mundo mediante `transformDirection(object.matrixWorld)` para distinguir con exactitud pendientes caminables (`|ny| > 0.42`) de muros verticales (`|ny| < 0.55`), sumando cilindros de colisión para los 26 troncos de árbol.
3. **Sistema de Audio Híbrido (Síntesis `.m64` + Web Audio API)**:
   * **Capa Principal**: Pistas y efectos auténticos renderizados desde secuencias `.m64` y muestras `.aiff` (`castle_grounds_bgm.mp3`, `star_fanfare.mp3`, `coin.mp3`, `door_open.mp3` y voces de salto).
   * **Capa de Respaldo (`RetroAudio`)**: Sintetizador procedural con `AudioContext` (ondas triangulares, cuadradas y senoidales) que garantiza respuesta sonora inmediata incluso si un recurso externo es bloqueado.

---

## 🛠️ Pipelines Offline de Activos y Audio (`scripts/`)

| Script | Función en la Arquitectura |
|---|---|
| `scripts/render_super_bukele_logo.py` | Genera en Blender el logotipo 3D extruido en bloques de madera con `TypefaceMario64.otf`. |
| `scripts/render_hand_cursor.py` | Modela y renderiza en Blender la mano enguantada blanca 3D para la pantalla *SELECT FILE*. |
| `scripts/build_bukele_hero.py` | Construye `assets/models/bukele_body.glb` con extremidades articuladas (`ArmL/R`, `LegL/R`) y atuendo formal azul marino oscuro + camiseta negra. |
| `scripts/export_castle_grounds.py` | Ejecuta las listas de despliegue RSP (`gsSPDisplayList`), hornea iluminación `gdSPDefLights1`, asocia las 27 texturas HD `RENDER96` y exporta `castle_grounds.glb`. |
| `scripts/export_castle_actors.py` | Exporta los actores independientes `castle_door.glb` (emblema estelar simétrico) y `wooden_signpost.glb`. |
| `scripts/render_sm64_audio.py` | Decodifica secuencias `.m64` junto con bancos JSON y muestras PCM `.aiff`, aplicando articulación `noteDuration` para generar los MP3 del juego. |
| `scripts/shot.sh` | Automatiza capturas de verificación en Chromium headless con aceleración WebGL SwiftShader (`?scene=6&pos=...&cam=...`). |
