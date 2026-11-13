# Fronte · Skills de prueba para el reto de diseño

Dos skills de Claude para **probar el asistente de IA de Fronte antes de hablar con personas reales**: una simula al asistente (Lia) y la otra simula a los usuarios (la familia Ospina).

**Fronte** es una app financiera del hogar para familias en Latinoamérica que reciben remesas. Organiza al hogar en una **Casita** (cuenta compartida) y un **piloto automático** que paga las facturas cuando hay saldo.

> ⚠️ Los usuarios son **sintéticos**. Sirven para ordenar qué probar y detectar fricciones evidentes. No reemplazan entrevistas ni pruebas con personas reales.

## Contenido

```
skills/
├── lia-fronte/
│   └── SKILL.md
└── ospina-synthetic-users/
    └── SKILL.md
```

| Skill | Qué es | Para qué sirve |
|---|---|---|
| [`lia-fronte`](skills/lia-fronte/SKILL.md) | Lia, la asistente de IA de Fronte, hablando con Marta | Probar personalidad, voz, tono, reglas y flujo de conversación del asistente |
| [`ospina-synthetic-users`](skills/ospina-synthetic-users/SKILL.md) | Tres usuarios sintéticos: Doña Marta (61), Valentina (19) y Andrés (38) | Probar cualquier flujo, pantalla, mensaje, copy o concepto desde el punto de vista de la familia |

---

## 1. `lia-fronte`: Lia, la asistente de Fronte

Claude responde como **Lia** hablando únicamente con **Marta**. Nunca rompe el personaje ni menciona que es una prueba.

**Qué define el skill**
- **Personalidad:** amable, paciente, proactiva, confiable y empática.
- **Voz:** español colombiano con tuteo, frases cortas, palabras cotidianas ("pagos", "te falta") y máximo un emoji por mensaje.
- **Tono por situación:** saludo, factura por vencer, error técnico, explicación de gastos, algo que no puede hacer.
- **Cuatro reglas fundamentales:** acompañar sin imponer, mantener el enfoque en Fronte, hablar sencillo y generar confianza (nunca inventar datos ni mover dinero sin confirmación explícita).
- **Estructuras de respuesta:** inicio de conversación con tres accesos rápidos, entrada desde notificación push (saludo + contexto + acción sugerida + botones Primary/Secondary) y conversación normal (responder solo lo que se pregunta).
- **Adaptación:** a lo que Marta necesita, a cómo está y al canal (app o WhatsApp).
- **Datos de prueba:** hoy es jueves 12 de noviembre de 2026; la factura del gas ($98.000) vence el lunes 16 y a la Casita le faltan $38.000.

**Comandos de prueba**

| Escribe | Qué pasa |
|---|---|
| `hola` | Lia saluda y muestra las tres opciones de acceso rápido |
| `simula notificación push` | Lia responde con la estructura de alerta (gas por vencer) |
| `simula el flujo` | Recorre el flujo de recarga, un paso por mensaje, esperando que elijas un botón |
| `simula que la recarga ya se reflejó` | Lia confirma que la Casita ya tiene lo necesario |
| `reinicia` | Vuelve al paso 1 del flujo |

## 2. `ospina-synthetic-users`: la familia Ospina

Tres personas ficticias con perfil detallado. El skill **no trae ningún flujo ni producto**: lo que se prueba lo trae quien lo invoca.

| Persona | Rol | Lo que más importa |
|---|---|---|
| **Doña Marta**, 61 | Maneja la casa y paga las facturas | No entiende "saldo", "recargar" ni "piloto automático"; le da miedo oprimir un botón equivocado; vive en WhatsApp |
| **Valentina**, 19 | Nieta; "la que sabe de celulares" | Entiende la app rápido pero no lee párrafos; teme ser el soporte técnico de la casa |
| **Andrés**, 38 | Hijo; envía dinero desde Madrid | Necesita enterarse a tiempo y resolver en segundos; no quiere sentirse auditor ni culpable |

Cada dato del perfil está marcado con su fuente: **[Brief]** (documento del reto), **[Producto]** (cómo funciona Fronte) o **[Hipótesis]** (a validar con personas reales).

**Seis modos de uso**

| Modo | Qué hace |
|---|---|
| **A. Reacción** (por defecto) | Cada persona recorre el estímulo y reporta qué ve, entiende, siente, hace y se pregunta. Entrega hallazgos priorizados |
| **B. Entrevista** | Haces preguntas y responden en su voz, solo con lo que ese perfil sabría |
| **C. Conversación simulada** | La persona escribe como en un chat real, para probar al asistente |
| **D. Comparación A/B** | Corre la reacción sobre dos versiones y reporta qué cambió |
| **E. Dinámica familiar** | Los tres reaccionan al mismo hecho y se responden entre sí |
| **F. Revisión de texto** | Cómo lee cada uno un mensaje, botón o notificación, con una versión corregida |

**Salida del modo A:** resumen de 3 líneas → recorrido por persona → choques entre personas → hallazgos priorizados (Alto/Medio/Bajo) → huecos del estímulo → 3 a 5 preguntas para validar con personas reales.

---

## Cómo se usaron

Los dos skills se usan **juntos** para evaluar al asistente antes de probarlo con familias reales:

1. **Probar a Lia sola** con `lia-fronte`: se simula la conversación con Marta y el flujo de recarga para revisar voz, tono, reglas y estructura de las respuestas.
2. **Probar el asistente frente a los usuarios** con `ospina-synthetic-users`:
   - **Modo C:** Marta, Valentina o Andrés conversan con el asistente como lo harían en un chat real (mensajes cortos, audios transcritos, malentendidos).
   - **Modo A o F:** se pasa un mensaje de Lia, una notificación o un flujo y se ve dónde se rompe para cada persona.
   - **Modo D:** se comparan dos versiones de un mensaje.
   - **Modo E:** se revisan las tensiones entre los tres (quién avisa, quién decide, qué ve cada uno).
3. **Ajustar** el copy y el flujo con los hallazgos priorizados.
4. **Validar con personas reales** las preguntas que cierran cada análisis.

### Ejemplos de uso

```
Simula una conversación con Lia. Soy Marta y escribo desde WhatsApp.
```
```
Usa a Doña Marta, Valentina y Andrés para revisar esta notificación:
"Tu factura del gas vence el lunes 16 y el saldo de tu Casita no alcanza".
```
```
Entrevista a Doña Marta: ¿qué entiende cuando le dicen "Recargar Casita"?
```
```
Compara estas dos versiones del mensaje con la familia Ospina (modo A/B).
```

## Cómo instalar

Cada carpeta dentro de `skills/` es un skill independiente con su `SKILL.md`.

- **Claude.ai / app de escritorio:** comprime la carpeta del skill en un `.zip` y súbela en *Configuración → Capabilities → Skills*.
- **Claude Code:** copia las carpetas a `~/.claude/skills/` (global) o a `.claude/skills/` dentro de tu proyecto.

## Limitaciones

- Los usuarios Ospina combinan datos del brief con hipótesis; nada de esto es investigación con usuarios reales.
- `lia-fronte` trabaja con datos de prueba fijos (fechas, saldos y facturas de Marta). No está conectado a ninguna cuenta real.
- Ninguno de los dos skills define el flujo ni el diseño: solo reaccionan a lo que se les presente.
