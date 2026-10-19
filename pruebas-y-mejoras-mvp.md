# Pruebas y mejoras del MVP — Asistente FCE Austral

## 1. Datos generales

- **Equipo:** Grupo 10 — Josefina Aramburu, Valen, Verónica y Paz
- **Fecha:** 17 al 19/10/2026
- **Usuario:** estudiantes de la Facultad de Ciencias Empresariales (FCE) de la Universidad Austral con una duda administrativa o de su carrera.
- **Problema:** hoy tienen que escribirle a secretaría y esperar, a veces días en época de inscripción.
- **Valor que buscamos:** que el estudiante reciba una respuesta concreta en el momento, sin que el bot lo mande a secretaría cuando tiene la información.
- **Acceso al MVP:** https://chatbot-lovat-three-39.vercel.app/ (se entra solo con un nombre; la API Key está en el servidor).
- **Código:** repositorio `JosefinaAramburu/chatbot`, desplegado en Vercel.
- **Versiones probadas:** ronda 1 con v2.2 (commit `4d7ab14`); ronda 2 con v3.1 (commit `0700335`).

### Recorrido hasta esta clase

1. **Problema:** estudiantes de la FCE con una duda administrativa (asistencia, recuperatorios, correlatividades) que hoy tienen que escribirle a secretaría y esperar. *(lean-product-canvas, mvp.md)*
2. **Hipótesis más riesgosa:** que Claude más el reglamento de la facultad alcance para responder con precisión (90%+) sin errores que hagan perder la confianza. *(lean-product-canvas)*
3. **Para probarla:** chatbot v1 con base de preguntas frecuentes y registro en Google Sheets. 3 participantes, 9 consultas, entre el 20 y el 27/9. Los 3 participantes eran integrantes del equipo: fue una prueba interna, sin participantes del segmento fuera del equipo. *(aprendizaje-y-mvp)*
4. **Observamos:** 0 de 9 consultas sin derivación (0 de 7 sin contar 2 saludos). En 4 el bot dio información parcial y después derivó; en 3 dijo que no tenía información. *(aprendizaje-y-mvp)*
5. **Decidimos:** arreglar la prueba, cambiando cómo responde el bot (v2). Después hicimos dos ajustes más a partir de pruebas internas (v2.1 y v2.2). *(mvp.md)*
6. **El MVP permite** escribir una duda y recibir una respuesta directa, con repreguntas y cálculo de faltas. **Falta comprobar** si a estudiantes de fuera del equipo se les resuelve la duda y si confían en la respuesta o igual consultan a secretaría. Eso es lo que prueba esta clase.

### Aclaraciones sobre la evidencia previa

- **La hipótesis y la métrica anterior no coincidían.** El canvas pone el riesgo en la precisión y la confianza, pero la v1 midió derivación. Consideramos que están relacionadas (si el bot deriva mucho, genera desconfianza), pero eso todavía es una hipótesis. En esta clase medimos las dos cosas por separado.
- **La base de conocimiento se recortó.** La v1 tenía unos 24 datos en 8 temas. La v2.2 tiene 9 datos en el Grupo A y 7 respuestas orientativas en el Grupo B (sin fuente oficial). Se sacaron requisitos de título, becas, horarios, planes de estudio y detalles de recuperatorios. `aprendizaje-y-mvp.md` dice "sin tocar la base", pero el historial del repositorio muestra que se modificó en los ajustes del 15 y 16/10.
- **La columna "¿Derivó a secretaría?" del Google Sheet no es confiable.** Marca "Sí" en las 28 filas registradas hasta el 16/10, incluso en respuestas que no mencionan secretaría. La columna "¿Escribió después a secretaría?" marca "No" en todas. Ninguna de las dos se usa como dato: la derivación se marca a mano leyendo cada respuesta.
- **El Sheet sí registra las conversaciones de la v2.2:** las últimas filas, del 16/10, muestran respuestas de esta versión.

## 2. Tarea

La tarea tiene dos partes. Solo la parte 1 cuenta para éxito y autonomía.

**Parte 1 (se mide):**
> "Cursás una materia de 30 clases y cada clase cuenta una sola falta. Ya faltaste 5. Usá el asistente para saber cuántas veces más podés faltar sin quedar libre."

- **Respuesta correcta:** 2. El máximo es el 25% de 30 = 7,5, redondeado hacia abajo = 7 faltas; 7 − 5 = 2.
- **Por qué esta tarea:** la asistencia está en el Grupo A de la base, que es lo más confiable que tiene el bot. Evitamos la doble falta porque su regla no está confirmada. Aclaramos "una sola falta por clase" porque el bot siempre lo pregunta, y no queríamos que la persona se trabe por un dato que no le dimos.

