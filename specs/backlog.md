# Backlog

Fases en orden de implementación. Una por historia. El detalle va después en `specs/NNN-<tema>/spec.md`.

- [ ] **MDA-1.** Crear y consultar tickets.
  Listo cuando un agente puede crear un ticket (cliente, categoría, prioridad y descripción) y consultarlo.

- [ ] **MDA-2.** Asignar y responder tickets.
  Listo cuando un agente puede asignar un ticket y registrar una respuesta.

- [ ] **MDA-3.** Cerrar tickets.
  Listo cuando un agente puede cerrar un ticket.

- [ ] **MDA-4.** SLA por prioridad: vencimientos de primera respuesta y de resolución.
  Listo cuando cada prioridad tiene un vencimiento de primera respuesta y otro de resolución, calculados sobre el ticket.

- [ ] **MDA-5.** Escalar de nivel (1, 2 y 3).
  Listo cuando un agente puede escalar un ticket entre los niveles 1, 2 y 3.

- [ ] **MDA-6.** SLA vencido: marcar el ticket y escalarlo.
  Listo cuando un SLA vencido deja el ticket marcado y lo escala de nivel.

- [ ] **MDA-7.** Reportes para operaciones: abiertos por nivel y cumplimiento de SLA.
  Listo cuando operaciones puede ver los tickets abiertos por nivel y el cumplimiento de SLA.
