# Estado Técnico del Chatbot – Clase 5

**Última actualización:** 20/09/2026 15:55  
**Estado general:** 85% completado, en arreglos finales

---

## ✅ Completado

### 1. Diseño y decisiones
- [x] Contrato experimental definido
- [x] Métrica y criterio claros (≥80% sin derivación)
- [x] Tipo de experimento elegido (Chatbot)
- [x] Alcance mínimo definido
- [x] Participantes identificados (4 estudiantes)

### 2. Implementación
- [x] Chatbot HTML funcional (index.html)
- [x] Knowledge base con 26 FAQs sobre reglamento FCE
- [x] Interfaz con autenticación (nombre + API Key)
- [x] Integración inicial con API de Claude
- [x] Webhook a Google Sheets para logging automático
- [x] Sistema de marcado de derivaciones (keywords)
- [x] Despliegue en Vercel (https://chatbot-lovat-three-39.vercel.app/)

### 3. Documentación
- [x] `diseno-experimento.md` — Diseño completo listo para subir
- [x] `registro-experimento.md` — Estructura lista para llenar
- [x] Protocolo de ejecución documentado

---

## ⚠️ En reparación (CRÍTICO)

### CORS Error — Bloqueando ejecución
**Problema:** El chatbot no puede llamar la API de Anthropic directamente desde el navegador.

```
Error: Access to fetch at 'https://api.anthropic.com/v1/messages' 
from origin 'https://chatbot-lovat-three-39.vercel.app' 
has been blocked by CORS policy
```

**Causa:** Las políticas de navegador no permiten JavaScript del lado cliente llamar a APIs externas sin headers CORS.

**Solución:** Crear Vercel Function como intermediaria (servidor-a-servidor, sin CORS)
- [x] Código de solución preparado: `api/chat.js`
- [x] HTML actualizado para llamar `/api/chat` en lugar de API directa: `index-updated.html`
- [ ] **Implementación en GitHub** (próximo paso — Josefina)

**Archivos listos para implementar:**
- `api/chat.js` — Nueva función servidor
- `index-updated.html` — Actualización de chatbot

---

## 🔄 Próximos pasos (Orden de ejecución)

### HOY (20/09/2026)
- [ ] 1. Josefina crea `api/chat.js` en GitHub
- [ ] 2. Josefina reemplaza `index.html` con versión actualizada
- [ ] 3. Commit a `main`, esperar redeploy Vercel (1-2 min)
- [ ] 4. Subir a GitHub: `diseno-experimento.md` + `registro-experimento.md`

### MAÑANA (21/09/2026)
- [ ] 5. Piloto interno: equipo prueba 2-3 consultas
- [ ] 6. Verificar: funcionamiento técnico, logging correcto
- [ ] 7. Invitar a estudiantes por WhatsApp

### PRÓXIMOS 3-4 DÍAS (21-24/09/2026)
- [ ] 8. Ejecución con 4 estudiantes
- [ ] 9. Registro automático en Google Sheet
- [ ] 10. Análisis de resultados

---

## 📋 Archivos a subir a GitHub

```
/chatbot
├── index.html                  ← ACTUALIZAR (nuevo, sin CORS error)
├── api/
│   └── chat.js                ← CREAR (Vercel Function)
├── diseno-experimento.md       ← CREAR (documentación)
├── registro-experimento.md     ← CREAR (para llenar con resultados)
├── vercel.json                (ya existe)
└── .gitignore                 (ya existe)
```

### Contenido exacto a copiar-pegar:
- **`api/chat.js`** → [archivo separado enviado]
- **`index.html`** → [archivo separado enviado: index-updated.html]
- **`diseno-experimento.md`** → [contenido arriba en este doc]
- **`registro-experimento.md`** → [contenido arriba en este doc]

---

## 🧪 Testing & Verificación

### Piloto interno (1 día)
Checklist antes de invitar estudiantes:
- [ ] Acceder a https://chatbot-lovat-three-39.vercel.app/ sin errores
- [ ] Ingresar nombre + API Key correctamente
- [ ] Escribir consulta → recibir respuesta en <5 segundos
- [ ] Consulta aparece en Google Sheet automáticamente
- [ ] Bot identifica correctamente "derivada sí/no"
- [ ] Sin errores en consola de navegador
- [ ] Funciona en múltiples navegadores/dispositivos

### Con estudiantes (3-4 días)
- [ ] 4 estudiantes × 2-3 consultas = ~12 consultas
- [ ] ≥80% sin derivación = hipótesis respaldada
- [ ] <80% sin derivación = hipótesis no respaldada (iterar)

---

## 📊 Métricas de éxito

| Métrica | Objetivo | Estado |
|---------|----------|--------|
| Chatbot funcional | ✓ Sin CORS error | ⚠️ En reparación |
| Logging automático | ✓ Google Sheet recibe datos | ⏳ Pendiente test |
| Precisión respuestas | ✓ ≥80% sin derivación | ⏳ Pendiente ejecución |
| Confianza estudiantes | ✓ Reportan confianza | ⏳ Pendiente ejecución |
| Documentación | ✓ Diseño + Registro listos | ✅ Completado |

---

## 🚀 Deployment

**Plataforma:** Vercel  
**Rama:** main  
**URL:** https://chatbot-lovat-three-39.vercel.app/  
**Auto-deploy:** Activado (cambios en GitHub = redeploy automático en 1-2 min)

**Último cambio:** 20/09/2026 — Código preparado, en espera de implementación

---

## 📝 Notas técnicas

- API Key de Claude: Manejada por el cliente (se guarda en localStorage del navegador)
- No se guarda en servidor por seguridad
- Knowledge base: 26 FAQs fijas durante prueba (sin actualizaciones en vivo)
- Logging: Webhook a Google Apps Script → Google Sheet
- Identificación de derivaciones: Búsqueda de keywords ("secretaría", "no tengo información")

---

## 🔗 Enlaces útiles

- [Repositorio GitHub](https://github.com/JosefinaAramburu/chatbot)
- [Chatbot en Vercel](https://chatbot-lovat-three-39.vercel.app/)
- [Consola Anthropic](https://console.anthropic.com/)
- [Google Sheet de logging](#)

---

**Responsable implementación técnica:** Josefina  
**Responsable coordinación:** Valen + equipo  
**Próxima review:** 21/09/2026 (después de piloto interno)
