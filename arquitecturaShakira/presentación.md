---
marp: true
theme: default
paginate: true
---

# Arquitectura IoT: Pulseras LED en el concierto de Shakira
**Caso de estudio de un sistema IoT masivo**
*(Tu Nombre / Tu Asignatura)*

---

# 1. Introducción al problema
- **El reto:** Sincronizar 60.000 pulseras LED en un estadio al mismo tiempo al ritmo de la música[span_0](start_span)[span_0](end_span).
- **Requisitos extremos:** 
  - Tienen que ser muy baratas (se regalan con la entrada)[span_1](start_span)[span_1](end_span).
  - La batería (pilas de botón) debe durar todo el concierto[span_2](start_span)[span_2](end_span).
  - No requieren ninguna configuración por parte del usuario (te la pones y funciona)[span_3](start_span)[span_3](end_span).
- **La solución contraintuitiva:** No usan WiFi ni Bluetooth para conectarse una a una, sino que actúan como si recibieran luz de una "linterna gigante[span_4](start_span)"[span_4](end_span).

# 2. Capa de Dispositivos (Percepción)
- **Componentes mínimos:** Cada pulsera lleva un microcontrolador de 8 bits muy básico, un receptor de infrarrojos (IR) y LEDs RGB[span_0](start_span)[span_0](end_span).
- **Energía:** Usan dos pilas de botón (CR1632) que duran todo el evento porque el chip pasa casi todo el tiempo "dormido" hasta que recibe luz IR[span_1](start_span)[span_1](end_span).
- **Lazo abierto:** Las pulseras solo reciben órdenes, nunca transmiten nada de vuelta ni confirman que se han encendido[span_2](start_span)[span_2](end_span).

---

# 3. Capa de Red (Transporte)
- **Emisión Broadcast por Infrarrojos:** Los transmisores del estadio envían pulsos de luz IR a todas las pulseras de una zona a la vez[span_3](start_span)[span_3](end_span).
- **Fiabilidad por repetición:** Como no hay confirmación de llegada (ACK), los transmisores envían la orden continuamente (cada ~6,3 ms) para que ninguna pulsera se quede apagada si pierde un destello[span_4](start_span)[span_4](end_span).
- **Pasarelas (Gateways):** Se usan nodos que traducen los protocolos de red estándar del espectáculo (Art-Net / sACN sobre Ethernet) a DMX512 físico, y de ahí a luz infrarroja[span_5](start_span)[span_5](end_span).

---

# 4. Capas de Procesamiento y Aplicación
- **Control centralizado:** En lugar de procesar datos en la pulsera, toda la "inteligencia" está en una consola de iluminación profesional (tipo grandMA)[span_6](start_span)[span_6](end_span).
- **El show y el operador:** La aplicación es un diseño previo de luces sincronizado con la pista musical (*timecode*), operado por un técnico que dispara las secuencias en directo para adaptarse a la música[span_7](start_span)[span_7](end_span).

---

# 5. ¿Cómo se hace el efecto de la "Ola"?
- **El truco de la infraestructura:** Las pulseras no saben en qué asiento del estadio están (no tienen GPS)[span_8](start_span)[span_8](end_span).
- **Zonas de emisión:** El estadio se divide en zonas físicas, cada una iluminada por un proyector IR direccional distinto[span_9](start_span)[span_9](end_span).
- **Secuencia:** La consola enciende las zonas en orden (ej: Zona A, 200ms después Zona B, etc.), creando visualmente la ola para el público[span_10](start_span)[span_10](end_span).


