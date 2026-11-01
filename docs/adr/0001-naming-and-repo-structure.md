# ADR 0001 · Convención de nombres y estructura de repos

- **Fecha:** 2026-11-01
- **Estado:** aceptada

## Contexto

El homelab va a crecer en varios repos a lo largo del tiempo (GitOps, Proxmox, CI móvil, IA, multi-cloud, dotfiles). En la cuenta de GitHub ya conviven repos de cursos, portafolio y clientes con nombres heterogéneos (`tf-arch-3tier-ecs`, `ccaf-s2-claude-code-workflow`, `python_fundamentals`, `poc-GitHub-actions-CI-CD`). Hace falta distinguir a simple vista qué pertenece al homelab y que todos los labs tengan la misma forma para no reinventar la estructura cada vez.

## Opciones

1. **Un monorepo `homelab`** con una carpeta por lab.
2. **Un repo por lab con prefijo `homelab-`**, más un repo hub que los indexa.
3. Una **organización de GitHub** dedicada al homelab.

## Decisión

Opción 2: repos independientes `homelab-<propósito>`, un hub `homelab` con docs e inventario, y una plantilla `homelab-template` (template repository de GitHub) de la que nacen todos.

## Consecuencias

- Cada lab tiene su propio CI, issues e historial; se puede mostrar uno solo en una entrevista sin ruido.
- El prefijo agrupa alfabéticamente y permite filtrar con `gh`. El topic `homelab` cubre el filtro en la web.
- La plantilla fija la estructura; cambios a la estructura se hacen en la plantilla y se propagan a mano a los repos existentes (coste aceptable mientras sean pocos).
- Se descarta el monorepo porque mezcla ciclos de vida muy distintos (Proxmox cambia poco; GitOps cambia a diario) y hace pesados los clones en el `dell`.
- Se descarta la organización porque añade administración sin beneficio mientras haya un solo colaborador; se puede migrar después conservando los nombres.
