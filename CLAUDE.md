# nudge: directores y CRM

Jorge trabaja solo con agentes de IA y es el orquestador. La agencia se organiza en **directores** (subagentes en `~/.claude/agents/`), cada uno con su cancha. Lo que necesita autorización se lo escalan a Jorge.

## Los dos CRM

- **CRM de ventas:** nudge.com.ar/nocrm, MCP `nudge-ventas`. Contactos (prospectos), leads, presupuestos NDG-…, próxima acción, seguimientos, motivo de pérdida, anticipo y proyección del mes.
- **CRM de administración:** el panel, nudge.com.ar/panel, MCP `nudge-panel`. Contiene:
  - las fichas de clientes, con su **director a cargo**;
  - servicios y renovaciones, comprobantes y facturas de ARCA;
  - el cobro del proyecto (anticipo, entrega y saldo);
  - los accesos de terceros, sin contraseñas;
  - la ficha interna del proyecto y el formulario de alta;
  - Mi día y su pestaña Dirección.

Están conectados con una clave compartida:
- cada consulta de la web entra sola como lead;
- Mi día lee y mueve el pipeline;
- el anticipo registrado en ventas da de alta solo al cliente en el panel.

## Directores y traspasos

| Director | Cancha | Escribe en |
|---|---|---|
| `director-ventas` | Prospectos, leads, presupuestos, seguimiento, cierre y proyección. Termina con el presupuesto aceptado y el 50% pagado | CRM de ventas (y Solicitudes) |
| `director-onboarding` | Revisa el alta automática, el formulario de alta, los accesos y el alcance, hasta pasar el cliente a Proyectos | Ficha del cliente |
| `director-proyectos` | Ficha documentada de cada proyecto (alcance, entregables, decisiones, bitácora), trabados y atrasados, entrega | Ficha interna, «Tu proyecto» y cobro (entrega) |
| `director-finanzas` | Saldo después de la entrega, pagos, renovaciones, vencimientos y resumen de cobros | Cobro, comprobantes y renovaciones |
| `director-marketing` | Que entren consultas a nudge. Le pasa los leads a Ventas | Nada (solo lee) |

1. **Ventas → Onboarding:** presupuesto aceptado más anticipo registrado (`presupuesto_anticipo`). El pase al panel es automático.
2. **Onboarding → Proyectos:** alta completa, con el formulario, los accesos y la ficha interna armada (`director_cambiar`).
3. **Proyectos → Finanzas:** proyecto entregado (`cobro_entregar`), que dispara el cobro del saldo.
4. **Finanzas → cliente activo:** saldo pagado. Desde ahí solo se siguen las renovaciones.

Ningún cliente queda sin director a cargo. Si hay un caso dudoso, se le escala a Jorge.

## Reglas

- **Todo va al CRM.** Lo que generan los directores (y esta sesión) se vuelca en el CRM que corresponde: nota, bitácora, próxima acción o informe. Nada queda solo en una conversación.
- **Cada director escribe solo en su parte.** Lo de otro se le pasa con una nota y en el informe, no se hace.
- **Siempre con autorización de Jorge:**
  - mandar mails o mensajes a clientes;
  - descuentos o cambios de precio;
  - bajas de clientes o servicios, y despausar avisos automáticos;
  - facturas de ARCA y comprobantes que mandan mail;
  - cambios en los plugins de los CRM.

  Los directores no tienen herramientas para eso: lo suben como **acción** a Mi día → Dirección (`direccion_subir`). Jorge aprueba y sale por la cola de osTicket, firmado por Juan o Magali.
- **Cómo pedirle algo a un director:** «Director de ventas: …», o pidiendo la ronda de dirección. Al terminar, cada uno deja su informe en Dirección.
