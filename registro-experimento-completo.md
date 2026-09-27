# Registro del Experimento – Chatbot FCE Austral

**Estado:** Completado  
**Fecha inicio:** 20/09/2026  
**Fecha fin:** 27/09/2026

---

## Contrato experimental (referencia)

Ver `diseno-experimento.md` para detalles completos.

| Campo | Valor |
|-------|-------|
| Hipótesis | ≥80% de consultas resueltas sin derivación a secretaría |
| Métrica | % sin derivación (keyword ausente: "secretaría", "no tengo información") |
| Criterio éxito | ≥80% |
| Participantes | 4 estudiantes, diferentes carreras |
| Duración | 3-4 días o ≥12 consultas |

---

## Ejecución

### Piloto interno
- **Fecha:** 20/09/2026
- **Participantes:** Equipo Clase 5 (Josefina)
- **Estado:** ✅ Completado
- **Resultados:** Chatbot funcionó técnicamente, primeras 2 consultas registradas

### Ejecución con estudiantes
- **Fecha inicio:** 20/09/2026
- **Fecha fin:** 27/09/2026
- **Duración total:** 7 días
- **Total consultas realizadas:** 9
- **Estudiantes participantes:**
  - Josefina (Administración)
  - Valen (carrera no especificada)
  - Josefina Aramburu (carrera no especificada)
  - Veronica (carrera no especificada)

---

## Resultados por estudiante

### Estudiante 1: Josefina (Administración)

| # | Fecha | Consulta | Respuesta (resumen) | ¿Derivada? | Timestamp |
|---|-------|----------|---|---|---|
| 1 | 20/9 | hola | Bienvenido, presentación del bot | Sí | 4:11:27 |
| 2 | 20/9 | ¿Cuántas veces puedo rendir un final? | "No tengo información específica... contactate con secretaría" | Sí | 4:11:47 |

**Subtotal Josefina:** 2 consultas, 2 derivadas (100%)

---

### Estudiante 2: Valen

| # | Fecha | Consulta | Respuesta (resumen) | ¿Derivada? | Timestamp |
|---|-------|----------|---|---|---|
| 1 | 27/9 | hola | Bienvenido, presentación del bot | Sí | 3:47:57 |

**Subtotal Valen:** 1 consulta, 1 derivada (100%)

---

### Estudiante 3: Josefina Aramburu

| # | Fecha | Consulta | Respuesta (resumen) | ¿Derivada? | Timestamp |
|---|-------|----------|---|---|---|
| 1 | 27/9 | ¿Cuántas veces puedo rendir un final? | Respuesta parcial: recuperatorio existe, pero "contacta con secretaría" para número total de oportunidades | Sí | 3:48:02 |
| 2 | 27/9 | ¿Cuántas veces puedo faltar a una materia? | Respuesta técnica: 75% asistencia mínima = 25% faltas máximo, pero "contacta con secretaría" para cálculo específico | Sí | 3:49:04 |
| 3 | 27/9 | Si falté dos veces, ¿puedo volver a faltar? | Respuesta parcial con cálculo, pero "contacta con secretaría" para confirmación exacta | Sí | 3:49:43 |

**Subtotal Josefina Aramburu:** 3 consultas, 3 derivadas (100%)

---

### Estudiante 4: Veronica

| # | Fecha | Consulta | Respuesta (resumen) | ¿Derivada? | Timestamp |
|---|-------|----------|---|---|---|
| 1 | 27/9 | ¿Límite máximo de materias que puedo cursar? | "No tengo información... contactate con secretaría" | Sí | 3:49:43 |
| 2 | 27/9 | ¿Puedo empezar doble titulación en segundo año? | "No tengo información específica... contactate con secretaría" | Sí | 3:50:58 |
| 3 | 27/9 | ¿Debo cursar Teología este año si mi plan dice tercero? | Respuesta parcial: correlatividades existen, pero "contacta con secretaría" para confirmación | Sí | 3:52:11 |

**Subtotal Veronica:** 3 consultas, 3 derivadas (100%)

---

## Mediciones agregadas

- **Total consultas:** 9
- **Consultas resueltas (sin derivación):** 0
- **Consultas derivadas a secretaría:** 9
- **% sin derivación:** 0%
- **% con derivación:** 100%
- **¿Cumple criterio ≥80% sin derivación?** ❌ NO
- **Confianza reportada:** No fue medida formalmente (pendiente)

---

## Análisis de patrones

### Tipo de consultas
1. **Consultas sobre límites numéricos** (3): cuántas veces rendir, cuántas faltar, cuántas materias
   - **Resultado:** 100% derivadas — bot no tiene rangos exactos en knowledge base
   
2. **Consultas sobre trámites administrativos** (3): doble titulación, requisitos por carrera
   - **Resultado:** 100% derivadas — bot remite a secretaría
   
3. **Consultas sobre políticas genéricas** (2): recuperatorios, teología obligatoria
   - **Resultado:** 100% derivadas — bot da contexto pero no certeza

4. **Consultas de bienvenida** (2): "hola"
   - **Resultado:** 100% derivadas — presentación se cuenta como derivación

### Patrón de derivación
Todas las respuestas del bot incluyeron explícitamente la frase:
- "contactate con secretaría" (o variantes)
- "no tengo información específica"
- "por favor contactata con secretaría"

**Conclusión:** El bot fue diseñado para derivar cuando no estaba completamente seguro, lo que resultó en 100% de derivaciones.

---

## Observaciones y anomalías

### Errores técnicos
- ✅ Chatbot funcionó sin errores CORS después de la solución
- ✅ Logging automático en Google Sheet funcionó correctamente
- ✅ Autenticación (nombre + API Key) funcionó

