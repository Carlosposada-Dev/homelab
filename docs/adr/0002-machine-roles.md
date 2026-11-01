# ADR 0002 · Rol de cada máquina

- **Fecha:** 2026-11-01
- **Estado:** aceptada

## Contexto

Hay tres máquinas personales con perfiles distintos: una Mac mini M4 (16 GB, silenciosa, ~5 W en reposo, única capaz de compilar iOS), un PC de escritorio con Ryzen 5 3600 y 48 GB (ruidoso, ~100 W, mucho disco, ampliable) y un portátil Dell i7 con 32 GB. Un cuarto equipo (HP del trabajo) existe pero pertenece al cliente.

## Decisión

| Máquina | Rol |
|---|---|
| `minimac` | Servidor siempre encendido: Kubernetes ligero (k3d), GitOps, observabilidad, runner de CI, Ollama, backups. También estación de trabajo principal y build de iOS. |
| `aorus` | Laboratorio pesado bajo demanda con Proxmox: VMs, clúster k8s "real", NAS. Encendido por Wake-on-LAN solo cuando se necesita. |
| `dell` | Cliente móvil: trabaja contra `minimac` por SSH; build de Android; nodo extra cuando está en casa. |
| HP del trabajo | Fuera del homelab, sin excepciones. |

## Consecuencias

- El consumo eléctrico base lo marca solo la Mac mini. El Aorus no suma coste mientras está apagado.
- Los 16 GB de la Mac mini obligan a disciplina: nada corre permanentemente si no se usa (por eso se retiraron MongoDB, MySQL, Docker Desktop, etc. el 2026-11-01).
- Cualquier cosa que necesite más de ~8 GB de RAM o varias VMs va al Aorus, no a la Mac mini.
- La separación estricta del HP evita mezclar credenciales o código del cliente con el homelab.
