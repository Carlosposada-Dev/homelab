# Prompt · preparar una máquina del homelab

Pégalo en Claude (Claude Code o la app) en la máquina que vas a preparar. Deja solo una de las dos variantes del final.

---

Soy Cloud DevOps Engineer. Trabajo a diario con AWS y Azure, Kubernetes, Terraform, Docker, CI/CD con GitHub Actions y Azure Pipelines, y doy soporte a apps móviles en Flutter. Estoy armando un homelab con tres computadores personales para practicar lo que hago en el trabajo, construir portafolio y montar servicios útiles para mi día a día. Quiero que actúes como mi ingeniero de plataforma: evalúa esta máquina, confirma su rol dentro del homelab y ayúdame a dejarla lista paso a paso.

## Fuente de verdad

Todo lo que describe el homelab vive en https://github.com/Carlosposada-Dev/homelab : arquitectura (`docs/architecture.md`), inventario por máquina (`docs/inventory/`), convenciones (`docs/conventions.md`) y ADRs (`docs/adr/`). Léelo antes de proponer nada. Si lo que ves en esta máquina no coincide con el inventario, lo corregimos en el repo.

Resumen para que no tengas que ir al repo por lo básico:

| Hostname | Equipo | Rol |
|---|---|---|
| `minimac` | Mac mini M4 · 16 GB · 256 GB + 1 TB externo APFS `Devops` · macOS 27 | Servidor siempre encendido y estación principal. Ya listo: OrbStack (Docker + k3d), kubectl/helm/k9s, Terraform/OpenTofu, AWS y Azure CLI, gh, mise, Ghostty, VS Code Insiders, Xcode 27, Flutter 3.47, Tailscale. Correrá k3d + ArgoCD + Prometheus/Grafana/Loki, runner self-hosted de GitHub Actions, Ollama. |
| `aorus` | AORUS Elite AX V2 · Ryzen 5 3600 · 48 GB · 1 TB NVMe + 480 GB SSD + 1 TB HDD · Windows hoy | Laboratorio pesado bajo demanda con Proxmox VE, encendido por Wake-on-LAN: clúster k8s de 3 VMs con Terraform + Ansible, NAS de backups. |
| `dell` | Dell · i7 11ª gen · Iris Xe · 32 GB · 1 TB · Windows 11 hoy | Cliente móvil: SSH y VS Code Remote-SSH hacia `minimac`, build de Android, nodo extra en casa. |

Las tres se unen por **Tailscale**. Un cuarto portátil del trabajo (HP) **queda totalmente fuera**; no lo incluyas en ningún plan.

## Estándares

- Todo como código en repos `homelab-<propósito>` (GitHub `Carlosposada-Dev`), creados desde `homelab-template`. Dotfiles compartidos con `chezmoi` en `homelab-dotfiles`.
- SSH solo con llaves; secretos con `sops` + `age`; `gitleaks` + `pre-commit`; `trivy` para imágenes.
- Observabilidad centralizada en `minimac`; cada máquina expone `node_exporter`.
- Backups 3-2-1: local → NAS en `aorus` → nube barata (Backblaze B2 / S3 Glacier).
- Herramientas libres y gratuitas por defecto; si algo de pago vale la pena, dímelo con el costo.
- Documentación en español, fechas absolutas, Conventional Commits.

## Labs, en orden

1. **GitOps** en `minimac` (`homelab-gitops`).
2. **Proxmox** en `aorus` (`homelab-proxmox`).
3. **CI móvil Flutter** iOS en `minimac`, Android en `dell`/`aorus` (`homelab-mobile-ci`).
4. **IA local** con Ollama (`homelab-ai`).
5. **Multi-cloud** AWS + Azure con presupuesto (`homelab-cloud`).

## Lo que quiero que hagas en esta máquina

1. **Evalúa el equipo**: hardware real, sistema, espacio, qué hay instalado, qué sobra, qué está desactualizado. Dime qué quitar y qué falta para su rol.
2. **Plan por fases** con tiempos. Primero lo que desbloquea a las demás máquinas: Tailscale, hostname correcto, SSH con llaves, `node_exporter`, dotfiles.
3. **Ejecútalo conmigo paso a paso.** Pregunta antes de cualquier acción destructiva o que pida contraseña de administrador; muestra qué hará cada comando; papelera antes que borrado.
4. **Documenta** para el hub: actualiza `docs/inventory/<hostname>.md` del repo `homelab` con lo que encontremos y lo que dejemos instalado, y propón los archivos de Terraform/Ansible/chezmoi que apliquen en el repo del lab correspondiente.
5. Cierra con un **checklist de verificación** y **qué sigue** en las otras máquinas.

Responde en español. Comandos exactos, archivos exactos, sin teoría de relleno.

## Máquina donde estoy ahora

<!-- Deja solo UNA variante -->

### Variante A · `aorus`
Estoy en el **Aorus**, el laboratorio pesado. Hoy tiene Windows. Quiero decidir contigo si instalo Proxmox VE directo en el NVMe y qué hago con Windows (eliminarlo, pasarlo a una VM o dual boot), cómo reparto los discos (NVMe → VMs, SSD 480 → ISOs y templates, HDD → backups/NAS), y cómo configuro Wake-on-LAN en BIOS y red para encenderlo desde `minimac` y el celular. Confirma también qué GPU tiene instalada: el Ryzen 5 3600 no trae gráficos integrados. Después del hipervisor: las primeras VMs con Terraform + Ansible.

### Variante B · `dell`
Estoy en el **Dell**, el cliente móvil. Tiene Windows 11. Quiero decidir contigo entre (a) WSL2 con Ubuntu bien configurado, (b) dual boot con Linux o (c) reemplazar Windows por Linux (Fedora o Pop!_OS), según qué tan bien funcione el hardware con Linux. Luego: Tailscale, llaves SSH hacia `minimac`, VS Code con Remote-SSH, Android Studio + SDK para Flutter, y los dotfiles de `homelab-dotfiles` con chezmoi.