### Respuestas inesperadas
- **Patrón observado:** Bot respondió con información contextual útil pero siempre terminaba derivando a secretaría
- **Ejemplo:** Pregunta sobre faltas → respuesta correcta (75% asistencia) → derivación a secretaría para el caso específico
- **Implicación:** La knowledge base de 26 FAQs no fue suficientemente exhaustiva para responder casos específicos

### Consultas fuera de knowledge base
- Todos los temas (faltas, finales, doble titulación, límite materias) estaban en los FAQs
- Sin embargo, nivel de detalle requerido por estudiantes > lo que knowledge base proporcionaba

---

## Conclusión

### Estado de la hipótesis
- ❌ **NO respaldada por esta prueba** (alcanzó 0% sin derivación, no ≥80%)

### Hallazgos clave

**Resultado definitivo:** 
- 9 consultas totales
- **0 consultas resueltas sin derivación** (0%)
- **9 consultas derivadas a secretaría** (100%)

**¿Por qué fracasó?**

1. **Knowledge base insuficiente:** 26 FAQs cubrían tópicos generales pero no casos específicos que estudiantes preguntaban
2. **Diseño conservador del bot:** Programado para derivar cuando no estaba 100% seguro (estrategia segura pero inútil para hipótesis)
3. **Mismatch entre documentación y necesidad:** Los FAQs eran respuestas genéricas; estudiantes necesitaban respuestas personalizadas según su situación

**Limitación de la prueba:**
- El bot estaba diseñado para "no fallar" (siempre derivar si hay duda)
- Esto hizo imposible probar la hipótesis: no hay forma de resolver consultas sin derivar si el bot está programado para no arriesgarse

---

## Análisis: ¿Fue un problema del instrumento o de la hipótesis?

### Problema del instrumento ✅
- **Causa identificable:** Knowledge base muy genérica
- **Evidencia:** El bot daba respuesta + derivación en 8 de 9 casos
- **Solución posible:** Expandir FAQs a 100+ casos específicos con reglas más granulares

### Problema de la hipótesis ❓
- **Incertidumbre:** ¿Los estudiantes necesitan respuestas automáticas o consulta con secretaría es inevitable?
- **Evidencia parcial:** Las 9 consultas fueron todas sobre tópicos que secretaría debe resolver (no son preguntas que un FAQ pueda responder completamente)

---

## Siguiente iteración (DECIDIDO: ITERAR)

### Decisión tomada: Opción A — Iterar el instrumento (plan acelerado)

**Acción:** Expandir knowledge base con Q&A basadas en evidencia real (3-5 días)

**Plan de ejecución:**

**Día 1:** Recopilar datos
- Usar las 9 consultas del experimento (ya disponibles)
- Obtener histórico de secretaría: tickets, emails, preguntas frecuentes
- Contactar a secretaría para validar respuestas oficiales

**Días 2-3:** Extraer Q&A reales
- De cada consulta/ticket → pregunta + respuesta exacta según reglamento
- Ejemplo: "¿Cuántas veces puedo rendir un final?" → respuesta basada en reglamento FCE
- 40-50 Q&A nuevas (basadas en datos, no inventadas)

**Día 4:** Actualizar bot
- Agregar Q&A nuevas a knowledge base JSON
- Cambiar lógica de bot: "si hay respuesta en KB → responder sin derivar"
- Probar con piloto interno (2-3 consultas)

**Día 5:** Segunda ronda con estudiantes
- Invitar nuevamente a los 4 estudiantes
- Medir % sin derivación (meta: ≥80%)

**Ventaja:** Construye sobre datos reales, no suposiciones. Más probable de éxito.

**Riesgo:** Aún podría resultar en >80% derivaciones si el problema es estructural (respuestas muy específicas por carrera/situación).

---

## Próximos pasos (Iteración 2)

1. **Recopilar histórico de secretaría** (responsable: equipo)
   - ¿Existen tickets o registro de preguntas?
   - ¿Contacto directo con secretaría para respuestas oficiales?

2. **Extraer 40-50 Q&A nuevas** (responsable: Claude + equipo)
   - Basadas en: 9 consultas experimentales + histórico secretaría

3. **Actualizar chatbot** (responsable: Josefina)
   - Agregar Q&A a `knowledge-base.json`
   - Cambiar regla de derivación en bot

4. **Piloto + segunda ronda** (responsable: equipo)
   - Validar técnicamente (1 día)
   - Invitar estudiantes nuevamente (3-4 días)

5. **Registrar resultados en `registro-experimento-v2.md`**

---

## Decisión rechazada: Opción B (Wizard of Oz)

Se consideró pero se eligió iterar primero porque:
- Más directo: el problema podría ser solo falta de conocimiento en la KB
- Menor costo: no requiere dedicación de secretaría
- Si falla, entonces pivotamos a Wizard of Oz

## Decisión rechazada: Opción C (Cerrar)

Demanda es real (9 consultas), así que vale intentar una iteración más.

---

## Historial de iteraciones

**Iteración 1 (Clase 5):** Chatbot HTML + Knowledge base de 26 FAQs
- Hipótesis: ≥80% resueltas sin derivación
- Resultado: 0% sin derivación ❌
- Causa: Knowledge base insuficiente + diseño conservador

---

## Logs técnicos (Google Sheet)

Todos los 9 registros llegaron correctamente a Google Sheet con timestamp, nombre estudiante, consulta, respuesta, marcado de derivación.

No se detectaron errores de logging.

---

**Última actualización:** 27/09/2026 — Experimento completado, análisis finalizado, listo para decisión del equipo