**Parte 2 (se observa):**
> "Ahora preguntale una duda real tuya de la facultad."

- Sirve para medir valor y para ver qué preguntan de verdad los estudiantes y qué le falta al bot.

**Definiciones**

- **Empieza:** la persona abre el link, antes de poner el nombre.
- **Completada (parte 1):** la persona responde que puede faltar 2 veces más.
- **Información:** el cálculo usa la regla del 75% cargada en el bot. Es real pero no está confirmada con el reglamento.
- **Cuenta como ayuda:** cualquier indicación del equipo sobre qué escribir, qué responderle al bot o cómo leer la respuesta. Como la prueba es a distancia, cualquier mensaje de la participante pidiendo orientación que el equipo responda cuenta como ayuda.
- **Termina:** cuando la persona responde, o cuando avisa que no pudo (abandono).

## 3. Métricas

Criterios exploratorios definidos antes de probar, para 5 participantes.

### Métricas principales

| Métrica | Cómo se mide | Fuente | Momento | Criterio | Qué haríamos con el resultado |
| --- | --- | --- | --- | --- | --- |
| Éxito | Personas que responden "2" / personas que intentan la parte 1 | Respuesta escrita de la participante + conversación en el Sheet | Al terminar la parte 1 | 4 de 5 | Si se cumple, el cálculo funciona y la mejora va por la parte 2. Si no, revisamos la conversación: si el bot calculó mal, se corrige la regla; si calculó bien pero la persona no llegó al "2", se mejora cómo presenta el resultado. |
| Autonomía | Personas que responden "2" sin ayuda / personas que intentan | Registro del equipo de cada pedido de ayuda (texto y momento) | Durante la parte 1 | 4 de 5 | Según dónde se necesitó ayuda: para entrar, se mejora la pantalla de inicio; sobre qué escribir, se mejora el mensaje de bienvenida; para entender la respuesta, se mejora cómo responde. |
| Valor | Personas que responden "sí" a "¿Se te resolvió tu duda?" / personas que hicieron la parte 2. "En parte" se registra aparte y no cuenta como sí. | Respuesta escrita de la participante | Al terminar la parte 2 | 3 de 5 | Se cruza con la derivación: si no se resolvió porque el tema no estaba en la base, se amplía la base (temas recortados, syllabus); si estaba y no sirvió, se mejora cómo responde. |

Además se registra la respuesta a "¿Harías lo que te dijo el bot sin consultar a secretaría?", como señal de confianza.

### Indicadores de apoyo (sin criterio, sirven para explicar los resultados)

| Indicador | Cómo se mide | Fuente | Momento | Qué informa |
| --- | --- | --- | --- | --- |
| Derivación | Cada consulta, sin contar saludos, se clasifica en: *respondió* / *respondió y sugirió confirmar* / *solo derivó* | Sheet, leído por el equipo | Al cerrar la ronda | Qué temas le faltan al bot |
| Repreguntas del usuario | Veces por conversación que la persona reformula, pide aclaración o insiste. No cuenta contestarle al bot lo que preguntó ni hacer una pregunta nueva sobre otro tema. | Sheet + respuestas de la participante | Al cerrar la ronda | Si las respuestas se entienden a la primera |

### Valor real: prueba posterior

El valor que buscamos es que el estudiante no tenga que consultar a secretaría después. Eso no se puede medir durante la prueba, así que en la ronda queda como **"no medido"** y se define una prueba posterior:

- **Con quién:** participantes que en la parte 2 respondieron "sí" o "en parte".
- **Cuándo:** una semana después de la prueba (24/10 para la ronda 1 y 26/10 para la ronda 2).
- **Cómo:** un mensaje: "¿Terminaste consultando esa duda en secretaría o con alguien más? ¿Hiciste lo que te dijo el bot?"
- **Qué se registra:** cuántas resolvieron su duda sin consultar a nadie más.

### Reglas de conteo

- Se cuenta el primer intento por persona y versión. Los reintentos se registran aparte.
- Los abandonos cuentan como "intentó, no completó".
- Lo que no se pudo medir se escribe "no medido".

## 4. Registro de participantes

### Cómo se hizo la ronda 1

