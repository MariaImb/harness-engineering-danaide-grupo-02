# Constitución

Acuerdos de Mesa de Ayuda. Cambian poco y con acuerdo del equipo.

## Misión y audiencia

Mesa de Ayuda es una API para gestionar tickets de soporte con SLA y escalamiento.

La usan dos roles:

- **Agente.** Crea y consulta tickets (cliente, categoría, prioridad y descripción), los asigna, los responde, los escala de nivel (1, 2 y 3) y los cierra.
- **Operaciones.** Ve cómo viene el trabajo: tickets abiertos por nivel y cumplimiento de SLA.

El cliente es un dato del ticket. Quien llama a la API es un usuario con uno de esos dos roles. El producto es la API.

## Stack

- Python 3.12
- FastAPI
- PostgreSQL
- SQLAlchemy 2
- Migraciones con Alembic
- pytest
- Ruff
- Docker Compose para correr la API y la base

Los identificadores y el código van en inglés. Esta constitución, los specs y el lenguaje del dominio van en español.

## Calidad

Una fase se cierra cuando pytest pasa, Ruff pasa, y la API junto con PostgreSQL levantan con Docker Compose.

## Seguridad y datos

- Todos los datos del proyecto son sintéticos: personas, clientes y sistemas de ejemplo, nunca reales.
- Cada request corresponde a un usuario con rol `agente` u `operaciones`.
- El agente opera tickets. Operaciones consulta reportes.
- Los roles entran en la primera fase. La forma concreta de presentar la credencial se fija en el spec de esa fase.

## Forma de trabajo

- El orden de las fases está en `specs/backlog.md`. Se revisa entre fase y fase.
- Antes de escribir el código de una fase, existe su `specs/NNN-<tema>/spec.md`.
- Una rama por fase, con la clave de la historia en el nombre (por ejemplo `MDA-1-tickets`).
- El PR va al `main` del fork del grupo. Otro integrante lo revisa. El merge cierra la fase.
