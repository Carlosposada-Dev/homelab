# Prompt · arrancar un repo `homelab-<propósito>` nuevo

Úsalo justo después de crear el repo desde la plantilla:

```bash
gh repo create Carlosposada-Dev/homelab-<proposito> --template Carlosposada-Dev/homelab-template --public --clone --description "Lab N · <una línea>"
cd homelab-<proposito> && gh repo edit --add-topic homelab --add-topic devops
```

Abre Claude Code dentro del repo, rellena los campos entre `<>` y pega lo que sigue a la línea.

---

Soy Cloud DevOps Engineer y este repo es un lab de mi homelab personal. Acabo de crearlo desde la plantilla `homelab-template`, así que ya tiene la estructura estándar (`docs/`, `infra/`, `config/`, `k8s/`, `scripts/`, `.github/`, `pre-commit`). Quiero que actúes como mi ingeniero de plataforma y me ayudes a convertir la plantilla en el lab real, dejando todo documentado como si fuera un proyecto de trabajo.

## Contexto del homelab

- Hub con arquitectura, inventario de máquinas y convenciones: https://github.com/Carlosposada-Dev/homelab . Léelo primero, en especial `docs/conventions.md`, `docs/architecture.md` y `docs/inventory/`.
- Tres máquinas unidas por Tailscale: `minimac` (Mac mini M4, 16 GB, servidor siempre encendido con OrbStack/k3d), `aorus` (Ryzen 5 3600, 48 GB, Proxmox bajo demanda) y `dell` (i7 11ª gen, 32 GB, cliente móvil).
- Estándares: todo como código, Conventional Commits, PRs aunque trabaje solo, secretos con `sops` + `age`, `gitleaks` y `pre-commit` en cada commit, `trivy` para imágenes, nada del trabajo entra aquí.

## Este lab

- **Repo:** `homelab-<proposito>`
- **Lab N:** <número y nombre, por ejemplo "Lab 1 · GitOps">
- **Objetivo en una frase:** <qué quiero tener funcionando al final>
- **Máquina(s) donde corre:** <minimac / aorus / dell>
- **Herramientas que quiero usar:** <lista>
- **Lo que ya existe y debe reutilizarse:** <otros repos homelab-*, servicios ya desplegados, o "nada">
- **Restricciones:** <RAM/disco disponible, presupuesto en nube, tiempo, lo que no quiero tocar>
- **Qué debe poder hacer alguien que clone este repo:** <levantarlo con N comandos, verificar con X, apagarlo con Y>

## Lo que quiero que hagas

1. **Lee la plantilla** y propón qué carpetas se quedan, cuáles se borran y qué falta, según el objetivo. Pide confirmación antes de borrar.
2. **Diseña antes de escribir código**: diagrama Mermaid en `docs/architecture.md`, componentes, flujo de datos, puertos, qué corre dónde y por qué. Si hay una decisión con más de una opción razonable, escribe un ADR en `docs/adr/` con contexto, opciones, decisión y consecuencias, y pregúntame antes de darla por tomada.
3. **Plan por fases** con criterio de "listo" verificable en cada fase. Empieza siempre por lo que hace falta para que lo demás funcione (red, acceso, secretos, bootstrap).
4. **Ejecuta conmigo fase por fase.** Muestra cada comando antes de correrlo; pregúntame antes de cualquier acción destructiva, de pago o que requiera `sudo`. Commits pequeños con Conventional Commits; una rama `feat/<fase>` y PR por fase.
5. **Documenta mientras avanzas, no al final**: README que responda en orden qué es, dónde corre, cómo levantarlo, cómo verificar que funciona y cómo apagarlo; un runbook en `docs/runbooks/` por cada procedimiento repetible (levantar, apagar, respaldar, recuperar, actualizar).
6. **CI útil desde el primer PR**: `pre-commit` con `gitleaks`, lint del lenguaje principal (`tflint`, `ansible-lint`, `helm lint`, `yamllint` según aplique) y `trivy` si hay imágenes.
7. Al cerrar, entrega: checklist de verificación ejecutado, lista de qué quedó pendiente con issue creado para cada punto (`gh issue create`), y la línea para actualizar la tabla de repos del hub `homelab`.

Responde en español. Comandos exactos, rutas exactas, sin teoría de relleno. Si algo del contexto no cuadra con lo que ves en la máquina o en el hub, dímelo antes de seguir.
