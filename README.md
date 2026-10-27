# threat-modeling

> Encontrar los problemas de seguridad cuando todavía son una línea del plan.

**Modelo de amenazas** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Mapea activos, puntos de entrada, fronteras de confianza y actores, y recorre doce dominios (autenticación, autorización, aislamiento entre clientes, entradas, secretos, pagos, consumo de recursos, agentes de IA, móvil, cadena de suministro, infraestructura y logs) para listar amenazas concretas con probabilidad, impacto, mitigación y prueba.

## Objetivo

Que las mitigaciones importantes entren al plan antes de implementar, no como parche después.

## Cuándo usarla

- Un plan toca autenticación, datos personales o de pago, multi-tenant, endpoints públicos, agentes o infraestructura

## Cuándo no

- Cambios sin superficie de seguridad

## Ejemplo

```text
Haz el modelo de amenazas del plan de pagos con webhooks.
```

## Cómo se activa

Esta skill **se activa sola**: Claude Code lee su descripción y la carga cuando la tarea coincide. También puedes pedirla por nombre ("usa la skill threat-modeling") o invocarla con `/threat-modeling:threat-modeling` (plugin) o `/threat-modeling` (copiada a `.claude/skills/`).

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install threat-modeling@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `dev-workflow@nvvdev` en su lugar (incluye esta skill y las demás de [dev-workflow](https://github.com/nvv-dev/dev-workflow)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/threat-modeling.git /tmp/threat-modeling
mkdir -p .claude/skills
cp -R /tmp/threat-modeling/skills/threat-modeling .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/threat-modeling/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/threat-modeling
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `threat-modeling` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall threat-modeling@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/threat-modeling`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/threat-modeling/SKILL.md`](skills/threat-modeling/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/threat-modeling/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) (attack domains), [Hainrixz/cyber-neo](https://github.com/Hainrixz/cyber-neo) (reference lists), [Hainrixz/agente-pagokit](https://github.com/Hainrixz/agente-pagokit) (payment pitfalls).

## Licencia

MIT.

---

## English

**threat-modeling** — Assets, entry points and trust boundaries, then concrete threats across twelve domains with mitigations and tests.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install threat-modeling@nvvdev`, or copy `skills/threat-modeling/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/threat-modeling`. Loads automatically when the task matches its description. Canonical source: [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow). License: MIT.
