---
title: 5. Validación y Corrección de Bugs
description: "Metodología de pruebas y solución a bugs críticos de salto infinito y permisos de audio."
layout: default
nav_order: 5
permalink: /docs/validacion/
---

# 5. Validación y Corrección de Bugs

## 🧪 Metodología de Pruebas

Para validar el funcionamiento del juego se aplicó una batería de pruebas manuales y en consola del navegador (Chrome DevTools):

1. **Prueba de Rendimiento (Frame Rate)**:
   * Verificación de tasa de refresco estable a **60 FPS** continuos sin caídas de frames ni fugas de memoria en Three.js.
2. **Prueba de Límites del Escenario**:
   * Intentar salir del mapa o caer al vacío para comprobar que el personaje reaparezca (*respawn*) de forma segura en el punto de partida en lugar de caer indefinidamente.
3. **Prueba de Colisiones y Aterrizaje**:
   * Saltar sobre cada plataforma desde diferentes ángulos para validar que la altura `Y` del jugador coincida exactamente con la superficie del bloque.
4. **Prueba de Condición de Victoria**:
   * Recolectar o ignorar Bitcoins y tocar la Estrella Dorada para confirmar que el estado del juego se congele correctamente y se muestre la interfaz de fin de nivel.

---

## 🐛 Errores Identificados y Ajustes Realizados

### Error 1: Salto Infinito en el Aire (*Air-Jumping*)
* **Descripción del fallo**: Si el usuario presionaba la barra espaciadora repetidamente mientras caía, el personaje seguía saltando en el aire infinitamente como si volara.
* **Causa técnica**: La variable booleana `isGrounded` no comprobaba si el personaje estaba realmente en contacto con el suelo o una plataforma antes de permitir la aplicación de la velocidad vertical positiva.
* **Solución aplicada**: Se implementó una verificación estricta:
  ```javascript
  if (keys['Space'] && isGrounded) {
    velocityY = JUMP_FORCE;
    isGrounded = false;
    audio.playJump();
  }
  ```

### Error 2: Bloqueo del Contexto de Audio en el Navegador
* **Descripción del fallo**: La consola mostraba la advertencia: `The AudioContext was not allowed to start. It must be resumed after a user gesture on the page`. Los sonidos no se escuchaban.
* **Causa técnica**: Las políticas de seguridad modernas de navegadores (Autoplay Policy) prohíben que una pestaña emita audio sin una interacción previa del usuario.
* **Solución aplicada**: Se configuró la reanudación del `AudioContext` en el primer evento `keydown` o `pointerdown` del usuario.
