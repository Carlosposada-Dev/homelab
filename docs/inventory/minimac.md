# minimac · Mac mini M4

Inventario al 2026-11-01, tras la limpieza y puesta a punto.

## Hardware

| | |
|---|---|
| Modelo | Mac mini (2024), Mac16,10, MU9D3LL/A |
| Chip | Apple M4 · 10 núcleos CPU (4P + 6E) · GPU 10 núcleos · Metal 4 |
| RAM | 16 GB unificada (no ampliable) |
| Disco interno | 256 GB SSD · ~105 GB libres |
| Disco externo | 1 TB NVMe en dock Ugreen · USB 3.2 Gen2 (10 Gb/s) · APFS · volumen `Devops` |
| Pantalla | HP V24v G5 · 1920×1080 @ 75 Hz |
| Teclado | Logitech K235 (receptor USB) · distribución Latinoamericano · Alt izq ↔ Cmd |

## Sistema

- macOS 27.2 · FileVault activo · Xcode 27.2 con licencia aceptada.
- Arranca al iniciar sesión: Raycast. Pendiente activar: Tailscale, OrbStack, Shottr.

## Herramientas

| Área | Herramientas |
|---|---|
| Runtimes (mise) | Node 26 LTS · Terraform 1.17 · tflint |
| Python | python3 (brew) · uv / uvx |
| Contenedores | OrbStack (Docker + Kubernetes) · lazydocker |
| Kubernetes | kubectl · helm · k9s · kubectx · kustomize · stern · k3d · eksctl |
| IaC | terraform · opentofu · terragrunt · tflint · pre-commit |
| Nube | aws-cli 2.39 · azure-cli 2.91 · gh |
| Seguridad | trivy · sops · age · gitleaks |
| Terminal | Ghostty · zsh + starship · fzf · zoxide · bat · eza · yq · jq · btop · delta · direnv |
| Móvil | Flutter 3.47.9 (fvm) · Xcode 27.2 · Android Studio + SDK 36 · CocoaPods · scrcpy |
| Editor | VS Code Insiders (`code`) |
| Datos | DBeaver · MongoDB Compass · Postman |
| Otros | Raycast · Shottr · Tailscale · OBS · VLC · Claude |

## Servicios previstos

| Servicio | Estado | Repo |
|---|---|---|
| Tailscale | instalado, falta login | — |
| k3d + ArgoCD + Prometheus/Grafana/Loki + Traefik | pendiente | homelab-gitops |
| Runner self-hosted GitHub Actions | pendiente | homelab-gitops |
| Ollama | pendiente | homelab-ai |
| Time Machine → `Devops` | pendiente | — |

## Historial

- **2026-11-01** — Limpieza completa: fuera Cursor, Warp, Termius, Teams, Docker Desktop, ChatGPT, Vysor, React Native Debugger, Mounty/macFUSE/iBoysoft, Jenkins, SonarQube, JMeter, Locust, MongoDB, MySQL, PostgreSQL, nvm. Entra el stack DevOps completo, OrbStack, Ghostty, Shottr, mise, Flutter 3.47. Node 16 → 26. Disco libre 79 GB → 105 GB.
