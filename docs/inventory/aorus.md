# aorus · PC de escritorio

Inventario al 2026-11-01. Pendiente de evaluar en sitio con [`prompts/machine-setup.md`](../../prompts/machine-setup.md) (variante A).

## Hardware

| | |
|---|---|
| Placa | AORUS Elite AX V2 |
| CPU | AMD Ryzen 5 3600 · 6 núcleos / 12 hilos |
| RAM | 48 GB DDR4: 32 GB @ 3200 MHz + 16 GB @ 3000 MHz (Corsair Vengeance). Corre a la velocidad del kit más lento. |
| GPU | ninguna dedicada (el Ryzen 5 3600 no tiene gráficos integrados: se necesita una GPU para tener video; confirmar cuál está instalada) |
| Discos | 1 TB NVMe · 480 GB SSD SATA · 1 TB HDD |
| Red | Ethernet 2.5 GbE + Wi-Fi (verificar soporte Wake-on-LAN en BIOS) |

## Sistema

- Windows (por confirmar edición). Candidato a Proxmox VE.

## Plan

- Hipervisor: Proxmox VE en el NVMe. Windows a VM o eliminado (ADR pendiente).
- Reparto de discos: NVMe → VMs; SSD 480 → ISOs y templates; HDD 1 TB → NAS/backups.
- Wake-on-LAN desde `minimac` y celular.
- Primeras VMs: 3 nodos k8s (Talos o k3s) + 1 Ubuntu de utilidades, con Terraform + Ansible.
