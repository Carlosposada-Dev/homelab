# Arquitectura

## Principio

**`minimac` es el cerebro que nunca se apaga, `aorus` es el músculo que se enciende bajo demanda y `dell` entra a todo desde donde esté.** Las tres forman una sola red privada con Tailscale.

```mermaid
flowchart LR
  subgraph ts[Tailscale · red privada]
    direction LR
    minimac["minimac · Mac mini M4\nsiempre encendido\nk3d · ArgoCD · Grafana · Loki\nrunner GitHub Actions · Ollama\nTime Machine → disco Devops"]
    aorus["aorus · Ryzen 5 3600 · 48 GB\nbajo demanda (WoL)\nProxmox VE\nk8s 3 VMs · NAS backups"]
    dell["dell · i7 11ª gen · 32 GB\ncliente móvil\nVS Code Remote-SSH\nAndroid build"]
  end
  phone["celular"] -. Tailscale .-> minimac
  phone -. WoL .-> aorus
  dell -- ssh / code --remote --> minimac
  minimac -- terraform + ansible --> aorus
  minimac -- node_exporter / loki --> aorus
  gh["GitHub\nhomelab-*"] -- ArgoCD pull --> minimac
  gh -- jobs --> minimac
  minimac -- iOS build --> gh
  dell -- Android build --> gh
  cloud["AWS · Azure\nsandbox"] <-- runner self-hosted --> minimac
```

## Flujos principales

| Flujo | Camino |
|---|---|
| Despliegue de una app al clúster | push a `homelab-*` → GitHub Actions (runner en `minimac`) construye imagen → ArgoCD en `minimac` sincroniza desde el repo |
| Aprovisionar una VM en `aorus` | `terraform apply` desde `minimac` contra la API de Proxmox → Ansible configura la VM |
| Trabajar desde fuera de casa | `dell` → Tailscale → SSH / VS Code Remote a `minimac` |
| Encender el lab pesado | celular o `minimac` envían Wake-on-LAN a `aorus` |
| Observabilidad | cada máquina expone `node_exporter`; Prometheus y Loki en `minimac` recolectan; Grafana muestra |
| Backups 3-2-1 | `minimac` → Time Machine en disco `Devops` → copia en NAS de `aorus` → copia fría en Backblaze B2 / S3 Glacier |

## Lo que queda fuera

- El portátil del trabajo (HP, EPAM/Nequi) no participa en ninguna parte del homelab.
- Nada del homelab expone puertos a Internet; todo acceso remoto pasa por Tailscale.
