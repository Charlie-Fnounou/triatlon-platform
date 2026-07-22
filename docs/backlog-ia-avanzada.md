# Backlog — funcionalidades avanzadas de IA (post-MVP)

Especificaciones detalladas dadas por el usuario el 2026-07-22, para las fases
de IA/plan de entrenamiento (ver fases 3+ en `ARCHITECTURE.md`). No se
implementan en el MVP; quedan documentadas acá para no perderlas.

## Gestión de múltiples carreras (A/B/C Race)

- El usuario planifica una o varias carreras a la vez: **A Race** (principal),
  **B Race** (secundarias), **C Race** (preparación).
- La IA identifica automáticamente el objetivo principal y reorganiza el
  calendario alrededor de esas competencias.
- Agregar/eliminar/cambiar una carrera recalcula automáticamente todo el plan
  de entrenamiento, nutrición y recuperación.
- Cada carrera incluye: nombre, modalidad, fecha, hora, lugar, distancia,
  desnivel, clima estimado, tiempo objetivo, tiempo ideal, tiempo mínimo
  aceptable, prioridad (A/B/C), estado de preparación, probabilidad de
  alcanzar el objetivo.

## Sueño y recuperación inteligente

Plan diario de recuperación generado por IA:
- Hora ideal de acostarse / despertarse, horas de sueño recomendadas.
- Estimación de sueño profundo y REM.
- Necesidad y duración de siesta.
- Nivel de recuperación esperado, calidad del sueño, energía esperada del día.

Si el usuario duerme menos de lo recomendado, la IA ajusta automáticamente:
entrenamiento, nutrición, recomendaciones del día, y explica el impacto
esperado en el rendimiento.

## Plan diario inteligente (generado cada mañana)

Combina: estado físico, estado mental, nivel de recuperación, calidad del
sueño, clima → y genera: entrenamiento del día y su objetivo, nutrición
completa con horarios por comida, agua, electrolitos, cafeína (si aplica),
hora ideal para entrenar y para dormir, tiempo recomendado de pantallas antes
de dormir, estiramientos, movilidad, fuerza, respiración/meditación, tiempo de
recuperación.

## Adaptación automática (dinámica, sin planes fijos)

Toda la app se recalcula continuamente según: sueño, HRV, fatiga, estrés,
clima, viajes, lesiones, enfermedades, alimentación, entrenamientos
completados u omitidos, competencias próximas. Ningún plan debe quedar fijo.

## Coach de vida deportiva

La IA no es solo un entrenador: es un asistente personal de alto rendimiento
que optimiza entrenamiento, nutrición, recuperación, sueño, estrés,
organización del día y preparación de competencias — con la idea de que el
usuario solo necesite esta única app para gestionar toda su vida deportiva.