- **Participantes:** 5 estudiantes de la FCE, fuera del equipo (pertenecen al segmento).
- **Modalidad:** a distancia, por mensaje. Cada participante recibió el link, la consigna y las preguntas finales, y entró al bot con el nombre U1 a U5 para no registrar datos personales.
- **Limitaciones:**
  - Al ser a distancia no observamos dónde dudaron ni cuánto tardaron. Lo reconstruimos con la conversación del Sheet y sus respuestas.
  - Son conocidas de una integrante del equipo: pueden haber respondido de forma favorable. Se les pidió que fueran sinceras y que lo evaluado era el bot.
  - Responden en un momento de prueba, no cuando tienen la duda en la vida real.

### Ronda 1 — versión v2.2

Pruebas realizadas entre el 17 y el 19/10/2026. Fuentes: respuestas escritas de cada participante y conversaciones registradas en el Google Sheet. En el Sheet, U2 figura como "Usuario 2" y U5 entró con su nombre de pila; en este documento se la identifica solo como U5.

| ID | ¿Pertenece al segmento? | Versión | ¿Intentó? | ¿Completó? (respondió "2") | ¿Sin ayuda? | Valor: ¿se resolvió su duda? | Dificultad y ayuda recibida |
| --- | --- | --- | --- | --- | --- | --- | --- |
| U1 | Sí (FCE) | v2.2 | Sí | Sí | Sí | En parte | Parte 1 sin dificultad: "lo resolvió de manera clara y directa, me mostró todos los cálculos". Parte 2: el bot no tenía la información y derivó. |
| U2 | Sí (FCE) | v2.2 | Sí | Sí | Sí | En parte | Parte 1 sin dificultad: "hace el cálculo directamente el chat". Parte 2: el bot no tenía la información y derivó. |
| U3 | Sí (FCE) | v2.2 | No | No medido | No medido | No medido | No participó: no respondió y no aparece en el Sheet. La ronda se cerró el 19/10 con 4 participantes. |
| U4 | Sí (FCE) | v2.2 | Sí | Sí | Sí | No | Parte 1 sin dificultad. Parte 2: el bot no tenía la información y derivó. |
| U5 | Sí (FCE) | v2.2 | Sí | Sí | Sí | No | Parte 1 sin dificultad. Parte 2: "no tenía la información de las carreras en específico". Hizo 3 consultas y las 3 derivaron. |

Ninguna participante pidió ayuda durante la prueba (confirmado por el equipo).

### Detalle de la parte 2 y de los indicadores

| ID | Duda que preguntó | Clasificación de la respuesta | Repreguntas del usuario | ¿Haría lo que dijo el bot sin consultar? | Comentario (qué fue confuso o esperaba distinto) |
| --- | --- | --- | --- | --- | --- |
| U1 | (1) Si se anotó a un final y no pudo ir, si puede presentarse en la fecha siguiente o tiene que esperar a la próxima mesa. (2) Si puede cursar una materia cuya correlativa no tiene el final aprobado. | (1) Solo derivó. (2) Solo derivó (citó que hay correlatividades obligatorias y preguntó carrera y plan, pero igual derivó). | 0 (la segunda es una pregunta nueva) | "Iría a secretaría a consultar lo que no me pudo responder." | "Fue fácil de usar y respondía de manera rápida y clara." |
| U2 | Si desaprueba un final, cuántas veces más puede rendirlo antes de recursar. | Solo derivó. | 0 | Para las faltas, sí; para la segunda duda, iría a secretaría. | "No hubo nada confuso, fue muy fácil de usar, te responde de manera directa y clara." |
| U3 | No medido | No medido | No medido | No medido | No medido |
| U4 | Si el descuento del 10% por hermano se renueva cada año o queda registrado desde el primer año. | Solo derivó ("no tengo información cargada sobre descuentos, becas ni beneficios económicos"). | 0 | "Me dijo que consultara a secretaría, así que sí lo haría." | "No." |
| U5 | (1) Cuántas materias de diferencia hay para hacer la doble titulación Marketing & Management + Negocios Digitales, y cuáles son. (2) Si hay un límite de materias por cuatrimestre. (3) Lo mismo, sin hacer la doble titulación. | (1), (2) y (3): solo derivó. | 1 (la consulta 3 aclara la 2, porque el bot respondió solo para doble titulación) | "Sí." | "Se entendió todo y me aclaró que había cierta información que no tenía y que entonces consulte en secretaría." |

**Clasificación de todas las consultas de la ronda (sin saludos): 11.**
- Parte 1 (4 consultas): 4 de 4 con el cálculo correcto. 2 respondieron sin derivar (U2, U5) y 2 respondieron y sugirieron confirmar en secretaría si alguna falta era justificada (U1, U4).
- Parte 2 (7 consultas): 7 de 7 solo derivaron. En ningún caso el bot inventó información: dijo con claridad que no la tenía.

