# TalentScout

Plataforma full-stack de reclutamiento de talento. Dos paquetes independientes gestionados como submódulos de Git.

## Estructura del repositorio

```
talent-scout/              (repositorio raíz)
├── talentscout-backend/   → NestJS 11, PostgreSQL 17, Drizzle ORM, Bun
├── talentscout-front/     → Next.js 16, React 19, Tailwind CSS v4, Bun
├── .gitmodules            → configuración de submódulos
└── AGENTS.md              → convenciones del proyecto
```

## Requisitos

- [Bun](https://bun.sh) 1.2+
- [Docker](https://docker.com) (para la base de datos)
- Node.js 22+

## Primeros pasos

Al clonar el repositorio por primera vez, inicializa los submódulos:

```bash
git clone https://github.com/bguzmanm/talent-scout.git
cd talent-scout
git submodule update --init --recursive
```

Cada submódulo es un proyecto independiente con su propio remoto:

| Submódulo | Remoto |
|-----------|--------|
| `talentscout-backend` | https://github.com/bguzmanm/talentscout-backend |
| `talentscout-front` | https://github.com/bguzmanm/talentscout-front |

Para actualizar los submódulos al último commit de su rama `main`:

```bash
git submodule update --remote --merge
```

## Comandos principales

Cada submódulo se gestiona por separado. Los comandos se ejecutan desde cada directorio:

### Backend (`talentscout-backend/`)

```bash
bun install            # instalar dependencias
bun run start:dev      # servidor de desarrollo (puerto 3000)
bun run test           # tests unitarios (Jest)
bun run docker:up      # levantar PostgreSQL
bun run db:generate    # generar migración
bun run db:migrate     # ejecutar migración
bun run db:seed        # cargar datos de prueba
```

### Frontend (`talentscout-front/`)

```bash
bun install            # instalar dependencias
bun dev                # servidor de desarrollo (puerto 3001)
bun run build          # build de producción
```

## Convenciones

Ver [`AGENTS.md`](./AGENTS.md) para convenciones detalladas del proyecto, incluyendo stack, scripts y reglas de estilo.
