# Spec 001 — Tickets

Fase [MDA-1 — Crear y consultar tickets](../backlog.md).

## Contexto

Un agente deja registrado un pedido de soporte y después lo recupera, por su identificador o en el listado de todos los tickets. El ticket de esta fase tiene cliente, categoría, prioridad y descripción, más el identificador que le asigna el sistema.

Quien llama se identifica con el encabezado `X-User-Id`. El rol sale del registro de ese usuario, no del pedido. Los usuarios son sintéticos y ya están cargados: esta fase no los da de alta. El agente crea y consulta. Operaciones, en esta fase, no opera tickets.

Los acuerdos de roles, datos sintéticos y forma de trabajo están en [constitution.md](../../constitution.md). Este spec no elige tecnologías.

## Historias

- [MDA-1 — Crear y consultar tickets](../backlog.md). Listo cuando un agente puede crear un ticket (cliente, categoría, prioridad y descripción) y consultarlo.
  - Como agente, quiero crear un ticket con cliente, categoría, prioridad y descripción para dejar registrado el pedido.
  - Como agente, quiero consultar un ticket por su identificador y ver el listado de todos para retomar el trabajo.

## Criterios

- **R1.** El sistema debe contar con exactamente dos usuarios sintéticos precargados: `agent-1` con rol `agente` y `ops-1` con rol `operaciones`. Cada uno tiene un identificador único y un único rol.

- **R2.** SI alguien intenta dar de alta un usuario o cambiar su rol, ENTONCES el sistema debe rechazar la operación. El conjunto de usuarios precargados debe permanecer igual.

- **R3.** CUANDO llega una operación de crear o consultar tickets, el sistema debe identificar al usuario por el encabezado `X-User-Id` y tomar su rol del registro precargado.

- **R4.** SI el encabezado `X-User-Id` está ausente o vacío, ENTONCES el sistema debe rechazar la operación por credencial ausente y no debe devolver datos de tickets.

- **R5.** SI el valor de `X-User-Id` no corresponde a un usuario precargado, ENTONCES el sistema debe rechazar la operación por usuario desconocido y no debe devolver datos de tickets.

- **R6.** SI el usuario identificado tiene rol `operaciones`, ENTONCES el sistema debe rechazar crear y consultar tickets por rol sin permiso y no debe devolver datos de tickets.

- **R7.** SI falla la credencial, el usuario o el rol, ENTONCES el sistema debe rechazar por esa causa y no debe juzgar los datos del ticket.

- **R8.** CUANDO un agente envía cliente, categoría, prioridad y descripción, y la prioridad es exactamente `baja`, `media`, `alta` o `urgente`, el sistema debe guardar un ticket nuevo y devolver solo su identificador, cliente, categoría, prioridad y descripción.

- **R9.** SI falta cliente, categoría, prioridad o descripción, o el valor es vacío o solo espacios, ENTONCES el sistema debe rechazar la creación por dato inválido y no debe guardar el ticket.

- **R10.** SI la prioridad no es exactamente `baja`, `media`, `alta` ni `urgente`, ENTONCES el sistema debe rechazar la creación por dato inválido y no debe guardar el ticket.

- **R11.** CUANDO un agente crea un ticket con los mismos cuatro datos que uno ya guardado, el sistema debe guardar otro ticket, con otro identificador.

- **R12.** CUANDO un agente consulta un identificador que existe, el sistema debe devolver solo el identificador, el cliente, la categoría, la prioridad y la descripción de ese ticket.

- **R13.** SI un agente consulta un identificador que no existe, ENTONCES el sistema debe rechazar la consulta por ticket inexistente.

- **R14.** CUANDO un agente pide el listado, el sistema debe devolver todos los tickets, cada uno con identificador, cliente, categoría, prioridad y descripción, sin filtrar.

- **R15.** CUANDO un agente pide el listado y no hay tickets, el sistema debe devolver un listado vacío.

- **R16.** SI el cliente supera 120 caracteres, la categoría supera 80 o la descripción supera 2000, contados sobre el texto tal como llega, ENTONCES el sistema debe rechazar la creación por dato inválido y no debe guardar el ticket.

- **R17.** CUANDO un agente pide el listado y hay tickets, el sistema debe devolverlos del más reciente al más antiguo, según el orden en que fueron creados.

- **R18.** SI la creación trae algún dato además de cliente, categoría, prioridad y descripción, ENTONCES el sistema debe rechazar la creación por dato inválido y no debe guardar el ticket. El encabezado `X-User-Id` no forma parte del ticket.

## Fuera de alcance

- Asignar y responder: [MDA-2](../backlog.md).
- Cerrar tickets: [MDA-3](../backlog.md).
- Vencimientos de SLA por prioridad: [MDA-4](../backlog.md).
- Niveles 1, 2 y 3: [MDA-5](../backlog.md).
- Marcar y escalar por SLA vencido: [MDA-6](../backlog.md).
- Reportes de operaciones: [MDA-7](../backlog.md).
- Estado del ticket, nivel, responsable, respuestas y fechas de SLA.
- Alta de usuarios y elección de tecnologías: los roles y el stack ya están en la constitución; este spec solo fija el comportamiento.
- Paginación del listado. Esta fase devuelve el listado completo. Si más adelante hiciera falta paginar, sería una fase nueva del backlog.

## Preguntas abiertas

No quedan preguntas abiertas en esta fase.
