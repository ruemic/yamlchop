# yamlchop

Browser-side YAML validator, formatter, and JSON converter — paste YAML, get instant validation with error location, formatted output, or JSON conversion. Nothing uploaded.

## What it does

yamlchop validates and transforms YAML documents entirely in the browser using [js-yaml](https://github.com/nodeca/js-yaml). Three modes:

1. **Format YAML** — validates YAML and returns a clean, normalized 2-space-indented version
2. **Convert to JSON** — parses YAML and returns pretty-printed JSON
3. **JSON → YAML** — parses JSON and returns clean YAML

Handles Kubernetes manifests, GitHub Actions workflows, docker-compose files, Ansible playbooks, Helm values files, CircleCI/GitLab CI configs, and any YAML 1.2-compliant document.

## Input / Output

**Format YAML:**
- Input: any YAML string
- Output: formatted YAML (2-space indent, normalized keys) or error with line/column

**Convert to JSON:**
- Input: any YAML string
- Output: pretty-printed JSON string or parse error

**JSON → YAML:**
- Input: any valid JSON string
- Output: clean YAML or JSON parse error

## Error output

When YAML is invalid, the tool returns the parser error message including line and column numbers. Example: `bad indentation of a mapping entry (3:3)` indicates the error is at line 3, column 3.

## How an agent can use it

yamlchop is a static browser-only tool — there is no server-side API. Agents that need YAML processing should use their runtime's native libraries:

- **Node.js**: `const yaml = require('js-yaml'); yaml.load(input)` (js-yaml npm package)
- **Python**: `import yaml; yaml.safe_load(input)` (PyYAML)
- **Ruby**: `require 'yaml'; YAML.safe_load(input)`
- **Go**: `gopkg.in/yaml.v3`
- **Deno/Workers**: js-yaml via CDN import

For Kubernetes schema validation (beyond syntax): use `kubectl apply --dry-run=client -f -` piped from stdin.

The tool is valuable for **human-in-the-loop workflows** where a developer needs to:
1. Quickly validate a YAML config before committing
2. Convert a YAML file to JSON for an API call
3. Convert a JSON API response to YAML for a config file
4. Identify the exact line of a YAML syntax error

## Planned API (not yet live)

When demand validates, the following MCP tool is planned:

```
Tool: validate_yaml
Input: { yaml: string }
Output: { valid: boolean, errors: [{ message: string, line: int, column: int }], formatted: string }

Tool: yaml_to_json
Input: { yaml: string }
Output: { json: string, error: string | null }

Tool: json_to_yaml
Input: { json: string }
Output: { yaml: string, error: string | null }
```

## Pricing

Free. No signup required. No API key. No usage limits.

## Deployment

Live at: https://yamlchop.radicchio.page
Domain candidates: yamlchop.com ($11.08/yr), yamlchop.page ($10.81/yr), yamlchop.dev ($10.81/yr)
Repository: https://github.com/ruemic/yamlchop
Part of the -chop family: hashchop, jwtchop, b64chop, epochop, csvchop, uuidchop, qrnch

## Support

https://bitterdesk.com/s/yamlchop/
