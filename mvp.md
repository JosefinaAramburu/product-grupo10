# Nuestro primer MVP

- **Usuario y situación:** estudiantes de la Facultad de Ciencias Empresariales de la Universidad Austral que tienen una duda administrativa o de su carrera (asistencia, recuperatorios, correlatividades) y hoy tendrían que escribirle a secretaría y esperar.
- **Valor y acción central:** que el estudiante reciba una respuesta concreta a su duda en el momento, sin que el bot lo mande a secretaría cuando tiene la información. Acción central: escribir una duda y recibir una respuesta directa.
- **Acceso o forma de ejecución:** https://chatbot-lovat-three-39.vercel.app/ — se entra solo con el nombre, sin API Key (la clave está en el servidor).
- **Recorrido:** inicio (ingresa su nombre) → acción (escribe su duda) → resultado (respuesta con lo que está cargado, o una pregunta para conocer su caso, o aviso de que no hay información).
- **Funciona / manual o simulado / fuera de alcance:**
  - *Funciona:* chat con IA, el bot recuerda la conversación, hace repreguntas sobre el caso del alumno, calcula faltas (25% del total de clases, redondeado hacia abajo; en materias de doble falta usa una cuenta prudente y avisa que no está confirmada) y avisa cuando no tiene información.
  - *Manual o simulado:* la base de conocimiento está cargada a mano. El Grupo A viene de la versión 1 del bot; el Grupo B son respuestas orientativas **sin fuente oficial confirmada** y el bot las presenta como tales. Los datos del alumno (cantidad de clases, faltas) los aporta el propio alumno en la conversación.
  - *Sin verificar en esta versión:* el registro automático de consultas en Google Sheets.
  - *Fuera de alcance:* conexión a sistemas de la facultad, login institucional, envío de mails a secretaría, paneles de métricas.
- **Evidencia disponible y duda pendiente:** en la prueba anterior (versión 1) 0 de 9 consultas se resolvieron sin derivar. Esta versión cambia cómo responde el bot, pero todavía no se probó con participantes. Duda pendiente: si el estudiante confía en la respuesta del bot para decidir, o igual la confirma con secretaría.
- **Qué medimos:** personas que intentan y completan la consulta; si a la persona se le resolvió la duda (preguntándoselo al final); % de consultas sin derivación sin contar saludos. Limitación: la marca de "derivada" del registro es automática (busca la palabra "secretaría") y puede marcar como derivada una respuesta que sí resolvió la duda.

## Prueba e iteración

- **Quién probó (rol) y tarea:** una integrante del equipo (prueba entre pares, conocía el bot, no cuenta como validación con usuarios). Tarea: preguntar cuántas veces se puede faltar a una materia y responder lo que el bot repregunte (30 clases, 3 faltas).
- **Qué ocurrió y cómo lo sabemos:** el bot saludó sin derivar, repreguntó, recordó la respuesta y calculó. Pero afirmó cosas que no están en su base: que las faltas justificadas no cuentan contra la asistencia, que el máximo eran "7 o 8" faltas (con 30 clases el máximo es 7), y nombró un área ("Bienestar Estudiantil") que no está cargada. Evidencia: transcripción de la conversación.
- **Devolución concreta que dimos a la IA:** "Preguntamos cuántas faltas se permiten con 30 clases. Esperábamos que usara solo lo cargado y calculara 7. El bot dijo '7 o 8', afirmó que las faltas justificadas no cuentan y nombró un área que no está en la base."
- **Cambio realizado y resultado de la nueva prueba:** se ajustaron las reglas del bot (usar solo lo que está en la base, no nombrar áreas externas, redondear faltas hacia abajo, no decir "confirmado"). Nueva prueba con 28 clases: respondió "28 × 0,25 = 7 faltas máximo", dijo "según la información que tenemos cargada" y no afirmó nada sobre las faltas justificadas.
- **Prueba entre pares con otra persona (Valen, integrante del equipo; no es validación con usuarios):**
  - *Tarea:* preguntarle al bot cómo queda el promedio de una materia, si cuenta solo el final o se promedia con la nota de cursada.
  - *Qué ocurrió:* el bot respondió que depende de cada cátedra, dijo que tiene cargado que existe un recuperatorio pero que no aclara cómo se integra la nota, y recomendó consultar a la cátedra o a secretaría académica. Evidencia: captura de la conversación y respuestas de Valen.
  - *Resultado según Valen:* "No se resolvió mi duda". Dijo que la respuesta era esperable, porque este tipo de dato suele estar en el syllabus, y que el bot le contestó que no podía responder porque depende de cada cátedra.
  - *Lo que propone Valen:* agregar al bot el syllabus de cada materia que se dicta.
  - *Obstáculos que observamos:* (1) la respuesta muestra asteriscos (`**cada cátedra**`) porque la página no interpreta el formato; (2) el bot afirmó "no hay una regla única en toda la FCE", algo que no está en su base (la base solo dice que depende de la cátedra); (3) no aclaró que el dato sobre promedio era orientativo.
  - *Lectura del equipo (Josefina):* la derivación a la cátedra fue correcta, pero el bot no mencionó el syllabus, que es el primer lugar donde mirar.
- **Segundo ajuste, a partir de lo observado con Valen y de nuestras propias pruebas:**
  - *Cambios en las reglas del bot:* texto plano sin asteriscos; no agregar generalizaciones que su base no dice; preguntar siempre si la materia cuenta doble falta antes de calcular; en doble falta, indicar también a cuántas clases completas equivale el máximo de faltas.
  - *Hallazgo en la prueba (Josefina, Teología, 15 clases, doble falta):* el bot usó una cuenta distinta a la de una prueba anterior (14 clases): antes calculó el 25% sobre las faltas posibles (14 × 2 = 28 → 7 faltas → 3 clases) y esta vez sobre las clases (25% de 15 → 3 faltas → 1 clase). Dos resultados distintos para el mismo tipo de pregunta. Nuestra base no confirma cuál es la regla correcta.
  - *Decisión del equipo (Josefina):* usar siempre la cuenta más baja, por prudencia, y que el bot avise que no está confirmada. No es una regla oficial de la facultad.
  - *Nueva prueba:* 15 clases, una falta por clase → 3 faltas, 3 clases (con la cuenta mostrada y sin asteriscos). 15 clases, doble falta → 3 faltas, 1 clase completa, "estimación más prudente", y aviso de que la base no confirma cómo se aplica y de confirmar en secretaría. Resultado consistente con la regla elegida.
  - *Sin repetir todavía:* la pregunta del promedio de una materia (la de Valen) y la prueba con 14 clases en doble falta.
- **Prueba con alguien del segmento fuera del equipo:** pendiente (Clase 8).
- **Próximo ajuste (a decidir por el equipo):** (a) confirmar con secretaría o con el reglamento cómo se aplica la doble falta, para reemplazar la cuenta prudente por la regla real; (b) evaluar si se puede cargar el syllabus de las materias, que es lo que pidió Valen; (c) volver a probar la pregunta del promedio. Después, probar el bot con personas ajenas al equipo sin explicarles cómo usarlo.
