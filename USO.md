# Guía de uso — Nudge Agentes

Documento completo sobre qué son estos agentes, cómo instalarlos y cómo invocar cada uno con ejemplos reales.

## 1. Qué son

Son subagentes de [Claude Code](https://docs.claude.com/claude-code): configuraciones independientes que definen un rol, un prompt de sistema y (opcionalmente) un modelo específico. Cuando Claude Code detecta que una tarea encaja con la descripción de un agente, puede delegarle el trabajo — o vos podés invocarlo explícitamente por nombre.

Cada agente:
- **No tiene memoria entre sesiones.** Arranca en blanco cada vez que se lo invoca.
- **No tiene acceso a fuentes de datos externas** (Google Ads, Analytics, un CMS, etc.) salvo que se lo des vos en el prompt.
- Vive en un archivo `.md` dentro de `.claude/agents/`, con frontmatter (`name`, `description`, `model`) y el prompt de sistema como cuerpo.

## 2. Instalación

**Opción A — Por proyecto** (recomendado si el agente aplica solo a un cliente/proyecto puntual):
```
cp -r nudge-agentes/.claude/agents/<agente>.md  <tu-proyecto>/.claude/agents/
```

**Opción B — Global** (disponible en cualquier proyecto que abras con Claude Code):
```
cp -r nudge-agentes/.claude/agents/*.md  ~/.claude/agents/
```

En Windows, `~` es `C:\Users\<tu-usuario>`. Después de copiar los archivos, reiniciá Claude Code (o abrí una sesión nueva) para que los detecte.

## 3. Cómo invocarlos

**Automático:** si le pedís a Claude Code algo que coincide con la `description` del agente (por ejemplo "revisá este código de WordPress"), puede invocarlo solo.

**Explícito (recomendado):** nombrá el agente en el pedido, así no hay ambigüedad:
> "Usá **web-code-reviewer** para revisar el `functions.php` de Perfumes Freeshop antes de subirlo a producción."

Como no tienen memoria, **siempre hay que darles el contexto completo en el mismo pedido**: cliente, objetivo, período, datos/cifras reales, links, archivos a revisar, etc. No asumen nada de conversaciones previas.

## 4. Guía por agente

### web-code-reviewer
Revisa código de sitios WordPress que Nudge construye o mantiene: temas, plugins custom, `functions.php`. Chequea seguridad (sanitización/escaping, nonces, capability checks), performance (queries, hooks, carga de assets) y buenas prácticas del ecosistema WordPress.

**Necesita:** ruta de los archivos/carpeta a revisar, tema base, page builder si aplica, plugins clave.

> "Usá web-code-reviewer para revisar el plugin custom que armamos para [cliente], carpeta `wp-content/plugins/cliente-custom/`, antes de subirlo a producción."

### design-qa
Compara un sitio (staging o producción) contra su mockup/brief de diseño: fidelidad visual (colores, tipografías, espaciados), responsive (mobile/tablet/desktop), estados de componentes (hover, focus, error, loading) y consistencia de marca.

**Necesita:** URL del sitio a revisar + link o referencia al mockup/brief.

> "Usá design-qa para comparar el staging de [cliente] (https://staging.cliente.com) contra el Figma (link) antes de lanzar."

### seo-auditor
Audita técnicamente un sitio dado su URL: identifica el stack/framework, corre una auditoría SEO técnica (velocidad, meta tags, estructura de headings/contenido) e investiga keywords/competidores del rubro.

**Necesita:** URL + contexto del negocio (rubro, mercado objetivo, competidores conocidos si los hay).

> "Usá seo-auditor para analizar https://clientex.com, es una clínica odontológica en Rosario, compará contra [competidor1] y [competidor2]."

### content-writer
Redacta copy de marketing: posts de redes (Instagram/LinkedIn), artículos de blog, copy de ads, contenido de email/newsletter.

**Necesita:** brief completo — negocio/cliente, objetivo, canal, extensión, ejemplos de referencia si hay.

> "Usá content-writer para armar 5 posts de Instagram sobre el lanzamiento de la web de [cliente], tono cercano, público joven."

### proposal-writer
Arma propuestas y presupuestos para proyectos nuevos (sitios web, paquetes de marketing, SEO, etc).

**Necesita:** negocio del cliente, qué necesita, alcance acordado, tarifas/paquetes a incluir (el agente no tiene tarifas memorizadas).

> "Usá proposal-writer para armar la propuesta del sitio WordPress de [cliente], paquete básico $X, incluye diseño + 5 secciones + hosting el primer año."

### client-reporter
Redacta informes periódicos (típicamente mensuales) de resultados para clientes post-lanzamiento: tráfico, leads, conversiones, ranking.

**Necesita:** cliente, período que cubre, datos/métricas reales de ese período (no los inventa).

> "Usá client-reporter para el informe mensual de julio de [cliente], estos son los números de Analytics: [datos]."

### ads-reporter
Redacta informes de performance de Google Ads: gasto, clics, CTR, CPA, conversiones, con insights y recomendaciones accionables.

**Necesita:** cliente, objetivos de campaña, período, datos reales exportados de Google Ads.

> "Usá ads-reporter para el informe de julio de la campaña de [cliente], estos son los datos exportados: [datos]."

### renewals-tracker
Organiza y prioriza vencimientos: hosting, dominios, SSL, soporte técnico, servicios de Google Ads. Calcula urgencia según las fechas que le pases.

**Necesita:** lista de vencimientos (cliente, servicio, fecha, costo si aplica).

> "Usá renewals-tracker, estos son los vencimientos del mes: [lista con cliente/servicio/fecha]."

### ops-assistant
Ayuda con operaciones internas de Nudge: (a) organizar/priorizar tareas pendientes entre proyectos, o (b) generar checklists de procesos repetibles (lanzamiento de sitio, onboarding de cliente nuevo).

**Necesita:** estado actual de tareas pendientes, o qué proceso necesitás.

> "Usá ops-assistant, necesito el checklist de lanzamiento de un sitio WordPress para [cliente]."

## 5. Buenas prácticas

- **Sé explícito con el nombre del agente** para evitar que Claude Code elija el equivocado.
- **Pasá siempre datos reales**, no placeholders — ninguno de estos agentes inventa cifras de performance, tarifas ni fechas.
- **Un agente por tarea.** Si necesitás varias cosas (ej. reporte + propuesta de renovación), invocalos por separado con su contexto propio.
- **Revisá el output antes de enviarlo al cliente.** Son borradores de alta calidad, no reemplazan una revisión humana final.

## 6. Agregar un agente nuevo

Crear un archivo `.md` en `.claude/agents/` con este formato:

```markdown
---
name: nombre-del-agente
description: Cuándo usarlo y qué hace, con 1-2 ejemplos de invocación.
model: sonnet
---

Prompt de sistema del agente: rol, criterios, formato de salida esperado.
```

Commitear y pushear al repo para que quede disponible para todo el equipo.
