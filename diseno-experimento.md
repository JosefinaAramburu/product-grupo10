# Diseño del Experimento – Chatbot FCE Austral

## Contexto y evidencia de partida

En la Clase 4 validamos que estudiantes de la FCE Austral tienen dudas frecuentes sobre asistencia, recuperatorios, correlatividades y trámites administrativos. Actualmente contactan a secretaría para resolver estas consultas, lo que consume recursos.

## Hipótesis principal

Si ofrecemos un chatbot que responde automáticamente dudas administrativas, **≥80% de las consultas se resolverán sin necesidad de derivar a secretaría**, y los estudiantes reportarán confianza en las respuestas.

## Pregunta de aprendizaje

**¿Los estudiantes usarán un chatbot para resolver dudas administrativas en lugar de contactar secretaría?**

## Incertidumbre a resolver

1. ¿El bot responde con precisión suficiente a las dudas administrativas reales?
2. ¿Los estudiantes encuentran el chatbot útil y confiable antes de escribir a secretaría?

## Tipo de experimento elegido

**Chatbot funcional HTML + API Claude + Logging automático**

### Especificaciones
- **Plataforma:** Vercel (despliegue en la nube)
- **Interfaz:** HTML/CSS/JavaScript
- **Backend:** API de Claude (Anthropic) vía Vercel Function
- **Base de conocimiento:** 26 FAQs manuales sobre reglamento FCE
- **Registro:** Google Sheets automático (webhook)
- **Duración:** 3-4 días
- **Participantes:** 4 estudiantes de diferentes carreras

### Por qué esta opción fue elegida

| Criterio | Chatbot ✓ | Landing | FAQ |
|----------|-----------|---------|-----|
| Funcional (respuesta real) | ✓ Sí | ✗ No | ✗ No |
| Barato | ✓ $0 | ✓ $0 | ✓ $0 |
| Rápido | ✓ 1-2 días | ✗ 3+ días | ✓ Horas |
| Medible | ✓ Cada consulta | ~ Parcial | ✗ No |
| Descartable | ✓ Sí | ✓ Sí | ✓ Sí |

**Decisión tomada:** Opción A (Chatbot) — produce evidencia suficiente con menor inversión

## Contrato experimental

| Campo | Especificación |
|-------|---|
| **Hipótesis** | Si ofrecemos un chatbot que responde automáticamente dudas administrativas, ≥80% de consultas se resolverán sin necesidad de derivar a secretaría, y estudiantes reportarán confianza. |
| **Métrica principal** | % de consultas resueltas sin derivación (ausencia de palabras clave: "secretaría", "no tengo información") |
| **Métrica secundaria** | Confianza reportada por estudiantes (pregunta posterior: "¿Confías en el bot?") |
| **Participantes** | 4 estudiantes de FCE Austral de diferentes carreras: Administración, Contabilidad, Marketing, Economía (amigas del equipo) |
| **Acción observable** | 1) Acceso al link 2) Ingreso de nombre + API Key 3) 2-3 consultas genuinas 4) Registro automático en Google Sheet |
| **Resultado observable** | Cada consulta registrada con: estudiante, pregunta, respuesta, marcado derivada/no derivada |
| **Criterio de éxito** | ≥80% de consultas resueltas sin derivación (keyword ausente) |
| **Duración** | 3-4 días (máximo, o después de ≥3 consultas por estudiante) |
| **Punto de parada** | Cuando se alcance ≥12 consultas totales o 4 días hayan pasado |
| **Limitación conocida** | No mide si el estudiante *hubiera* contactado secretaría sin el bot; solo si el bot satisface cuando es consultado |

## Alcance mínimo

### Imprescindible (sin esto no se puede medir)
- ✓ Chatbot HTML funcional, interactivo
- ✓ Autenticación simple (nombre + API Key) para trazabilidad
- ✓ Knowledge base con 26 FAQs sobre reglamento FCE
- ✓ Integración con API Claude en tiempo real
- ✓ Logging automático a Google Sheet
- ✓ Marcado automático de derivaciones (búsqueda de keywords)

### Simulado (aceptable)
- ✓ Diseño visual simple (gradiente morado + botones básicos)
- ✓ Sesión local sin persistencia entre reinicios

### Fuera de alcance
- ✗ Correcciones de FAQs en vivo durante prueba
- ✗ Múltiples idiomas
- ✗ Login con Google
- ✗ Historial permanente
- ✗ Entrenamiento de IA específico

## Partes reales vs simuladas

| Componente | Tipo | Descripción |
|------------|------|---|
| Consultas de estudiantes | **Real** | Preguntas genuinas de estudiantes reales |
| Respuesta del bot | **Real** | Generada por API de Claude (Anthropic) |
| Knowledge base | **Semi-real** | 26 FAQs curadas manualmente, no IA entrenada |
| Identidad estudiante | **Real** | Nombre ingresado manualmente |
| Logging | **Real** | Google Sheet auténtica, registros permanentes |
| Marcado derivada | **Automatizado** | Análisis de keywords en respuesta |

## Protocolo de ejecución

### Fase 1: Piloto interno (1 día)
1. Equipo accede al chatbot
2. Realiza 2-3 consultas de prueba
3. Verifica: funcionamiento técnico, logging correcto, identificación de derivaciones

### Fase 2: Ejecución con estudiantes (3-4 días)
1. Mensaje WhatsApp a 4 estudiantes con link del chatbot + API Key
2. Cada estudiante abre de forma independiente
3. Ingresa su nombre
4. Realiza 2-3 consultas genuinas (dudas administrativas reales que tenga)
5. **No se le indica qué preguntar** (libertad para consultar lo que quiera)
6. Respuestas se registran automáticamente en Google Sheet
7. Se espera a que complete ≥3 consultas o pasen 4 días

### Fase 3: Registro y análisis (1 día)
1. Recopilar resultados de Google Sheet
2. Calcular % sin derivación
3. Comparar con criterio (≥80%)
4. Registrar en `registro-experimento.md`

## Decisiones humanas ya tomadas

✓ **Elegida opción A:** Chatbot funcional vs Landing vs FAQ  
✓ **Métrica:** % consultas sin derivación (no solo "resueltas")  
✓ **Criterio:** ≥80% (no 100%, reconoce que algunas dudas complejas deben ir a secretaría)  
✓ **Duración:** 3-4 días (suficiente para ~12 consultas totales)  
✓ **Participantes:** 4 estudiantes de distinta carrera (representatividad mínima)  
✓ **Knowledge base:** 26 FAQs fijas durante la prueba (sin correcciones en vivo)  

## Siguiente paso

**Fase 1 (Piloto interno):** El equipo realiza 2-3 consultas de prueba para verificar:
- ✓ Funcionamiento técnico sin errores
- ✓ Logging correcto en Google Sheet
- ✓ Identificación correcta de derivaciones
- ✓ Que el API Key funcione

Una vez validado, procede a invitar a los 4 estudiantes.

---

**Fecha de diseño:** 20/09/2026  
**Estado:** Listo para ejecutar piloto