**Temas de la parte 2 y si estaban en la base:**
- Instancias de final (U1, U2): en el Grupo B figura como "dato NO confirmado". Es el mismo tema que preguntaron 2 veces en las pruebas internas de la v1.
- Doble titulación y límite de materias (U5): en el Grupo B, "no hay una cantidad de materias por cuatrimestre confirmada". También lo preguntaron en las pruebas internas de la v1.
- Descuentos y becas (U4): no está en la base actual. La v1 tenía información general sobre becas, que se quitó.
- Correlatividad con final pendiente (U1): la base solo dice que hay correlatividades obligatorias.

**Limitación de la pregunta 4:** cuando el bot recomienda ir a secretaría, "hacer lo que dijo el bot" significa justamente consultar a secretaría. Por eso las respuestas de U4 y U5 no se pueden leer como confianza para no consultar. Para la ronda 2 conviene reformular la pregunta.

### Resumen ronda 1

| Métrica | Resultado | ¿Cumple el criterio? |
| --- | --- | --- |
| Éxito | 4 de 4 que intentaron (U3 no participó) | Sí (criterio: 4 de 5) |
| Autonomía | 4 de 4 que intentaron | Sí (criterio: 4 de 5) |
| Valor (en la prueba) | 0 de 4 "sí"; 2 "en parte" (U1, U2); 2 "no" (U4, U5) | No (criterio: 3 de 5) |
| Valor real (a la semana) | No medido | Pendiente |
| Apoyo: derivación | Parte 1: 0 de 4 solo derivaron. Parte 2: 7 de 7 solo derivaron. | — |
| Apoyo: repreguntas del usuario | 1 en 4 conversaciones (U5) | — |

Se consiguieron 4 participantes de los 5 previstos. Los resultados son exploratorios y no se generalizan a todos los estudiantes.

### Ronda 2 — versión v3.1

Pruebas del 19/10/2026 (por la tarde). Fuentes: respuestas escritas de cada participante y conversaciones del Google Sheet.

**Cambios respecto de la ronda 1:**
- Versión v3.1 en lugar de v2.2.
- Personas nuevas (U6 a U9), distintas de las de la ronda 1.
- La pregunta 4 se reformuló: "¿Necesitarías consultar a alguien más para resolver tu duda?". En la ronda 1 era "¿Harías lo que te dijo el bot sin consultar a secretaría?", que resultó ambigua.
- U9 respondió las preguntas finales por separado para cada duda de la parte 2 y no escribió su respuesta de la parte 1; su resultado de la parte 1 se toma de la conversación del Sheet.
- En el Sheet, la conversación de U6 quedó registrada con el nombre "U8"; se identificó por el contenido (doble titulación con Contador Público, plan viejo, ingreso 2025).

| ID | ¿Pertenece al segmento? | Versión | ¿Intentó? | ¿Completó? (respondió "2") | ¿Sin ayuda? | Valor: ¿se resolvió su duda? | Dificultad y ayuda recibida |
| --- | --- | --- | --- | --- | --- | --- | --- |
| U6 | Sí (FCE) | v3.1 | Sí | Sí | Sí | Sí | Parte 1 sin dificultad. Parte 2: "me explicó muy bien que según el reglamento se puede hacer doble titulación si los planes de estudio lo permiten". |
| U7 | Sí (FCE) | v3.1 | Sí | Sí | Sí | Sí | Parte 1 sin dificultad. Parte 2: "el chat me respondió bien". |
| U8 | Sí (FCE) | v3.1 | Sí | Sí | Sí | En parte | Parte 1 sin dificultad. Parte 2: el bot explicó la cursada reducida pero no tenía el dato de la cuota con una sola materia. |
| U9 | Sí (FCE) | v3.1 | Sí | Sí (según el Sheet; no lo escribió en su respuesta) | Sí | En parte (una duda sí, otra en parte) | Parte 1 sin dificultad. Parte 2: la duda de créditos se resolvió en parte ("no fue la respuesta de 10 créditos"); la del final, sí. |

Regla aplicada a U9: cuando una persona hizo dos dudas con resultados distintos, se registra "en parte" a nivel persona y se detalla cada consulta abajo.

