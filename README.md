# Agentes de nudge

Subagentes personalizados de Claude Code para el trabajo diario de [nudge](https://github.com/nudge-digital-lab), agencia digital. Cada uno cubre un área específica del proceso: código, diseño, SEO, contenido, propuestas, reportes y operaciones internas.

Ninguno tiene memoria entre sesiones — hay que pasarle el contexto y los datos reales (cliente, período, cifras, links) en cada invocación.

## Agentes disponibles

| Agente | Uso |
|---|---|
| [`web-code-reviewer`](.claude/agents/web-code-reviewer.md) | Revisa código de sitios WordPress (seguridad, performance, buenas prácticas) antes de subir a producción. |
| [`design-qa`](.claude/agents/design-qa.md) | QA visual de un sitio contra su mockup/brief: fidelidad, responsive, estados de componentes. |
| [`seo-auditor`](.claude/agents/seo-auditor.md) | Audita técnicamente un sitio dado su URL: stack, SEO técnico, keywords y competencia. |
| [`content-writer`](.claude/agents/content-writer.md) | Redacta copy de marketing: posts, blog, ads, newsletters. |
| [`proposal-writer`](.claude/agents/proposal-writer.md) | Arma propuestas y presupuestos para proyectos nuevos. |
| [`client-reporter`](.claude/agents/client-reporter.md) | Informes periódicos de resultados: sitio y contenido (tráfico, leads, conversiones) o campañas pagas (gasto, CTR, CPA, conversiones). |
| [`renewals-tracker`](.claude/agents/renewals-tracker.md) | Prioriza vencimientos: hosting, dominios, SSL, soporte, Ads. |
| [`director-marketing`](.claude/agents/director-marketing.md) | Dirección: que entren consultas y leads a nudge con su marketing propio (pauta de nudge, web, newsletter, redes). Mide de dónde vienen y cuáles cierran. Solo lee y propone. |
| [`director-ventas`](.claude/agents/director-ventas.md) | Dirección: el closer. Prospectos, leads, presupuestos, seguimiento hasta el cierre o la pérdida (con motivo) y proyección del mes. Escribe en el CRM de ventas (`nudge-ventas`); su cancha termina con el presupuesto aceptado y el 50% pagado. |
| [`director-onboarding`](.claude/agents/director-onboarding.md) | Dirección: desde el pase automático hasta el alta completa (formulario de alta, accesos de terceros, alcance del proyecto). Escribe en la ficha del panel (`nudge-panel`). |
| [`director-proyectos`](.claude/agents/director-proyectos.md) | Dirección: ficha documentada de cada proyecto (alcance, entregables, decisiones, bitácora), trabados y atrasados, entrega. Escribe en la ficha interna del panel. |
| [`director-finanzas`](.claude/agents/director-finanzas.md) | Dirección: saldo después de la entrega, pagos, renovaciones, vencimientos y resumen de cobros. Escribe en el cobro y los comprobantes del panel. |
| [`ops-assistant`](.claude/agents/ops-assistant.md) | Organiza tareas internas o genera checklists de procesos repetibles (lanzamiento, onboarding). |

## La dirección: cómo trabajan juntos

La dirección cubre el recorrido completo de un cliente, con traspasos fijos:
- **Ventas → Onboarding:** presupuesto aceptado + 50% pagado. El pase al panel es automático.
- **Onboarding → Proyectos:** alta completa.
- **Proyectos → Finanzas:** proyecto entregado, que dispara el cobro del saldo.

**Marketing** trae las consultas y solo lee.

**Todo va al CRM**, y cada director escribe solo en su parte. Lo que necesita autorización lo suben como acción a Mi día → Dirección y Jorge lo aprueba:
- mensajes a clientes;
- precios y descuentos;
- bajas;
- facturas;
- cambios en los plugins.

Ningún director tiene herramientas para mandar mails. Ver [`CLAUDE.md`](CLAUDE.md) (se instala en `~/.claude/CLAUDE.md`).

## Uso

Copiar la carpeta `.claude/agents` a la raíz de un proyecto (o a `~/.claude/agents` para uso global) y los agentes quedan disponibles en Claude Code. Cada archivo `.md` define el agente vía frontmatter (`name`, `description`, `model`) y su prompt de sistema.
