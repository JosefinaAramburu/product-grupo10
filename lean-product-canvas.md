# Lean Product Canvas — Solución de comunicación estudiantes-secretaría

> Este canvas contiene hipótesis. La evidencia surgirá de observar y experimentar.

## 1. Problema de negocio

Los estudiantes universitarios tienen dificultades para resolver consultas administrativas a tiempo porque secretaría tarda días en responder mails, especialmente en períodos de saturación como inscripción. Esto genera que reenvíen, pregunten a compañeros o vayan presencialmente, lo que a su vez sobrecarga a secretaría con consultas repetidas. Lo sabemos porque esto ocurrió a estudiantes del equipo y conocidos, y hay un caso documentado de otra universidad con demoras similares (48-72h en picos). **Supuestos pendientes de validar:** si el problema es igual en toda la facultad, con qué frecuencia ocurre, y si la causa es solo la demora o también respuestas incompletas.

## 2. Resultados de negocio

- **Reducir el tiempo promedio que tarda un estudiante en resolver una consulta administrativa**: desde [línea de base: pendiente de medir] hasta [objetivo: pendiente de definir tras validar].

- **Reducir el porcentaje de estudiantes que necesita reenviar o repreguntar la misma consulta para obtener una respuesta completa**: desde [pendiente de medir] hasta [pendiente de definir].

- **Mejorar la percepción de atención administrativa entre estudiantes**: métrica pendiente de definir (satisfacción, velocidad percibida, confianza).

## 3. Usuarios y clientes

**Usuario principal:** Estudiantes universitarios que envían consultas administrativas por mail.

**Usuario secundario (afectado):** Personal de secretaría que recibe y responde consultas.

**Decisor/Cliente:** Facultad (administración académica).

**Influenciador:** Delegados de estudiantes o representantes de curso (podrían recomendar a compañeros usar el chatbot).

## 4. Necesidades y resultados del usuario

**Para estudiantes:**
- Cuando tengo una duda administrativa, quiero acceso inmediato a respuestas completas, para resolver sin esperar ni repreguntar.

**Para secretaría (usuario secundario):**
- Cuando recibo muchas consultas, quiero reducir el tiempo dedicado a preguntas repetidas, para poder enfocarse en consultas que requieren análisis específico.

## 5. Ideas de solución

### Chatbot de asistencia a consultas administrativas

**Propuesta:**
Un asistente digital (chatbot) disponible 24/7 que responde preguntas frecuentes sobre reglamento, trámites y plazos. El estudiante chatea, el bot responde automáticamente; si no puede resolver, lo deriva a secretaría.

**Valor para el usuario:**
- Respuesta inmediata a preguntas rutinarias (no esperar 48-72h)
- Respuesta completa sin necesidad de repreguntar
- Disponible fuera del horario de secretaría

**Tecnología central:**
Chatbot basado en IA entrenado con reglamento y FAQs de la facultad.

**Datos necesarios:**
- Reglamento actual de la facultad
- Preguntas frecuentes respondidas por secretaría
- Listado de trámites, plazos y correlatividades

**Riesgo principal:**
El estudiante no confía en un bot para dudas normativas y prefiere escribir a una persona de secretaría, o el bot da respuestas incorrectas.

**Prototipo inicial:**
Chatbot automático codificado con Claude API que responde en tiempo real a estudiantes, usando 15-20 preguntas frecuentes preparadas de antemano basadas en reglamento.

**Dependencias:**
- Acceso a reglamento de la facultad
- Base de preguntas frecuentes de secretaría
- Acceso a Claude API
- Herramienta de chat (Telegram, WhatsApp con bot automático, o interfaz web)

**Estado:** Idea no validada.

## 6. Hipótesis principales

### Hipótesis de problema

Creemos que los estudiantes tienen dificultades reales para resolver dudas administrativas porque secretaría tarda 48-72h+ en responder, especialmente en períodos de alta demanda.

Lo sabremos si en el experimento los estudiantes escriben al bot con preguntas que ya probablemente habían pensado escribirle a secretaría (no preguntas aleatorias).

### Hipótesis de valor

Creemos que un chatbot que responde instantáneamente a preguntas frecuentes sobre reglamento ayudará a los estudiantes a resolver sus dudas sin esperar 48-72h.

Lo sabremos si en el experimento los estudiantes logran resolver su duda específica con la respuesta del bot sin necesidad de reenviar, preguntar a compañeros, o escribir a secretaría después.

### Hipótesis de comportamiento

Creemos que los estudiantes confiarán en un chatbot para resolver dudas normativas y lo usarán en lugar de escribir a secretaría.

Lo sabremos si en el experimento los estudiantes usan el bot en más de una ocasión durante el período de prueba, y no escriben a secretaría para la misma pregunta después.

### Hipótesis de factibilidad

Creemos que podemos entrenar un chatbot con suficiente precisión usando el reglamento y FAQs de la facultad, sin que dé respuestas incorrectas que pierdan confianza.

Lo sabremos si en el experimento, el bot responde correctamente al menos el 90% de las preguntas usando solo información del reglamento preparada de antemano. Si hay preguntas que no puede responder con certeza, las deriva correctamente a secretaría.

## 7. Lo más importante por aprender

¿Podrá un bot reemplazar completamente a una persona para resolver dudas administrativas, o hay límites técnicos y de contexto que lo hacen solo parcialmente efectivo?

