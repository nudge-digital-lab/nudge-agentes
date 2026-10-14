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
| [`director-comercial`](.claude/agents/director-comercial.md) | Dirección: busca ventas: servicios nuevos para clientes actuales y cierre de leads. Lee todo: CRM de ventas (MCP `nudge-ventas`), panel (`nudge-panel`), Google Ads, Meta Ads, Gmail, agenda, Airtable y la web. Solo lee y propone. |
| [`onboarding`](.claude/agents/onboarding.md) | Dirección: da de alta a cada cliente nuevo (ficha y servicios en el panel, bienvenida, brief, accesos, "Tu proyecto") hasta el traspaso a desarrollo, y detecta altas a medias. Solo lee y propone. |
| [`director-desarrollo`](.claude/agents/director-desarrollo.md) | Dirección: la parte operativa. Inventario de proyectos y campañas, alertas (cobrado sin entregar, reclamos, vencimientos), bloqueos y plan de la semana. Solo lee y propone. |
| [`ops-assistant`](.claude/agents/ops-assistant.md) | Organiza tareas internas o genera checklists de procesos repetibles (lanzamiento, onboarding). |

## La dirección: cómo trabajan juntos

Los cuatro agentes de dirección cubren el recorrido completo de un cliente: **marketing** trae las consultas, el **comercial** las cierra, **onboarding** da de alta al cliente y **desarrollo** entrega y opera. Los cuatro leen todo (CRM de ventas, panel, Google Ads, Meta Ads, Gmail, agenda, Airtable y la web) y no escriben nada: proponen y Jorge aprueba en la sesión principal.

Se pasan el trabajo con informes en `~/Documents/nudge-direccion/` (`AAAA-MM-DD-<area>.md`). La sesión principal guarda cada informe después de que Jorge lo ve, y cada director lee el último de los otros antes de armar el suyo. Ronda semanal: marketing → comercial → onboarding → desarrollo.

## Uso

Copiar la carpeta `.claude/agents` a la raíz de un proyecto (o a `~/.claude/agents` para uso global) y los agentes quedan disponibles en Claude Code. Cada archivo `.md` define el agente vía frontmatter (`name`, `description`, `model`) y su prompt de sistema.