| ID | Duda que preguntó | Clasificación de la respuesta | Repreguntas del usuario | ¿Necesitaría consultar a alguien más? | Comentario | ¿La respuesta tuvo datos que no están en la base? |
| --- | --- | --- | --- | --- | --- | --- |
| U6 | Qué plan de Contador Público le corresponde para la doble titulación, si estudia Administración (plan 2018) y entró en 2025. | Respondió y sugirió confirmar (Dirección de Estudios o Secretaría de Alumnos). | 0 | Sí: "iría porque me dijo que lo compruebe con Dirección de Estudios". | "Fue muy claro con las respuestas." | Sí. Afirmó que quien entró en 2025 "debería estar en el plan 2026" y que "la Facultad te asignará también el plan 2026 de Contador", y que tener el plan 2018 "es raro". Nada de eso está en la base. |
| U7 | Qué es lo primero que tiene que hacer para empezar la doble titulación con Contador Público, estudiando Administración. | Respondió y sugirió confirmar (Dirección de Estudios). | 0 | Sí: "tengo que hablar con director de estudios, pero el chat me respondió bien". | "No." | Sí. Dijo que lo primero es hablar con la Dirección de Estudios "para gestionar el trámite" y que ellos asesoran sobre materias comunes; el art. 30 no nombra ninguna oficina. Además afirmó "podés hacer doble titulación con Contador Público", cuando el art. 30 lo condiciona a que los planes lo permitan. |
| U8 | Si recursa una materia en último año y le queda solo esa, si paga la cuota normal. | Respondió y sugirió confirmar (Secretaría de Alumnos). | 0 | Sí: "Secretaría de Alumnos". | "Siento que para el 80% de las dudas la va a responder sin problema; preguntas más específicas como facturación requieren algo más personal." | Sí, menor. Dijo que la materia se recursa "en el próximo cuatrimestre"; la base no dice en qué cuatrimestre se dicta cada materia. Lo de cursada reducida (art. 37) es correcto. |
| U9 (1) | Cuántos créditos necesita para graduarse. | Respondió en parte (requisitos del art. 22 y créditos durante los dos primeros años) y derivó la cantidad a Secretaría de Alumnos. | 0 | Sí: "a Vida Universitaria". | "No." | No. La base no tiene la cantidad de créditos (los planes la expresan en horas). |
| U9 (2) | Qué nota tiene que sacar para poder rendir en el segundo llamado si desaprueba. | Respondió sin derivar (art. 45: con 3 puede; con 1 o 2 no). | 0 | No. | "No." | No. |

**Clasificación de las consultas de la parte 2: 5.**
- Solo derivó: 0 de 5 (en la ronda 1, 7 de 7).
- Respondió y sugirió confirmar: 4 de 5.
- Respondió sin derivar: 1 de 5.

**Precisión (observación nueva, vinculada con la hipótesis más riesgosa del canvas):**
- 3 de las 5 respuestas de la parte 2 incluyeron afirmaciones que no están en la base (U6, U7, U8).
- En 2 de esas 3 (U6 y U7), la persona dijo que se le resolvió la duda. Es decir, confiaron en información que el bot dedujo o inventó.
- En la parte 1, una respuesta (U7) agregó una frase incorrecta después del cálculo correcto: "si llegás al 75% de inasistencia, no podés aprobar" (debería ser más del 25%).

**Otras observaciones:**
- En la parte 1, el bot preguntó si la materia cuenta doble falta aunque U7 y U9 ya habían aclarado que cada clase cuenta una falta. Las dos tuvieron que contestar una pregunta de más.
- 2 de 4 participantes (U6 y U7) preguntaron por doble titulación, igual que U5 en la ronda 1. Es el tema que más se repite entre las dudas reales.

### Resumen ronda 2

| Métrica | Resultado | ¿Cumple el criterio? |
| --- | --- | --- |
| Éxito | 4 de 4 | Sí (criterio: 4 de 5) |
| Autonomía | 4 de 4 | Sí (criterio: 4 de 5) |
| Valor (en la prueba) | 2 de 4 "sí" (U6, U7); 2 "en parte" (U8, U9) | No (criterio: 3 de 5) |
| Valor por consulta | 3 de 5 consultas resueltas; 2 en parte | — |
| ¿Necesitaría consultar a alguien más? | 4 de 5 consultas sí | — |
| Apoyo: derivación | 0 de 5 solo derivaron | — |
| Apoyo: repreguntas del usuario | 0 en 4 conversaciones | — |
| Precisión | 3 de 5 respuestas de la parte 2 con datos que no están en la base | — |

## 5. Dificultad priorizada

