# Arquitectura — plataforma de entrenamiento para triatlón (nombre por definir)

## Visión completa (para no perderla de vista)

Plataforma todo-en-uno para triatletas y deportistas de resistencia: entrenamiento
inteligente con IA, análisis de rendimiento, nutrición, recuperación, comunidad y
coaching profesional. A futuro: todos los deportes de resistencia, todas las
distancias, apps nativas (iOS/Android/Apple Watch/Wear OS), integración con
Garmin/Strava/Polar/Suunto/COROS/Whoop/Oura/etc., marketplace de entrenadores.

## Alcance real del MVP (decidido con el usuario, 2026-07-21)

Esa visión completa es un proyecto de varios años con equipo y presupuesto. Para
que exista algo real y útil pronto, el MVP se acota a:

- **Un deporte:** triatlón (natación, ciclismo, running como disciplinas).
- **Una plataforma:** web (Next.js), responsive. Nada de apps nativas todavía
  (requieren cuentas de pago: Apple Developer 99 USD/año, Google Play 25 USD
  único — se evalúan cuando el proyecto tenga usuarios reales).
- **Registro manual de entrenamientos primero.** Sincronización automática con
  Garmin/Strava/etc. queda para cuando haya cuentas de desarrollador aprobadas
  con esos proveedores (proceso de partner, no instantáneo).
- **IA como asistente de texto** (Anthropic API) para explicar métricas y sugerir
  entrenamientos — no todavía "coach 24/7" con todas las señales biométricas.

Todo lo demás de la visión original queda como **backlog priorizado**, no
descartado: se aborda fase por fase a medida que el MVP funcione y tenga sentido
seguir invirtiendo tiempo/dinero.

## Stack

Mismo patrón que ya funciona en producción en el proyecto hermano World Runner
(gratis para empezar, probado, sin sorpresas):

- **Next.js 16 (App Router) + TypeScript + Tailwind** — frontend y backend en el
  mismo proyecto (server actions / route handlers), sin separar en microservicios
  todavía. Un monolito bien organizado por dominio escala perfectamente para esta
  etapa y es mucho más simple de operar para un equipo de una persona.
- **PostgreSQL en Supabase** (plan gratis) + **Prisma 6** como ORM (NO usar
  Prisma 7: mueve la configuración a `prisma.config.ts` y rompe el flujo estándar
  `url`/`directUrl` con el pooler de Supabase — lección ya aprendida en World
  Runner, ver `prisma/schema.prisma`).
- **Supabase Auth** para login (email + Google, igual que World Runner).
- **Vercel** (hosting, plan gratis) con despliegue automático en cada push a
  GitHub.
- **IA:** API de Anthropic (Claude), llave solo en el servidor.

## Modelo de datos (MVP)

Ver `prisma/schema.prisma`, entidades principales:

- **Usuario** — perfil del atleta (peso, altura, sexo, nivel).
- **Umbral** — FTP de ciclismo, ritmo umbral de running/natación, FC máx/reposo,
  **con historial temporal** (cada umbral tiene una fecha de vigencia). Esto
  importa porque las métricas de una actividad deben calcularse con el umbral
  que estaba vigente *en esa fecha*, no con el actual — si no, el historial de
  carga de entrenamiento queda distorsionado cada vez que el atleta mejora.
- **Actividad** — un entrenamiento registrado (disciplina, duración, distancia,
  FC, potencia, ritmo, TSS calculado).
- **PlanEntrenamiento** / **SesionPlan** — plan hacia una carrera objetivo
  (sprint, olímpico, medio Ironman, Ironman...), con sesiones programadas que se
  vinculan a la actividad real cuando el atleta la completa.
- **RegistroComida** — nutrición diaria (calorías, macros), manual por ahora.
- **MensajeIA** — historial de conversación con el asistente de IA.

## Plan de fases

0. **Cuentas** — GitHub, Supabase, Vercel para este proyecto (nuevos, separados
   de World Runner). Requiere acción del usuario.
1. **MVP en producción** — login, perfil, registrar entrenamientos a mano,
   dashboard con métricas básicas (TSS, CTL/ATL/TSB), historial.
2. **Planes de entrenamiento** — crear un plan hacia una carrera objetivo con
   sesiones semanales, marcar sesiones completadas.
3. **IA asistente** — chat que explica métricas y sugiere ajustes al plan.
4. **Nutrición** — registro de comidas y recomendaciones básicas.
5. **Sincronización automática** — Strava primero (API pública, sin proceso de
   partner), después Garmin/otros (requieren aprobación de partner).
6. **Comunidad y monetización** — según cómo vaya lo anterior.

## Qué NO se toca de este repo

Se descubrió por accidente una carpeta `endurance-platform` en Downloads (backend
Python/FastAPI de origen desconocido, no reconocida por el usuario). Por decisión
explícita del usuario, este proyecto **no tiene ninguna relación** con esa carpeta
ni la reutiliza.
