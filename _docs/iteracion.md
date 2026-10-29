---
title: 4. Iteración y Mejora
description: "Ajustes del game feel en salto, diseño del modelo de Nayib Bukele y efectos visuales."
layout: default
nav_order: 4
permalink: /docs/iteracion/
---

# 4. Iteración y Mejora

## 🔄 El Bucle de Vibecoding: Ajustando el Comportamiento

En el desarrollo asistido por IA, la primera respuesta difícilmente cumple todas las expectativas de jugabilidad (*game feel*). A continuación se documentan las mejoras y modificaciones puntuales solicitadas:

### 1. Ajuste del "Game Feel" del Salto (Física e Inercia)
* **Comportamiento inicial**: El personaje salía disparado hacia arriba a velocidad fija y caía lentamente de golpe, sintiéndose ingrávido y difícil de controlar para aterrizar sobre las plataformas.
* **Instrucción de mejora dada a la IA**:
  > *"El salto se siente flotante. Aumenta la fuerza de gravedad a -32 unidades y dale una velocidad de despegue más rápida. Agrega además una pequeña inercia horizontal para que si el jugador corre antes de saltar, conserve el impulso hacia adelante en el aire."*
* **Resultado**: El control pasó de sentirse como un prototipo rígido a tener la clásica curva parabólica de Super Mario 64.

### 2. Estilizado Visual del Protagonista (Nayib Bukele)
* **Comportamiento inicial**: El personaje se generó con formas geométricas muy básicas y proporciones genéricas.
* **Instrucción de mejora dada a la IA**:
  > *"Ajusta el modelo 3D: Nayib debe llevar un saco azul marino con solapas visibles, camiseta negra interna, peinado oscuro estilizado hacia atrás y su característica barba bien delineada. Agrega una sombra circular semitransparente bajo sus pies proyectada sobre el suelo para que sea fácil calcular los aterrizajes."*
* **Resultado**: La silueta del personaje se volvió reconocible al instante y la sombra proyectada facilitó enormemente la precisión en los saltos.

### 3. Rotación y Resplandor de la Estrella
* **Comportamiento inicial**: La estrella era estática y se confundía con el cielo.
* **Instrucción de mejora dada a la IA**:
  > *"Haz que la Estrella Dorada oscile verticalmente con un seno matemático (bobbing) y gire constantemente sobre su eje Y. Añade una luz puntual dorada (`PointLight`) que emita resplandor sobre la cima de la colina."*
* **Resultado**: La cumbre del nivel se convirtió en un foco de atención visual inmediato para el jugador.