- **Hecho (lo observado):** en la parte 1 (faltas), 4 de 4 llegaron a la respuesta correcta sin ayuda. En la parte 2 (dudas reales), 0 de 4 resolvieron su duda: 2 "en parte" y 2 "no". Las 7 consultas de la parte 2 terminaron derivadas a secretaría porque el bot no tenía la información. En ningún caso respondió con información incorrecta.
- **Posible causa (a comprobar):** falta de información en la base de conocimiento. Cuando el bot tiene el dato (asistencia), resuelve; cuando no lo tiene, deriva. Las dudas fueron sobre finales (U1, U2), doble titulación y límite de materias (U5), correlatividades (U1) y descuentos (U4).
- **Mejora propuesta:** ampliar la base de conocimiento con fuentes oficiales: el reglamento de la FCE (finales, regularidad, límite de materias) y los planes de carrera (materias y correlatividades). Solo se carga información que esté en esos documentos.
- **Fuera de esta mejora (pendiente):** syllabus de las materias (nadie lo pidió en esta ronda y requiere decenas de documentos) y becas y descuentos (solo si se consigue información oficial).
- **Por qué elegimos esta dificultad:**
  - *Cuánto bloquea:* es lo que impide el valor. 0 de 4 resolvieron su duda real.
  - *Cuántas veces apareció:* en 4 de 4 participantes y en 7 de 7 consultas de la parte 2. Los temas de finales y doble titulación ya habían aparecido en las pruebas internas de la v1.
  - *Esfuerzo:* bajo a medio. Agregar texto a la base no cambia cómo funciona el bot; el trabajo principal es conseguir y revisar los documentos.
  - *Decisión del equipo:* consideramos que la dificultad es la falta de información en general, no un tema puntual. Acotamos el alcance a dos documentos oficiales para poder terminarlo y volver a medirlo.
- **Responsable de conseguir los documentos:** Valen.
- **Pedido a la IA:**

> Nuestro usuario es un estudiante de la FCE de la Universidad Austral y busca resolver una duda administrativa en el momento, sin tener que ir a secretaría. Probamos la versión v2.2 con 4 estudiantes de la FCE fuera del equipo. Observamos que 4 de 4 resolvieron sin ayuda la tarea de faltas, pero 0 de 4 resolvieron su duda real: las 7 consultas terminaron derivadas porque el bot no tenía la información (finales, doble titulación, límite de materias, correlatividades, descuentos). Elegimos trabajar sobre la falta de información porque bloquea el valor y apareció en todas las participantes. Ayudanos a analizar posibles causas y proponé hasta tres cambios pequeños. Antes de modificar, discutamos las alternativas.

## 6. Cambio implementado y verificación técnica

- **Versión nueva:** v3 (archivo `api/chat.js`, preparado el 19/10/2026) y v3.1, su ajuste tras las pruebas internas. La ronda 2 se hace con la v3.1.
- **Punto de recuperación:** v2.2, commit `4d7ab14`. Para volver atrás alcanza con restaurar ese archivo.
- **Fuentes cargadas (conseguidas por Valen):**
  - Reglamento de Carreras de Grado de la FCE, Sede Pilar (versión 2023). Se cargaron los artículos sobre oficinas, regularidad, correlatividades, graduación, promedio, doble titulación, asistencia, inscripción, recuperatorios, finales, mesas especiales y revisión de exámenes, cada uno con su número de artículo.
  - Planes de estudio de las 5 carreras de la FCE (Negocios Digitales, Comercialización y Marketing Estratégico, Administración de Empresas, Contador Público y Economía Empresarial), cada una con su plan anterior y su plan 2026: materias por año, horas y correlativas.
- **Qué cambió en el bot:**
  - La base pasó a tener dos fuentes oficiales y una sección aparte de información sin fuente oficial.
  - El bot cita el artículo o el plan de donde sale cada dato.
  - Cuando deriva, nombra la oficina que indica el reglamento (por ejemplo, Secretaría de Alumnos para exámenes e inscripciones) en lugar de "secretaría académica". Según el art. 8, la Secretaría Académica se ocupa de las actividades de los profesores.
  - Reglas nuevas: cómo comparar planes en una doble titulación, cómo responder el promedio de una materia, qué hacer si el reglamento cubre solo parte del caso o da dos plazos distintos, y qué hacer si nombran una carrera que no existe en la base.
