# homelab

Hub del homelab de [Carlos Posada](https://github.com/Carlosposada-Dev): arquitectura, inventario de máquinas, convenciones y roadmap de labs. Aquí no vive código de ningún lab; cada lab tiene su propio repo `homelab-<propósito>` y este repo los indexa.

> Objetivo: practicar en casa lo que hago como Cloud DevOps Engineer (AWS, Azure, Kubernetes, Terraform, CI/CD, Flutter) y que el resultado sirva de portafolio.

## Máquinas

| Hostname | Equipo | Rol |
|---|---|---|
| `minimac` | Mac mini M4 · 16 GB · 256 GB + 1 TB externo | Servidor siempre encendido y estación de trabajo. Único equipo que compila iOS. |
| `aorus` | AORUS Elite AX V2 · Ryzen 5 3600 · 48 GB · 2.5 TB | Laboratorio pesado bajo demanda (Proxmox). Se enciende con Wake-on-LAN. |
| `dell` | Dell · i7 11ª gen · 32 GB · 1 TB | Cliente móvil y nodo extra. Compila Android. |

Las tres se conectan por **Tailscale**. Detalle por máquina en [`docs/inventory/`](docs/inventory/). Diagrama y flujos en [`docs/architecture.md`](docs/architecture.md).

## Repos del homelab

Todos siguen la convención `homelab-<propósito>` y nacen desde [`homelab-template`](https://github.com/Carlosposada-Dev/homelab-template). Ver [`docs/conventions.md`](docs/conventions.md).

| Repo | Propósito | Máquina principal | Estado |
|---|---|---|---|
| [homelab](https://github.com/Carlosposada-Dev/homelab) | Hub: docs, inventario, convenciones, prompts | — | activo |
| [homelab-template](https://github.com/Carlosposada-Dev/homelab-template) | Plantilla de repo para cada lab | — | activo |
| homelab-dotfiles | Dotfiles compartidos con chezmoi (zsh, Starship, Ghostty, git) | todas | planeado |
| homelab-gitops | Lab 1 · k3d + ArgoCD + Prometheus/Grafana/Loki + Traefik + runner self-hosted | `minimac` | planeado |
| homelab-proxmox | Lab 2 · Proxmox VE, clúster k8s de 3 VMs con Terraform + Ansible, NAS, WoL | `aorus` | planeado |
| homelab-mobile-ci | Lab 3 · Pipeline Flutter iOS + Android con GitHub Actions y Fastlane | `minimac` + `dell` | planeado |
| homelab-ai | Lab 4 · Ollama servido por Tailscale, evaluación de GPU | `minimac` | planeado |
| homelab-cloud | Lab 5 · Módulos Terraform multi-cloud (AWS + Azure) con presupuesto | runner | planeado |

## Roadmap

1. **Red y base** — Tailscale en las tres máquinas, SSH con llaves, `homelab-dotfiles`.
2. **Lab 1 GitOps** en `minimac` con un "proyecto víctima" (API pequeña + Helm chart + k6).
3. **Lab 2 Proxmox** en `aorus`.
4. **Lab 3 Mobile CI**, **Lab 4 IA local**, **Lab 5 Multi-cloud**.

El estado real se lleva en los [issues](https://github.com/Carlosposada-Dev/homelab/issues) de este repo.

## Crear un lab nuevo

```bash
gh repo create Carlosposada-Dev/homelab-<proposito> \
  --template Carlosposada-Dev/homelab-template \
  --public --clone \
  --description "Lab N · <qué hace, en una línea>"
cd homelab-<proposito>
gh repo edit --add-topic homelab --add-topic devops
```

Luego pega en Claude el prompt de [`prompts/new-lab-repo.md`](prompts/new-lab-repo.md).

## Prompts

- [`prompts/machine-setup.md`](prompts/machine-setup.md) — para preparar una máquina nueva del homelab con Claude.
- [`prompts/new-lab-repo.md`](prompts/new-lab-repo.md) — para arrancar un repo `homelab-<propósito>` recién creado desde la plantilla.

## Decisiones

Las decisiones de arquitectura se registran como ADR en [`docs/adr/`](docs/adr/).
