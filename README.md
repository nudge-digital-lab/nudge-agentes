# Nudge Agentes

Subagentes personalizados de Claude Code para el trabajo diario de [Nudge](https://github.com/nudge-digital-lab), agencia digital. Cada uno cubre un área específica del proceso: código, diseño, SEO, contenido, propuestas, reportes y operaciones internas.

Ninguno tiene memoria entre sesiones — hay que pasarle el contexto y los datos reales (cliente, período, cifras, links) en cada invocación.

## Agentes disponibles

| Agente | Uso |
|---|---|
| [`web-code-reviewer`](.claude/agents/web-code-reviewer.md) | Revisa código de sitios WordPress (seguridad, performance, buenas prácticas) antes de subir a producción. |
| [`design-qa`](.claude/agents/design-qa.md) | QA visual de un sitio contra su mockup/brief: fidelidad, responsive, estados de componentes. |
| [`seo-auditor`](.claude/agents/seo-auditor.md) | Audita técnicamente un sitio dado su URL: stack, SEO técnico, keywords y competencia. |
| [`content-writer`](.claude/agents/content-writer.md) | Redacta copy de marketing: posts, blog, ads, newsletters. |
| [`proposal-writer`](.claude/agents/proposal-writer.md) | Arma propuestas y presupuestos para proyectos nuevos. |
| [`client-reporter`](.claude/agents/client-reporter.md) | Informes periódicos de resultados post-lanzamiento (tráfico, leads, conversiones). |
| [`ads-reporter`](.claude/agents/ads-reporter.md) | Informes de performance de campañas de Google Ads. |
| [`renewals-tracker`](.claude/agents/renewals-tracker.md) | Prioriza vencimientos: hosting, dominios, SSL, soporte, Ads. |
| [`ops-assistant`](.claude/agents/ops-assistant.md) | Organiza tareas internas o genera checklists de procesos repetibles (lanzamiento, onboarding). |

## Uso

Copiar la carpeta `.claude/agents` a la raíz de un proyecto (o a `~/.claude/agents` para uso global) y los agentes quedan disponibles en Claude Code. Cada archivo `.md` define el agente vía frontmatter (`name`, `description`, `model`) y su prompt de sistema.