- **Qué se reemplazó de la base anterior:**
  - "Existe un recuperatorio por materia al final del cuatrimestre" → art. 43: hasta dos recuperatorios en el llamado a final del turno inmediato posterior, si la cátedra lo autoriza en el syllabus.
  - "Teología Moral es correlativa de Teología Dogmática" → correlativas según cada plan.
  - "Los cambios de comisión requieren autorización de la cátedra" → se quitó; el art. 34 dice que la Gerencia de Carreras asigna la comisión.
  - Promedio, instancias de final y doble titulación (antes orientativos) → ahora salen de los arts. 23, 30, 36, 41 y 45.
  - Faltas justificadas, plazo de certificados, campus cancelado y cambio de carrera → pasaron a "sin fuente oficial", porque el reglamento no los menciona.
- **Qué se conservó (funcionaba en la ronda 1):** el cálculo de faltas con redondeo hacia abajo, la pregunta por la doble falta y la cuenta prudente, el texto plano, las repreguntas de a una y la memoria de la conversación.
- **Criterio de aceptación:** ante las dudas reales de la ronda 1 (finales, doble titulación, correlativas), el bot responde con el dato del reglamento o del plan y cita la fuente, sin inventar lo que no está. La tarea de faltas sigue dando "2".
- **Verificación técnica realizada:**
  - El archivo no tiene errores de sintaxis.
  - Con la API simulada, una consulta normal devuelve respuesta (200) y la base completa viaja en el pedido.
  - Casos de error: sin API Key devuelve 500, mensaje vacío devuelve 400, un GET devuelve 405 y una caída de la API devuelve 502.
  - Las reglas y la base se marcan para caché, así que las consultas repetidas son más baratas y rápidas. Cada consulta envía unos 15.000 tokens de contexto.
- **Subida y prueba interna (19/10/2026, Josefina):**
  - v3 subida al repositorio (commit `15848af`) y desplegada en Vercel.
  - Josefina hizo 6 pruebas internas con el nombre PRUEBA (no cuentan como participantes): tarea de faltas, cuántas veces se rinde un final, final al que no se presentó, correlativas, comparación de planes para doble titulación y descuento por hermano.
  - Resultado de la v3 (según las conversaciones del Sheet, 19/10):
    - Faltas: correcto (2).
    - Cuántas veces se rinde un final: correcto en lo central (tres desaprobados), pero no dio el plazo de seis turnos y agregó reglas de notas que no se preguntaron.
    - Final al que no se presentó: falló. Le preguntó qué nota sacó y citó un inciso equivocado.
    - Correlativas: falló. Dijo que no se puede cursar y se contradijo (art. 18 dice que alcanza con la correlativa regularizada).
    - Comparación de planes: falló. Listó materias que sí figuran en los dos planes y dio un total "aproximado".
    - Descuento por hermano: dijo bien que no tenía el dato, pero derivó a la oficina de cobranzas atribuyéndole funciones que el reglamento no le da.
  - Resultado de la v3.1 (mismas 6 pruebas): faltas, final, ausente, correlativas y descuento respondieron según lo esperado. La comparación de planes mejoró en el formato (separa materias comunes y cuenta), pero sigue con errores: en una prueba incluyó como materias de Negocios Digitales 2026 dos materias que son de Comercialización (Estrategia de Producto y Marca, Introducción al Conocimiento del Consumidor), y en otra marcó como faltante Negocios Cloud, que figura en ambos planes 2026.
- **Ajuste v3.1 (commit `0700335`), a partir de esas pruebas:**
  - Correlativas: regla explícita para distinguir cursar (alcanza con la correlativa regularizada) de rendir el final (hace falta aprobada), con las excepciones de 3° y 4° año del art. 18.
  - Final al que no se presentó: no preguntar la nota, decir que queda "ausente" (art. 45), aclarar lo que el reglamento no dice y mencionar la baja hasta 48 horas hábiles antes.
  - Cuántas veces se rinde un final: dar siempre los tres desaprobados y los dos plazos (art. 45 inc. 8 y art. 36).
  - Comparación de planes: recorrer materia por materia, separar las que ya figuran por nombre, contar exactamente las faltantes y dejar aparte las optativas.
  - Citar solo artículos e incisos que estén escritos en la base, y no atribuirle a una oficina funciones que la base no le da.
  - Filtro en el código que saca los asteriscos de la respuesta antes de mostrarla.
  - Puntos de recuperación: v3 = `15848af`; v2.2 = `4d7ab14`.
- **Prueba con personas:** ronda 2 hecha con la v3.1 (ver sección 4).

## 7. Comparación antes / después

Misma tarea y mismas definiciones de métricas, con personas nuevas de la FCE en cada ronda.