## 8. Experimento mínimo

### Hipótesis que prueba

¿Podrá un bot reemplazar completamente a una persona para resolver dudas administrativas, o hay límites técnicos y de contexto que lo hacen solo parcialmente efectivo?

### Objetivo

Validar si estudiantes pueden resolver sus dudas administrativas usando un chatbot automático basado en Claude API, sin necesidad de escribir a secretaría después.

### Tipo de experimento

Chatbot automático codificado con Claude API, entrenado con reglamento y FAQs de la facultad.

### Herramienta

Claude API + Telegram o WhatsApp (integración con bot automático) o interfaz web simple.

### Participantes

5-8 estudiantes de la facultad que hayan tenido dudas administrativas en el último año.

### Duración

Tiempo necesario para: codificar el bot (1-2 semanas), recopilar datos del reglamento (1 semana), probar con estudiantes (2-3 semanas).

### Tarea

1. Preparar 15-20 preguntas frecuentes + respuestas correctas del reglamento.
2. Codificar un chatbot con Claude API que responda basado en ese conocimiento.
3. Invitar a 5-8 estudiantes a usar el bot para resolver una duda administrativa real.
4. Registrar si logran resolver o si después escriben a secretaría.

### Datos necesarios

- Reglamento actual de la facultad
- Preguntas frecuentes que secretaría ya respondió
- Listado de trámites, plazos, correlatividades
- Acceso a Claude API

### Métrica principal

Porcentaje de estudiantes que resuelven su duda con el bot sin escribir a secretaría después.

### Criterio de éxito

- Al menos el 80% de los estudiantes resuelve su duda con el bot sin necesidad de escribir a secretaría.
- El bot responde con precisión (no hay errores graves que requieran corrección).
- Los estudiantes reportan confianza en las respuestas.

### Criterio de fracaso

- Menos del 60% de los estudiantes resuelve su duda sin escribir a secretaría.
- El bot da respuestas incorrectas o incompletas.
- Los estudiantes pierden confianza después de una mala respuesta.

### Aprendizaje esperado

- Qué porcentaje de consultas reales el bot puede resolver automáticamente.
- Qué tipos de preguntas requieren intervención humana (límites del bot).
- Si la precisión es suficiente para mantener confianza en estudiantes.
- Qué mejoras necesita el bot antes de una versión en producción.

### Limitaciones

- 5-8 estudiantes es muestra pequeña; no generaliza.
- No valida si secretaría implementaría o resistiría la solución.
- Solo mide resolución de dudas textuales; no prueba UX final completa.
- Duración corta; no mide adopción sostenida.

---

## Pre-mortem: Riesgos principales

### Riesgo 1: Bot impreciso → pierde confianza (PRIORITARIO)

**Supuesto que podría fallar:** que Claude API + reglamento es suficiente para entrenar un bot que responda correctamente.

**Señal temprana:** en la prueba con 20 preguntas, el bot da respuestas ambiguas, incompletas o incorrectas.

**Acción preventiva:** probar exhaustivamente antes de invitar estudiantes. Si falla, ajustar prompts o agregar contexto.

### Riesgo 2: Secretaría no apoya o resiste

**Supuesto que podría fallar:** que la facultad querrá implementar un bot que "reduzca su trabajo".

**Señal temprana:** secretaría no facilita datos; pone objeciones legales o administrativas.

**Acción preventiva:** dialogar temprano con secretaría sobre la propuesta antes de prototipar.

---

## Cierre del equipo

**La solución digital que decidimos explorar es:**
Un chatbot automático disponible 24/7 basado en Claude API que responde preguntas frecuentes sobre reglamento, trámites y plazos de la facultad. El bot responde instantáneamente; si no puede resolver, deriva a secretaría.

**La evidencia más fuerte que la respalda es:**
Las 4 integrantes del equipo experimentaron demoras de días en respuestas de secretaría durante períodos de saturación (inscripción). Conocidos reportaron situaciones similares. Un caso documentado de otra universidad mostró demoras de 48-72h+ en picos. El patrón de "reenvío + consulta a compañeros" se repite consistentemente.

**El supuesto más riesgoso es:**
Que Claude API + el reglamento de la facultad sea suficiente para entrenar un bot que responda con precisión (90%+) sin errores que pierdan confianza. Si el bot es impreciso, los estudiantes no confiarán y no lo usarán.

**Lo más importante que necesitamos aprender es:**
¿Podrá un bot reemplazar completamente a una persona para resolver dudas administrativas, o hay límites técnicos y de contexto que lo hacen solo parcialmente efectivo?

**El experimento que realizaremos es:**
Codificar un chatbot con Claude API entrenado con 15-20 preguntas frecuentes + reglamento de la facultad. Probarlo con 5-8 estudiantes que hayan tenido dudas administrativas reales. Medir si resuelven su duda sin escribir a secretaría después. Criterio de éxito: al menos 80% de los estudiantes resuelve sin reescribir + el bot responde correctamente + estudiantes reportan confianza.

**Abandonaremos o cambiaremos la propuesta si:**
- El bot es impreciso (menos del 90% de respuestas correctas) en las primeras pruebas internas.
- Más del 40% de estudiantes sigue escribiendo a secretaría después de usar el bot.
- Los estudiantes pierden confianza después de una respuesta incorrecta.
- Secretaría se opone o no facilita acceso a datos/preguntas frecuentes.
