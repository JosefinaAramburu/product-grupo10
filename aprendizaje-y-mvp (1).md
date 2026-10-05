# Aprendizaje y MVP — Chatbot FCE Austral

## 1. Qué probamos

- Queríamos comprobar: si un chatbot que responde dudas administrativas logra que los estudiantes las resuelvan sin derivar a secretaría.
- Criterio de éxito (original): ≥80% de las consultas sin derivación.
- Construimos: un chatbot web con la API de Claude, 26 FAQs del reglamento FCE y registro automático en Google Sheets.
- Participaron 3 estudiantes (Josefina, Valen y Verónica), entre el 20 y el 27/9, con 9 consultas en total.

## 2. Resultado

| Qué pasó | Cómo lo sabemos |
|---|---|
| Las 9 respuestas del bot incluyeron "contactate con secretaría" o "no tengo información": 0 de 9 sin derivación. | Google Sheet, marcado automático por palabras clave |
| 2 de las 9 consultas fueron un "hola" (no una duda administrativa). Sin ellas serían 0 de 7. | Google Sheet |
| En 4 consultas el bot dio información parcial útil y después derivó. En 3 dijo directamente que no tenía información. | Google Sheet, lectura de las respuestas |

- Resultado frente al criterio: no se alcanzó (0% contra ≥80%).
- Algo que salió distinto de lo esperado: el bot funcionó técnicamente sin errores, pero derivó siempre, incluso cuando tenía parte de la respuesta.

## 3. Aprendizaje

- Aprendimos que: el bot derivó a secretaría en las 9 consultas (0% sin derivación), incluso en 4 casos donde tenía parte de la respuesta, y creemos que esto se debe a que está armado para no arriesgarse cuando no tiene certeza.
- Todavía no sabemos si: el problema es la falta de información del bot o cómo está estructurado.

## 4. Decisión

- Elegimos: Arreglar la prueba.
- Porque: el bot derivó siempre y no pudimos probar si los estudiantes resuelven sus dudas con él.
- Próximo paso: cambiar cómo responde el bot (que conteste con lo que sabe y avise cuando no está seguro), sin tocar la base de conocimiento todavía, y repetir la prueba sin contar los saludos.

## 5. Punto de partida del MVP

- Usuario: estudiantes de la Facultad de Ciencias Empresariales de la Universidad Austral.
- Situación: tienen una duda administrativa o de su carrera (asistencia, recuperatorios, correlatividades) y hoy tendrían que escribirle a secretaría y esperar.
- Valor que queremos entregar: que el estudiante reciba una respuesta concreta a su duda en el momento, sin que el bot lo mande a secretaría cuando tiene la información.
- Una sola cosa que el MVP debe permitir hacer: escribir una duda y recibir una respuesta directa.
- Qué vamos a medir cuando lo use una persona: a cuántas personas se les resolvió la duda (preguntándoselo al final) y el % de consultas sin derivación, sin contar los saludos.