| Métrica | Antes (ronda 1, v2.2) | Después (ronda 2, v3.1) | Qué aprendimos y qué limita la comparación |
| --- | --- | --- | --- |
| Éxito | 4 de 4 | 4 de 4 | El cálculo de faltas ya funcionaba y se mantuvo. No cambió porque no era lo que se mejoró. |
| Autonomía | 4 de 4 | 4 de 4 | Nadie necesitó ayuda en ninguna ronda. La prueba fue a distancia, así que solo sabemos de la ayuda que las participantes pidieron por mensaje. |
| Valor | 0 de 4 "sí" (2 en parte, 2 no) | 2 de 4 "sí" (2 en parte, 0 no) | Mejoró: nadie quedó con "no". Las dudas son distintas en cada ronda, así que no se compara la misma pregunta. |
| Derivación (apoyo) | 7 de 7 consultas solo derivaron | 0 de 5 solo derivaron | El bot pasó de "no tengo información" a responder con el reglamento y los planes. Es el cambio más claro y coincide con la mejora implementada. |
| Precisión (observación nueva) | No hubo errores: el bot no respondía | 3 de 5 respuestas con datos que no están en la base | Al responder más, aparecieron afirmaciones no respaldadas, y 2 personas las tomaron como válidas. Es justo el riesgo de la hipótesis del canvas. |

**Qué limita la comparación:**
- Son 4 personas por ronda, no las 5 previstas. Los resultados son exploratorios.
- Cada persona preguntó una duda distinta: la mejora puede deberse en parte a que en la ronda 2 las dudas cayeron en temas que el reglamento cubre.
- La pregunta 4 cambió entre rondas, así que no se compara.
- Las participantes son conocidas de una integrante del equipo y la prueba fue a distancia.
- Esta comparación no demuestra por sí sola que el cambio causó el resultado.

**En una frase:** medimos si estudiantes de la FCE resuelven su duda con el bot; en la ronda 1, 0 de 4 la resolvieron porque el bot no tenía la información; ampliamos la base con el reglamento y los planes; en la ronda 2, 2 de 4 la resolvieron y ninguna consulta quedó solo derivada, pero apareció un problema nuevo: 3 de 5 respuestas incluyeron datos que no están en la base.

## 8. Próximo paso

- **Próxima incertidumbre:** si el bot puede responder sin agregar datos que no están en su base. En la ronda 2, 3 de 5 respuestas lo hicieron, sobre todo al nombrar oficinas y al deducir qué plan le corresponde a alguien.
- **Acción más barata para resolverla:** armar una lista de 10 preguntas reales (las de las rondas 1 y 2), con la respuesta correcta según el reglamento y los planes, y probar el bot antes de cada cambio. Ajustar las reglas para que no nombre una oficina si la base no la asigna a ese trámite y no deduzca qué plan le corresponde a alguien. Se mide igual: cuántas de 10 respuestas tienen datos fuera de la base. Esta prueba es interna y no cuenta como participantes.
- **Responsable:** Josefina (tiene acceso al repositorio y a Vercel). Asignación provisoria, a confirmar por el equipo.
- **Momento:** semana del 26/10/2026, antes de una próxima ronda con personas.
- **Valor real (pendiente desde la sección 3):** mensaje a U1–U9 una semana después de su prueba: "¿Terminaste consultando esa duda en secretaría o con alguien más?". Responsable: Valen (contactó a las participantes). Asignación provisoria, a confirmar por el equipo. Fecha: 24/10/2026 (ronda 1) y 26/10/2026 (ronda 2).

### Pendientes ya identificados

- Confirmar con Secretaría de Alumnos cómo se aplica la doble falta. El art. 33 dice que la asistencia se computa por hora de clase, lo que podría significar que la cuenta prudente actual da de menos.
- Confirmar con Secretaría de Alumnos qué oficina gestiona la doble titulación y qué plan le corresponde a cada cohorte, que fueron los temas donde el bot dedujo de más.
- Que el bot no pregunte por la doble falta cuando el alumno ya aclaró que cada clase cuenta una falta.
- La comparación de planes sigue teniendo errores en las pruebas internas; conviene que el cálculo de materias faltantes lo haga el código y no el modelo.
- Verificar la información "sin fuente oficial" que quedó en la base (faltas justificadas, plazo de certificados, campus cancelado, cambio de carrera).
- Evaluar cargar los syllabus de las materias. Hoy el bot responde el promedio con el art. 45 y remite al syllabus.
- Cargar la cantidad de créditos de Vida Universitaria y Talleres (U9 preguntó y el bot no lo tenía).
- Arreglar el script del Google Sheet que marca todas las consultas como derivadas.
