# Registro del experimento — Chatbot de comunicación estudiantes-secretaría

## 1. Punto de partida
- Hipótesis priorizada: Que Claude API + el reglamento de la facultad alcanzan para entrenar un bot que responda con precisión (≥90%) sin errores que hagan perder confianza (hipótesis de factibilidad, marcada como riesgo prioritario en el pre-mortem).
- Pregunta de aprendizaje: ¿Podrá un bot reemplazar completamente a una persona para resolver dudas administrativas, o hay límites técnicos y de contexto que lo hacen solo parcialmente efectivo?
- Experimento mínimo: Chatbot funcional con Claude API, entrenado con FAQs fundamentadas en los reglamentos de la facultad, probado con estudiantes con dudas administrativas reales.
- Métrica: % de estudiantes que resuelven su duda con el bot sin necesidad de escribir después a secretaría.
- Criterio de éxito: ≥80% de los estudiantes resuelve sin reescribir a secretaría + el bot responde con precisión (sin errores graves) + los estudiantes reportan confianza en las respuestas.

## 2. Posición inicial en la curva de la verdad
- Evidencia disponible: Poca — evidencia cualitativa del propio equipo y conocidos, más un caso documentado de otra universidad. Sin datos institucionales ni prueba de que Claude API responda con precisión sobre el reglamento real.
- Incertidumbre pendiente: Si el bot puede responder con precisión suficiente (factibilidad) y si eso alcanza para que el estudiante no vuelva a escribir a secretaría.
- Inversión autorizada: Baja — interfaz web simple con Claude API, acotada a FAQs predefinidas. Quedan afuera por prematuros: integración con WhatsApp/Telegram, autenticación, base de datos persistente, panel para secretaría, derivación automática real, y cobertura completa del reglamento.

## 3. Instrumento construido por la IA
- Tipo de instrumento: Página web simple (HTML/CSS/JS autocontenido) que consume la Claude API (modelo Haiku) directamente desde el navegador, sin backend.
- Enlace o archivo: chatbot-secretaria-prototipo.html
- Qué incluye: interfaz de chat; base de conocimiento de 26 FAQs fundamentadas en 5 reglamentos reales de la facultad (Carreras de Grado, Ayudas Económicas, Requisitos de Título); instrucción explícita de no inventar y derivar a secretaría cuando la consulta esté fuera de esa base (horarios de comisión, cambios/detalles de plan de estudios por materia puntual, facturación/pagos).
- Qué quedó fuera: backend propio, persistencia de conversación, autenticación, panel de administración para que secretaría cargue contenido nuevo (propuesta del equipo para una futura iteración, no validada todavía).
- Ajuste durante la verificación: en la primera versión, una consulta sobre una materia puntual con plan de estudios ambiguo (caso Teología Moral) no derivaba a secretaría y daba una respuesta general con un "probablemente". Se corrigió el prompt para que ese tipo de consulta también derive. Cambio aplicado y confirmado por el equipo sin volver a testear exhaustivamente.

## 4. Ejecución
- Fecha y contexto: 12/09/2026. Prueba con las 4 integrantes del equipo (no estudiantes externos), usando la versión ya corregida del bot.
- Participantes: las 4 integrantes del equipo, como estudiantes de la facultad con dudas administrativas reales.
- Tarea realizada: interactuaron con el bot planteando en conjunto 7 consultas, combinando dudas reales de reglamento y consultas deliberadas fuera de alcance para poner a prueba los límites.
- Resultados obtenidos: 4 de 7 consultas resueltas directamente por el bot con el reglamento (asistencia, recuperatorios, días de falta, correlatividades/caso Teología Moral tras la corrección), sin necesidad de escribir después a secretaría. 3 de 7 consultas (comisión de una materia, materias por cuatrimestre x2) derivadas correctamente a secretaría por falta de esa información.
- Anomalías observadas: la consulta sobre Teología Moral no derivó correctamente en su primera versión (ver sección 3).

## 5. Evidencia
- A favor: de las consultas que el bot pudo responder (4 de 7), 100% correctas, sin necesidad de contactar después a secretaría. Identificó bien sus propios límites en 3 de 7 casos, derivando en vez de inventar.
- En contra: solo 57% (4 de 7) del total de consultas pudo resolverse íntegramente por el bot; el resto depende de datos (horarios, plan de estudios vigente) que nunca estuvieron en el alcance de este experimento.
- Interpretación del equipo: confían en que un futuro panel para que secretaría cargue información resolvería las consultas que hoy quedan fuera de alcance.
- Limitaciones: muestra de 4 integrantes del equipo (construyeron el bot y ya conocen el reglamento), no estudiantes externos independientes. No todas las consultas eran dudas reales personales. No se registró si reportaron "confianza" explícitamente.

## 6. Aprendizajes
- Qué aprendimos: el enfoque reglamento + Claude API responde con precisión sobre lo que tiene cargado, y reconoce y deriva correctamente lo que no cubre, sin inventar.
- Qué continúa siendo un supuesto: que estudiantes externos (no el equipo) confiarán en el bot y no volverán a escribir a secretaría; que un panel de carga de contenido para secretaría resolvería las dudas de horarios/plan de estudios sin necesitar conectarse al SIU.
- Cambios realizados o propuestos: se amplió el prompt para derivar consultas sobre materias puntuales/año de plan de estudios (aplicado). Propuesta a futuro: panel de carga de contenido para secretaría (no construido, no validado).

## 7. Estado de la evidencia y próxima iteración
- Estado: Inconclusa por ahora. La muestra (equipo, no estudiantes externos) no permite validar con confianza la hipótesis de comportamiento/confianza, aunque la de factibilidad muestra señales fuertes a favor dentro de lo que el bot cubre.
- Comparación con el criterio: 100% de precisión sobre consultas de reglamento (supera el ≥80%); 57% sobre el total de dudas administrativas reales (por debajo, por falta de datos cargados, no por imprecisión).
- Decisión de iteración: probar con estudiantes externos reales (los 5-8 originales de la caja 8) antes de clasificar como respaldada o no respaldada.
- Justificación: la autoevaluación del equipo introduce sesgo (ya conocen las respuestas esperadas) y no valida si un estudiante externo confiaría en el bot o preferiría escribir a secretaría igual.
- Próxima incertidumbre por reducir: comportamiento/confianza de estudiantes externos reales.

## 8. Nueva posición en la curva de la verdad
- Evidencia incorporada: el enfoque reglamento + Claude API es preciso y no inventa dentro de su base de conocimiento.
- Inversión que se justifica ahora: probar con estudiantes externos reales, sin agregar funcionalidades nuevas todavía.
- Qué todavía no se justifica construir: panel de carga de contenido para secretaría, ni integración con SIU — ambos son supuestos no validados aún.
