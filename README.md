# Maat — Skill contra el slop de IA para Claude Code

Audita el slop de IA en artefactos de negocio: informes estratégicos, memos de M&A, presentaciones de comité, pipelines RAG y librerías de prompts. Skill de Claude Code que detecta afirmaciones sin trazabilidad, autoridad falsa, incertidumbre perdida, contraanálisis ausente y sesgo de prompt en documentos generados o asistidos por IA.

> El problema no es que la IA alucine. El problema es que las organizaciones alucinan que están informadas.

## Por qué "Maat"

En la cosmología egipcia, Maat es la diosa de la verdad, el equilibrio y el orden cósmico — el principio que pesa el corazón del difunto contra una pluma. Más ligero que la pluma, pasas. Más pesado, no.

La premisa de esta skill: el slop de IA es lo que pasa cuando las organizaciones dejan de pesar las afirmaciones contra la evidencia y empiezan a confiar en la prosa fluida. Maat audita la diferencia entre *lo que parece verificado* y *lo que realmente lo está*.

## Qué audita

Cualquier artefacto donde se haya usado IA para producir, resumir o informar un output de negocio:

- Informes estratégicos, memos de M&A, tesis de inversión, presentaciones de comité
- Análisis de mercado, due diligence, inteligencia competitiva
- Pipelines RAG internos y bases de conocimiento curadas
- Librerías de prompts usadas para decisiones recurrentes
- Resúmenes de reuniones que alimentaron una decisión

## Los 10 principios Maat

1. **La IA no es la fuente.** Nunca cites a ChatGPT/Claude/Gemini como verdad de base.
2. **Toda afirmación estratégica necesita trazabilidad.** De dónde, quién, cuándo, definición, evidencia que la contradice, decisión que depende de ella.
3. **Separa borrador / análisis / verdad aprobada.** Tres estados documentales, nunca mezclados.
4. **Revisión experta = revisar verdad, no estilo.** Premisas, datos, omisiones — no comas.
5. **Gobierna los prompts, no solo los outputs.** Un prompt es una pregunta de investigación.
6. **RAG solo sobre conocimiento curado.** Versionado, fechado, con responsable, con marcado de obsolescencia.
7. **La incertidumbre debe sobrevivir al resumen.** Conocido vs. creído vs. desconocido.
8. **Las decisiones estratégicas exigen contraanálisis.** "Por qué esto puede estar equivocado" es obligatorio.
9. **Separa IA generativa de IA de decisión.** Riesgo distinto, controles distintos.
10. **Auditoría periódica de outputs en producción.** Tasa de error real, muestreada, no percibida.

## Instalación

```bash
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/maat
```

Después, en Claude Code: `/maat <ruta-archivo-o-texto-o-url>`

## Salida

La skill produce:

- **Veredicto ejecutivo** (SLOP_CRITICO / SLOP_MODERADO / RIESGO_BAJO / LIMPIO)
- **Auditoría por principio** (PASS/WARN/FAIL con evidencia literal)
- **Top 5 de afirmaciones peligrosas** en tabla
- **Contraanálisis** (autogenerado cuando falta)
- **Prompt inferido** — reconstrucción del prompt probable que generó el artefacto, con grado de confianza, sesgo arrastrado y versión neutralizada
- **Puntuación Maat 0–10** en un bloque `MAAT_REPORT` legible por máquina al final

### Puntuación

Cada principio puntúa PASS = 1.0 · WARN = 0.5 · FAIL = 0.0 · N/A se excluye. Los principios 2 (trazabilidad), 7 (incertidumbre) y 8 (contraanálisis) tienen peso doble. La puntuación se redondea a un decimal y se mapea a un veredicto:

| Puntuación | Veredicto |
|---|---|
| 0.0 – 2.9 | SLOP_CRITICO |
| 3.0 – 5.9 | SLOP_MODERADO |
| 6.0 – 7.9 | RIESGO_BAJO |
| 8.0 – 10.0 | LIMPIO |

Umbral de bloqueo recomendado: **7.0** para documentos que informan decisiones, **5.0** para borradores en revisión temprana. Los fallos duros en el principio 1 o en el principio 8 (cuando el artefacto es de grado decisión) fuerzan `bloqueante: true` independientemente de la puntuación.

## Autor

[@jlcases](https://github.com/jlcases) — basado en los 10 principios para un uso serio de IA en organizaciones.
