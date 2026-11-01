# Convenciones del homelab

## Nombres de repos

Patrón: **`homelab-<propósito>`**, en minúsculas y kebab-case, en inglés.

| Correcto | Incorrecto | Por qué |
|---|---|---|
| `homelab-gitops` | `homelab_gitops` | Sin guiones bajos (`python_fundamentals` fue la excepción histórica) |
| `homelab-mobile-ci` | `homelab-Mobile-CI` | Sin mayúsculas (`poc-GitHub-actions-CI-CD` fue la excepción histórica) |
| `homelab-proxmox` | `homelab-lab2-proxmox` | El número de lab va en la descripción, no en el nombre: el orden puede cambiar |
| `homelab-cloud` | `homelab-aws-azure-terraform` | Un propósito, no la lista de herramientas |

El prefijo `homelab-` agrupa los repos alfabéticamente en GitHub y permite filtrarlos con `gh repo list --json name -q '.[] | select(.name | startswith("homelab"))'`. El mismo criterio ya se usaba con `ccaf-s2-*` y `ccaf-s5-*`.

Excepción: el hub se llama `homelab`, sin sufijo, para que quede primero en la lista.

## Metadatos obligatorios en GitHub

- **Descripción** en una línea, en español, empezando por `Lab N ·` cuando aplique. Ejemplo: `Lab 1 · GitOps en k3d con ArgoCD, Prometheus, Grafana y Loki`.
- **Topics**: siempre `homelab` y `devops`; más los de la tecnología principal (`kubernetes`, `terraform`, `proxmox`, `flutter`, `ollama`, `aws`, `azure`).
- **Visibilidad**: público. Si algo no puede ser público, no va en el repo: va en `sops` + `age` o en un gestor de secretos.
- **Licencia**: MIT.

## Estructura de repo

Todo repo `homelab-<propósito>` nace de [`homelab-template`](https://github.com/Carlosposada-Dev/homelab-template):

```
.
├── README.md                 # qué es, qué máquina, cómo levantarlo, cómo verificarlo
├── docs/
│   ├── architecture.md       # diagrama (Mermaid) y decisiones de diseño
│   ├── adr/                  # un ADR por decisión importante
│   └── runbooks/             # cómo operar: levantar, apagar, respaldar, recuperar
├── infra/                    # Terraform / OpenTofu
├── config/                   # Ansible
├── k8s/                      # Helm, Kustomize, manifiestos de ArgoCD
├── scripts/                  # utilidades pequeñas (bash, python con uv)
├── .github/workflows/        # CI: pre-commit, gitleaks, lint
├── .pre-commit-config.yaml
├── .editorconfig
├── .gitignore
└── LICENSE
```

Las carpetas que un lab no usa se borran. Lo que no se borra se documenta.

## Git

- Rama principal: `main`, protegida. Trabajo en `feat/<tema>`, `fix/<tema>`, `docs/<tema>`.
- Commits con [Conventional Commits](https://www.conventionalcommits.org/): `feat(argocd): bootstrap app-of-apps`.
- Todo cambio entra por PR, aunque sea propio: deja rastro de por qué.
- `pre-commit` instalado en cada clon (`pre-commit install`). Mínimo: `gitleaks`, fin de línea, YAML válido; `tflint` donde haya Terraform.

## Seguridad

- SSH solo con llaves. Llave personal `~/.ssh/cposada`; la llave `work` nunca toca estos repos.
- Secretos cifrados con `sops` + `age`. La llave privada de `age` vive fuera del repo y se respalda en el gestor de contraseñas.
- Imágenes de contenedores escaneadas con `trivy` en CI.
- Nada del trabajo (EPAM, Nequi, Trumed) entra en el homelab: ni código, ni credenciales, ni datos.

## Documentación

- El README de cada lab responde en orden: **qué es**, **en qué máquina corre**, **cómo levantarlo**, **cómo verificar que funciona**, **cómo apagarlo**.
- Cada decisión que costó pensar es un ADR: contexto, opciones, decisión, consecuencias.
- Cada procedimiento que se repite es un runbook.
- Fechas siempre absolutas (`2026-11-01`), nunca "hoy" o "la semana pasada".
